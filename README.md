# SCA_LAGOS
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

AWS account credentials with permissions to create S3 buckets, IAM users, and policies.




To create s3 bucket using Aws cli you must have IAM user with s3 full access.

![](./images/7.png)




![](./images/8.png)



![](./images/9.png)

![](./images/10.png)



![](./images/11.png)

![](./images/12.png)


![](./images/13.png)


![](./images/14.png)

![](./images/15.png)

![](./images/16.png)



## RESEARCH AND HOST A SIMPLE WEBSITE ON S3


By default, any object that you upload in the s3 bucket is made private .it can not be made public.


Create the bucket `sca-lagos`

![](./images/17.png)


OPen the bucket, click on upload, add files, drag and drop all the files and click upload and all the files will be uploaded.

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



















## CLOUDFORMATION


- Set up LAMP stack webserver using cloudformation. On your webserver Echo "sample web from SCAlagos TDD" created by your name and attendance number.

- Let your webserver instance vpc and other resources be created with the suffix scatdd_your name_xxx.

- Run your webserver and capture the screen, save screen shot on your repo .

- Add readme that explains how to run the script.

- Save your script to github repo and submit to the SCATDD assignment form.





__TERMINOLOGIES IN CLOUDFORMATIONS__

- TEMPLATES: Are the text files or the script of cloud formation, but not scripts in programming language. You can write them in YAML or JSON format.

Cloud formation will read templates as an input and the output will be resource that will create and maintain the stack

Textfiles- YAML or JSON

Here is an example of an AWS CloudFormation YAML template that creates a simple setup with an EC2 instance and a security group


```
AWSTemplateFormatVersion: '2010-09-09'
Description: A simple AWS CloudFormation template to create an EC2 instance with a security group.

Resources:
  MyEC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0c55b159cbfafe10
      SecurityGroups:
        - Ref: MySecurityGroup
      KeyName: MyKeyPair  

  MySecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupDescription: Allow SSH and HTTP access
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '22'
          ToPort: '22'
          CidrIp: '0.0.0.0/0'
        - IpProtocol: tcp
          FromPort: '80'
          ToPort: '80'
          CidrIp: '0.0.0.0/0'

Outputs:
  InstanceId:
    Description: The Instance ID of the newly created EC2 instance
    Value: !Ref MyEC2Instance
  PublicIP:
    Description: The public IP address of the newly created EC2 instance
    Value: !GetAtt MyEC2Instance.PublicIp
```



__SOLUTION__
 


We'll go to cloudformation service

![](./images/37.png)

![](./images/38.png)



We will create a directory and name it `cloudformation` then cd into the directory and open in our text sublime editor vscode using `code ..`

![](./images/39.png)

Go to `file` and `open folder`

![](./images/40.png)

Go to the location where you have the directory and select folder.

![](./images/41.png)


Then create a file `example.yaml`

![](./images/42.png)


Your templates

![](./images/50.png)

![](./images/51.png)




To get you `AMI ID`

![](./images/43.png)


Create a stack

![](./images/44.png)



Choose an existing template, upload a template, choose a file(find your template and upload)

![](./images/45.png)


Provide a stack name `SCATDD` and submit

![](./images/46.png)



Our stack is completed, and our instance is running

![](./images/47.png)

![](./images/48.png)


But if our instance doesn't have tag, to give it a tag we'll update our stack and make changes to our template, go to your sublime text(vscode) and create another file and name it `updated.yaml` and give list of tags, give your instance a name `scatdd_ogechukwu_instance`


![](./images/52.png)

![](./images/53.png)

![](./images/49.png)

![](./images/54.png)

Our update is complete


![](./images/55.png)



Install Necessary Softwares

`sudo yum update -y` 

`sudo yum install httpd php mysql -y`


`sudo systemctl start httpd`: Starts the Apache HTTP server.

`sudo systemctl enable httpd`: Configures Apache to start on boot.

`sudo systemctl status httpd`


![](./images/57.png)


![](./images/58.png)

































































































































