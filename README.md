This Repo is created for Project1 #10WeeksOfCloudOps hosted by Piyush Sachdeva

![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/f92c54a1-e938-4936-b153-2896b519745f)# TenWeeksCloud_static_s3


Prerequisites:

1. AWS Account: You can choose your cloud hosting provider, but for this guide, we will use AWS (Amazon Web Services) as an example.

2. Domain Name: You are free to select your domain registrar, we'll demonstrate using Namecheap as the hosting service for your domain.

3. GitHub Account: You may use any version control platform you prefer. We will illustrate using GitHub for version control and collaboration.

You can adjust the prerequisites according to your personal preferences and requirements.

Overview:
Hosting a static website on AWS by using an S3 bucket which can be accessed by the user.
The user will hit the DNS which is routed to Cloudfront service using OAI protocol to access the objects in the S3 bucket.

Architecture Diagram:

![Architecture_Presentation](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/bdc3a607-3943-4e89-8908-e7fca24c1ce4)

Step1 :
1. Create a Domain name of your choice, we have registered a domain name with an affordable price of about USD $1.16
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/a1e81426-a269-42dc-afec-a685d1872112)

Step2:
1. Create an S3 bucket with the name same as that of the registered domain name
   a. Search S3 in the AWS console
   b. Click on Create a bucket
      ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/4f9441ea-66d5-4795-a0d3-01eb77fe100d)

2. Enter the bucket name as the Domain name which was registered
   ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/563b8be7-c147-46eb-a082-6a48a34cb234)

3. Keep all the default settings as it is and click on Create Bucket. S3 Bucket is created.

Step3:
1. Once the S3 bucket is created click on the bucket name and browse to the properties section 

   ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/63fccbc7-f54a-4ffc-b4d6-4f0b71c6b338)

2. Scroll down to the Static website hosting section, click on edit and enable the static website hosting
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/57018de9-90de-49bc-8bdb-cd1a22c490e9)

3. Scroll down and enter index.html and error.html files (This is optional, good practice is to create those files) and save changes.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/8d764694-5ebf-4a3b-8412-a73eb889c675)

4. Browsing to the Objects section, we can upload any required files to the host.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/9035e547-50b8-4057-b11b-6392080c94d2)

5. If we browse in the properties section where we enabled the static website hosting, we will get the bucket endpoint URL
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/a49b53f8-e96a-4102-a350-cb4a21e25e23)
This URL is not accessible if we paste it browser, since we have restricted the permissions while creating the bucket. We will make it accessible in further steps using Cloud Front.

Step4:
1. Search for Cloud Front in AWS Console.
CloudFront is a content delivery network (CDN) service. It is designed to accelerate the delivery of web content, including images, videos, static assets, and dynamic content, by distributing it across a global network of edge locations. This helps reduce latency and improves the performance of web applications for end-users around the world.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/96cf5ab9-bdf4-4cfb-891c-22f93f43edbe)

2. Create Distribution
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/502d85cb-1438-4328-bf31-d9914b809615)

3. Choose the origin domain, the bucket will populated automatically
 ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/bcebdd5c-9794-4059-81a1-afbedd84f514)

4. There will be an origin name auto-populated
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/841bdd23-d655-49c9-9536-378005723a79)

5. Origin access we will select as Legacy access identities, to enable OAI (Origin Access Identity). OAI is a special CloudFront user that you can associate with your distribution to restrict access to your S3 content. It allows you to control who can access objects in an S3 bucket through CloudFront.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/6a6e379e-9db3-4a73-9851-a22bf4423c4d)

6. Click on Create New OAI, and select the bullet point as update the bucket policy, where aceess policy through OAI will updated automatically in the S3 bucket.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/10e36edc-f4a2-4767-a027-ff3ecc0fa638)

7. Let's keep the rest of the options as default and scroll down to Viewers where we select the bullet points as shown in the screenshot. we can choose the options as per our choice.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/c4f4d115-e272-446f-a30d-946c52bf4656)

8. Select the Web Application Firewall
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/d1500665-2c0f-4c60-b748-9e550712a1fa)

9. Add the Alternate Domain name
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/943f4726-1c59-42f0-b0ee-91bff415c6ad)

10. Will keep the rest of the settings as default, scroll to Custom SSL certificate and click on Request Certificate
 we need to make sure the certificate is in the us-east-1 region   
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/2a6f4207-9bc3-45c4-9e53-426196da3c9d)

