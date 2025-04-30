# Static-Website-Hosting-

##  **Project Title**: Static Website Hosting on AWS using S3


## **Objective**
Host a static website (HTML, CSS, JS files) using **Amazon S3**, optionally with a **custom domain**, **HTTPS**, and **CloudFront CDN** for performance and security.



## **Step-by-Step Implementation**

---

###  **Step 1: Prepare Your Website Files**

- Create or gather your static files:
  - `index.html` (homepage)
  - `style.css`, `script.js`, `images/`, etc.


###  **Step 2: Create an S3 Bucket**

1. Go to the **AWS S3 Console**.
2. Click **Create bucket**.
3. **Name the bucket exactly like your domain name** (e.g., `example.com` or `www.example.com`).
4. Select a region.
5. **Uncheck** "Block all public access".
6. Acknowledge the warning and create the bucket.



###  **Step 3: Upload Your Website Files**

1. Open your bucket.
2. Click **Upload**.
3. Add all website files and folders.
4. Click **Upload** to complete.



### **Step 4: Enable Static Website Hosting**

1. In your bucket, go to the **Properties** tab.
2. Scroll to **Static website hosting**.
3. Choose **Enable**.
4. Enter:
   - **Index document**: `index.html`
   - (Optional) **Error document**: `error.html`
5. Copy the **Endpoint URL** provided — this is your website URL for now.



###  **Step 5: Set Bucket Policy to Allow Public Access**

1. Go to the **Permissions** tab.
2. Scroll to **Bucket policy**.
3. Add the following policy (replace `your-bucket-name`):

#
** 
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadForStaticWebsite",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
**
#


4. Save the policy.



### **At this point, your static website is live** at the S3 endpoint URL like:


http://your-bucket-name.s3-website-us-east-1.amazonaws.com




## Set Up a Custom Domain (e.g., `www.example.com`)



### 🔹 Step 6: Use Route 53 (or other DNS provider)

1. Buy a domain or use an existing one.
2. In **Route 53**, create a **hosted zone** if needed.
3. Create an **A Record (alias)** pointing to your S3 website endpoint.

For example:
- Name: `www.example.com`
- Type: A
- Alias: Yes
- Alias Target: S3 static website endpoint



##Enable HTTPS and CDN with CloudFront


### 🔹 Step 7: Set Up CloudFront Distribution

1. Go to **CloudFront** > **Create Distribution**.
2. Origin Domain: Your S3 bucket website endpoint (not the S3 REST API).
3. Viewer Protocol Policy: **Redirect HTTP to HTTPS**
4. Enable Caching, Compression.
5. Add Alternate Domain (CNAME): `www.example.com`
6. Choose or create an **SSL certificate** using **AWS Certificate Manager (ACM)**.



###  Step 8: Update DNS to Point to CloudFront

- In **Route 53**, update your `A` record to point to the CloudFront distribution (alias).




-


