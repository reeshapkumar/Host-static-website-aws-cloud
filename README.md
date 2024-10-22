# Host Static Website Aws Cloud

Creating a static website on AWS involves using various services like Amazon S3 for hosting, Amazon CloudFront for content delivery, and optionally Route 53 for domain management. Below are the steps to create a simple static website on AWS.

Project Overview
Create an S3 Bucket for storing your website files.
Upload Website Files to the S3 Bucket.
Configure S3 Bucket for Static Website Hosting.
Set Permissions for the S3 Bucket.
(Optional) Configure CloudFront for faster content delivery.
(Optional) Set Up a Custom Domain using Route 53.

**Step 1: Create an S3 Bucket**

Log in to the AWS Management Console.
Go to the S3 service.
Click on Create bucket.
Configure the bucket settings:
Bucket name: Enter a unique name (e.g., my-static-website).
Region: Choose your preferred AWS region.
Uncheck Block all public access (you will set permissions later).
Click on Create bucket.

**Step 2: Upload Website Files**

Prepare your static website files (HTML, CSS, JavaScript, images).
In your S3 bucket, click on Upload.
Drag and drop your website files or use the file selector to choose them.
Click on Upload.

**Step 3: Configure S3 Bucket for Static Website Hosting**

In your S3 bucket, go to the Properties tab.
Scroll down to Static website hosting.
Select Enable.
For Index document, enter index.html (or the main file of your website).
For Error document, enter error.html (or leave it blank if you don't have one).
Click Save changes.

**Step 4: Set Permissions for the S3 Bucket**

Go to the Permissions tab in your S3 bucket.
Click on Bucket Policy.
Add the following policy to allow public access to your files (replace my-static-website with your bucket name):

``json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::my-static-website/*"
        }
    ]
}
``

Click on Save.
Ensure that Block public access is disabled in the Permissions tab to allow public access.

**Step 5: (Optional) Configure CloudFront**

Using CloudFront will help deliver your content more efficiently by caching it in multiple locations globally.
Go to the CloudFront service in the AWS Management Console.
Click on Create Distribution.
Under Web, click Get Started.
Configure the following settings:
Origin Domain Name: Choose your S3 bucket from the dropdown list.
Viewer Protocol Policy: Redirect HTTP to HTTPS.
Cache Behavior Settings: Set as per your requirements.
Click Create Distribution.
It may take a few minutes to deploy. Once it's ready, you'll get a CloudFront URL.

**Step 6: (Optional) Set Up a Custom Domain with Route 53**

If you have a domain name, go to the Route 53 service.
Click on Hosted zones and then Create Hosted Zone.
Domain Name: Enter your domain (e.g., example.com).
Type: Choose Public Hosted Zone.
Create a record set:
Record name: Leave it blank for root domain.
Type: Choose A - IPv4 address.
Alias: Yes.
Alias Target: Select your CloudFront distribution or S3 bucket.
Click on Create.

**Step 7: Access Your Website**

If using S3 directly, your website URL will be in the format:

``vbnet
http://my-static-website.s3-website-us-east-1.amazonaws.com
``

If using CloudFront, access your website using the CloudFront URL.
If you set up Route 53, you can access your website using your custom domain.
Example Static Website Code
Here’s a simple example of static website files:

``html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Static Website</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Welcome to My Static Website</h1>
    </header>
    <main>
        <p>This is a simple static website hosted on AWS S3.</p>
    </main>
    <footer>
        <p>&copy; 2024 My Static Website</p>
    </footer>
</body>
</html>
``

``css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 20px;
}

header {
    background: #333;
    color: #fff;
    padding: 10px 0;
    text-align: center;
}

main {
    margin: 20px 0;
    padding: 20px;
    background: #fff;
    border-radius: 5px;
}

footer {
    text-align: center;
    margin-top: 20px;
}
``

**Conclusion**

You now have a static website hosted on AWS using S3. This setup provides a robust solution for serving static content efficiently. You can further enhance the project by using CloudFront for content delivery and Route 53 for domain management. Let me know if you have any questions or need further assistance!