Step5:
1. A new tab opens where we select request for a public certificate and click on next.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/7a0b8918-fe5e-4c28-8c03-c39e7a60db1f)

2. Will keep the Validation method as DNS, keep the default settings and hit request. The certificate will be pending validation
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/d608d595-adbb-45db-884f-1c44b5f13a18)

3. click on the certificate which shows the status as pending validation and has CNAME and CNAME value (the below screenshot was captured after the validation)
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/47ada9ed-fe33-4e8e-a66f-af6c70387650)

4. The CNAME and CNAME value need to be added in the domain registrar where we created the Domain and then the DNS validation will be done. We will use NameCheap in the following step

Step6:
1. Go to the dashboard where the domain name is registered
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/79a39dba-0e50-4477-8bab-91bc19dbe329)
2. Click on Manage and browse to Advanced DNS settings
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/030e4504-b133-4e47-b29a-9a01b2801823)
click on add a new record, select record type as CNAME record, and select the value before the domain name starts like shown below to add it in the host section of NameCheap
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/4e7c2605-439a-4594-a8eb-28528d4a0092)
Similarly, For the target value we select the entire CNAME value excluding the . like shown in the screenshot and save.
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/0bf7f2ae-2f4f-4d12-92da-086662030ecc)
It will take a few minutes to complete the validation, click on refresh and the certificate will be issued. 

Step7:
1. Go to the CloudFront tab click on refresh and select the custom certificate that we generated
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/11ca70fd-fa5c-4402-855e-8b0aef97a6c6)

2. Let's name the default root object to avoid adding the home page in the URL every time we try to access it, we have used the file name beauty.html it can be any file.
   ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/bcc19129-fe52-4406-bffd-f46108c6acf8)

3. Click on Create Distribution
4. Once the Distribution is created we will have the domain name which will be accessible over the internet
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/eeee05cf-5aba-4f48-b077-8f93d234c0dd)

5. We can see the bucket permissions which were updated automatically for selecting the update bucket policy while creating the Distribution
   ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/e276496b-799e-45fc-a212-b3f4d7ff1b39)

6. The URL which was generated while creating the distribution needs to be added in NameCheap to redirect while we use the registered Domain name

Step8:
1. Redirect to NameCheap and add two CNAME records, where is1 record will have the hostname as www and target as the URL generated by CloudFront Distribution
2nd record will have the hostname as the domain name which we created in this example edrich.store and the target will be the URL generated by CloudFront Distribution
![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/4abb3d1e-5090-4773-b915-c8e05fafc3d4)


NOW WHEN WE USE URL: WWW.EDRICH.STORE THE PAGE WILL BE DISPLAYED IN THE BROWSER

Lets Continue to build a Pipeline
Step9:
1. Browse for Code Pipeline, click on create a new pipeline
2. Give the name to the pipeline and keep the default settings and click next
   ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/22b0989e-4265-42dd-9e83-df4f91c33233)

4. We can select the source provider which we have used in this project is Git Hub, we choose Git Hub (version)
   ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/b032d8fe-bd25-411f-9a75-ebc8d6d0ef93)

5. Connect to Git Hub by providing the credentials
6. We can select the required Repository from the dropdown
7. Select the Branch
8. Change detection portion we will select as Git Hub webhook i.e. when any changes are made in the repository the files are pushed to the S3 bucket through Code Pipeline
 ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/cb10cadc-7c9c-46c3-9380-0e1a4aff233a)

9. We will skip the build provider since we are hosting a static website from S3 bucket
    ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/d30ffa97-eb31-4a94-8a22-8d8f2a59a064)

10. Deploy provider will select Amazon S3, select the bucket name we created from the drop-down (www.edrich.store) and then click on create a pipeline
    ![image](https://github.com/edrichlewis/TenWeeksCloud_static_s3/assets/105597780/64296254-442f-4bd8-a283-a256a74b7363)
 
11. To validate go to Git Hub Repo make any changes and commit the changes, The Pipeline should be triggered and we can check in S3 storage if the changes are reflected in the bucket or we can browse the URL and check if changes made are reflected.

Here we complete our project of Hosting Static Website using S3 bucket and implementing the Pipeline

Learning:
1. DNS
2. Cloudfront - OAI, ACM certificate
3. S3 Storage
4. Cloud Pipeline


Reference:
https://www.youtube.com/watch?v=UVvc_RtOoWg&list=PLl4APkPHzsUUc8HOEIwfB3Z2uxRv2SKOG&index=2  - For more detailed video.

Thank you



