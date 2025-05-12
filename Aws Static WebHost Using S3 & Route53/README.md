## 🌐 Hosting a Static Website on AWS S3 + Route 53
This guide explains how to host a static website (like HTML/CSS/JS files) on Amazon S3 and map it to a custom domain using AWS Route 53.  
**Prerequisites**  
-> AWS Account  
-> Domain registered in Route 53 (or transfer one there)  
-> Static website files (e.g., index.html, styles.css, etc.)   
-> IAM permissions to create S3 buckets and Route 53 records  
**Step 1: Register for Route 53**
1. click on register Domain
2. give a domain name as you want
3. complete the formalities
4. resgister domain wait for 10-15 mins for create
5. recommand to take domain as .click
6. And Ensure domain name same to apply for S3 also

**Step 2: Create and Configure the S3 Bucket**
1. Go to the S3 service in AWS Console.
2. Click Create Bucket.
3. Set the Bucket Name to match your domain exactly (e.g., example.com).
4. Region: Choose the region you want (keep it consistent for easier management).
5. Uncheck Block All Public Access (important! for website access).
Click Create Bucket.

**Step 3: Upload Website Files**
1. Open your newly created bucket.
2. Click Upload > Add Files.
3. Select your index.html (and any other files like css, js, images).
Click Upload.

**Step 4: Enable Static Website Hosting**
1. In your S3 bucket, go to the Properties tab.
2. Scroll to Static Website Hosting.
3. Enable it.
For Index Document, enter: index.html
4. Save Changes

**Step 5: Make Files Public**
1. Go to the Permissions tab in the bucket.

2. Under Bucket Policy, click Edit.

Add the following Bucket Policy (replace YOUR_BUCKET_NAME with your bucket name):

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
3. Save the policy.

**Step 5: Set Up Domain Using Route 53**
1. Go to Route 53 in AWS Console.
2. Click Hosted Zones.
3. Find and open your domain name.
4. Click Create Record.
 - Record Name: leave empty to map root domain (or type www if creating a subdomain).
 - Alias: Yes
 - Alias Target: Click and choose your S3 bucket's static website hosting endpoint (it will auto-populate).
 - Alias Region : Enter your region you are hosting.
5. Save the record.
6. Now go and check the website domain name in google search it is hosted or not(use the Domain Name Which you given).

### Done! ###
**Now your static website is live on your custom domain via AWS S3 and Route 53!**
