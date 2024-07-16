## S3 BUCKET AND IAM 


- create s3 bucket from cli, name of s3 bucket should be your name_scalagos.

- create IAM user 

- Attach a policy to read s3 bucket AmazonS3ReadOnlyAccess.

- create Access keys for the user.

- create a git repo and push your script to the repo with process screenshot, name user sca_lagos

__solutions__


Open Aws console, search for s3. To create s3 bucket on console

![](./images/1.png)

Create an s3 bucket name `ogechukwu-scalagos`

![](./images/2.png)


For object ownership keep it disabled, so s3 can also provide access based on access control list, the Aws account users can be given the access to the s3 bucket, but most of the bucket permission will be through policies. But when we want to make the s3 bucket public, then we need to enable ACL(Access control list).

![](./images/3.png)


__Bucket versioning:__ Enabling versioning on an S3 bucket helps you preserve, retrieve, and restore every version of every object stored in the bucket. 


![](./images/4.png)

__Encryption type__

- server side encryption with Amazon s3 managed keys (means the encryption keys will be managed by Amazon s3, it's the cheapest option)

- then you have encryption with KMS (you can create your own encryption key by using Aws kms service but it's not free)

- Dual layer of encryption (the pricing will increase)


![](./images/5.png)

AWS CLI must be installed and configured with the necessary permissions.

- open your powershell as an administrator 

- run the command `choco install awscli` and open through git bash




To create s3 bucket using Aws cli you must have IAM user with s3 full access.

![](./images/7.png)




![](./images/8.png)



![](./images/9.png)



![](./images/10.png)

when the user is created, click on the username, go to the security crendentials and create the access keys

![](./images/11.png)

![](./images/12.png)



![](./images/13.png)

- open your powershell as an administrator and run the command 

`choco install awscli`

- open through git bash and configure aws cli

`aws --version`

`aws configure`

![](./images/14.png)

![](./images/15.png)

![](./images/16.png)



## RESEARCH AND HOST A SIMPLE WEBSITE ON S3


By default, any object that you upload in the s3 bucket is made private .it can not be made public.


Create the bucket `sca-lagos`

![](./images/17.png)


Open the bucket, click on upload, add files, drag and drop all the files and click upload and all the files will be uploaded.

![](./images/18.png)



![](./images/19.png)


![](./images/20.png)


We will create one more bucket to store the access logs of our website `sca-lagos2`

![](./images/21.png)


We will make it public, go to permission and edit


![](./images/22.png)


Go to block all public access and uncheck it, then save and confirm.


![](./images/23.png)


Then for object ownership, we will enable the ACL and save changes.


![](./images/24.png)



![](./images/25.png)


Go to the objects and select all of them, go to action and make public using ACL 

![](./images/26.png)


![](./images/27.png)


The warning says it will be available on everybody on the internet. All the object are public but the website is accessed through the main index page `index.html`

![](./images/28.png)


Go to properties, there is an option static website hosting, click on edit and enable it. The document is index.html then save changes.

![](./images/29.png)


![](./images/30.png)


![](./images/31.png)

You will get the URL

![](./images/32.png)

For the access logs, enable it, specify the bucket browse it and choose the bucket and destination and save changes.

![](./images/33.png)


![](./images/34.png)

Go the static website hosting and copy the URL, put it in the browser

![](./images/35.png)

The result


![](./images/36.png)
