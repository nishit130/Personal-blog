---
layout: post
title:  "How to create custom signed URLs"
author: "Nishit Patel"
date:   2023-06-01 14:46:01 +0530
comments: True
categories: Tutorials
collectionpage: signed-url
feature: False
excerpt: "In today's cloud-based world, secure and efficient access to private resources stored on cloud platforms is crucial. One of the ways to provide secure access to these resources is by using Signed URLs...."
---

![signed-url-blog.png](../../../../assets/img/signed-url-blog.png)

In today's cloud-based world, secure and efficient access to private resources stored on cloud platforms is crucial. One of the ways to provide secure access to these resources is by using Signed URLs. Signed URLs allow users to access private objects on cloud platforms like Amazon Web Services (AWS) S3 and Google Cloud Storage (GCS).

A signed URL is a special type of URL that includes a signature, or token, that verifies the identity of the user or application making the request to access a specific resource, such as an object stored in GCS/S3 bucket. This token allows the server to confirm that the user or application has the necessary permissions to access the resource and prevent unauthorized access.

Major cloud platforms like AWS and GCP provide functionality of signed URL but they have a limitation on the expiry of the URL. We can set maximum expiry time to only 7 days. To overcome this constraints of expiry In this blog you will learn how to create your own custom signed url’s for your usecase.

So, why should you care about custom signed URLs? Consider these scenarios:

- You need to provide limited access to private resources for a temporary period, without granting permanent rights.
- You wish to let users download files without going through tedious multiple authentication.
- You intend to generate time-limited URLs, specifically for sharing resources based on your product’s RBAC.

Imagine owning an e-learning platform where students can access various course materials, from lecture videos and presentation slides to supplementary documents. To accommodate their learning journey, you want to offer them access for an extended period, perhaps the entire semester. Here's where you encounter a roadblock: the 7-day expiry limit imposed by AWS and GCS. To bypass this hurdle, you need a custom implementation of the signed URL feature.

This is how high level architecture is going to look like.

![shapes.png](../../../../assets/img/shapes.png)

Users will send a `Get` request to your backend API server through a signed URL. The response to this request will be determined by the parameters in the signed URL. To qualify as a signed URL, the custom signed URL should adhere to the following three principles:

1. **Time-Limited Access:** The URL is a temporary passport, bearing an expiration time or duration that restricts access to a specific timeframe.
2. **Controlled Access Permissions**: The URL must carry the necessary access permissions, much like a VIP pass for a specific event, granting entry only for the requested operation.
3. **Secure Authentication and Authorization**: The URL must ensure that only those bearing proper credentials can access the resource.

### URL Structure

Here's a blueprint of your signed URL

![shapes (2).png](../../../../assets/img/shapes (2).png)

The `token` parameter serves as the [HMAC (Hashed Message Authentication Code)](https://en.wikipedia.org/wiki/HMAC){:target="_blank"}, a cryptographic signature formed using a secret key and the other URL parameters. It guarantees the integrity and authenticity of the signed URL, making any alterations in the parameters futile by invalidating the URL. <br>
`expiry` parameter helps in defining the expiry of the url while generating it. <br>
`user_id` parameter or any other unique identifier can be used, will help in verifying that user has authorization to access the content requested by the singed url.
Here is an illustrative python code snippet for generating signed URLs:

```python

BASE_URL = "http://api-server.com/"

def generate_signed_url(user_id, object_name, expiry):
    try:
	# Create new secret-key or user existing from db
        encrypted_secret = get_signed_url_secret_from_id(user_id)

        if encrypted_secret is None:
            encrypted_secret = generate_secret_key(user_id)
				
        # decrypt secret key
        secret = decrypt_with_prefix_iv(encrypted_secret)
				
	# add expiry of 91 days
        expiry = datetime.datetime.now() + datetime.timedelta(days=91)
        expiry_timestamp = int(expiry.timestamp() * 1000)

        signed_url = f'{BASE_URL}/endpoint?user_id={str(user_id)}&expiry={str(expiry_timestamp)}&object={object_name}'

        data = {
	        "user_id": str(user_id),
		"object_name": object_name,
	        "expiry": str(expiry)
	}
        hmac_code = generate_code(data, secret)
        signed_url += "&token=" + hmac_code
        return signed_url

    except Exception as e:
        pass # Error handling
        return None
```

### Backend API

Let’s define the Backend logic for serving the requested content whenever a `Get` request is made to our `https://api-server.com/endpoint` . Here is the pseudo python code for implementation of the api.

```python
@app.get("/endpoint")
def get_course_ppt(user_id: UUID, object_name: str, expiry: int, token: str) -> Response:
    # Check if URL is expired
    if expiry < int(datetime.now().timestamp() * 1000):
        return Response(status=400, entity="URL is expired")

    # fetch secret-key for user
    encrypted_secret = userUtil.get_signed_url_secret_from_id(user_id)
		
    # decrypt encrypted secret-key stored in db
    secret = AESUtil.decrypt_with_prefix_iv(encrypted_secret)

    data = {
        "user_id": str(user_id),
	"object_name": object_name,
        "expiry": str(expiry)
    }
		
    # check if caclulated hmac is same as token
    if HmacUtil.matches(data, secret, token): 
        # Fetch object from GCS/S3       
        ppt = GoogleStorageUtils.get_file_as_is(bucket_name, object_name)

        return Response(status=200, entity=ppt,
                        media_type=MediaType.APPLICATION_OCTET_STREAM,
                        headers={HttpHeaders.CONTENT_DISPOSITION: 'attachment;
                                 filename="' + object_name + '"'
                        })
    else:
        return Response(status=401, entity="Invalid URL")

    # Exception handling
    except Exception as e:
        logger.error(e)
        return Response(status=500, entity="Some error occurred")
```

We check if calculated value of HMAC matches the `token` to make sure that the url parameters are not tampered by the third party.

### Conclusion

Concluding, signed URLs are your trusted allies in securing access to your cloud-hosted private resources. However, the 7-day expiry limit can sometimes be a hindrance. Creating custom signed URLs, honoring the principles of time-limited access, controlled access permissions, and secure authentication and authorization, is a savvy way to circumvent this challenge. This strategy empowers you to provide temporary access to your resources while ensuring optimal security and control.


