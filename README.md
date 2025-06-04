# AWS S3 Static Website Lab

AWS static website hosting lab by **Jon Ong**

## 🎯 Lab Objectives

This lab demonstrates how to host a static website using Amazon S3 static website hosting feature, focusing on core AWS S3 concepts and configurations.

## 📚 Key S3 Learnings

### **1. S3 Bucket Configuration**
- **Object Ownership**: Learned difference between ACLs enabled vs disabled
  - ACLs disabled (recommended) = bucket owner owns all objects, uses policies for access control
  - ACLs enabled = allows granular object-level permissions and cross-account ownership
- **Block Public Access**: Must be disabled for static website hosting to allow public read access
- **Bucket Versioning**: Keeps multiple variants of objects, useful for rollbacks but adds storage costs
- **Default Encryption**: SSE-S3 is applied automatically to all new objects
- **Bucket Key**: Cost optimization feature for SSE-KMS encryption (not applicable to SSE-S3)

### **2. Static Website Hosting Setup**
- **Index Document**: Entry point file (index.html) served when accessing root domain
- **Error Document**: Custom 404 page (404.html) shown when requested files don't exist
- **Website Endpoint**: S3 provides a unique URL format: `bucket-name.s3-website-region.amazonaws.com`
- **HTTP Only**: S3 static hosting only supports HTTP (HTTPS requires CloudFront)

### **3. Security & Access Control**
- **Bucket Policy**: JSON policy granting public read access to all objects
  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid": "PublicReadGetObject",
        "Effect": "Allow",
        "Principal": "*",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::bucket-name/*"
      }
    ]
  }
  ```
- **CORS Configuration**: Not needed for simple static websites (only for cross-origin requests)
- **Requester Pays**: Billing model where downloaders pay transfer costs (useful for large datasets)

### **4. Advanced S3 Features**
- **Transfer Acceleration**: Uses edge locations to speed up uploads TO S3
- **CloudFront Integration**: Uses edge locations to speed up downloads FROM S3 (adds HTTPS support)
- **Object Lock**: WORM model preventing deletion/modification (requires versioning)
- **Custom Domains**: Can use Route 53 for custom domain names

### **5. S3 Website Architecture**
- **S3 as Web Server**: Serves static files directly to browsers
- **No Server-Side Processing**: Only serves pre-built HTML, CSS, JS files
- **Scalability**: Automatically handles traffic spikes without configuration
- **Deployment**: Upload files to S3 bucket, instantly available via website endpoint

## 🛠️ Technical Implementation

### **AWS Resources Created:**
- **S3 Bucket**: `mystaticwebsitelab-4jun`
- **Region**: Asia Pacific (Sydney) - ap-southeast-2
- **Website Endpoint**: `http://mystaticwebsitelab-4jun.s3-website-ap-southeast-2.amazonaws.com/`

### **S3 Configuration Applied:**
- ✅ Static website hosting enabled
- ✅ Public read access configured
- ✅ Custom error document setup
- ✅ Bucket policy for public access
- ✅ Default encryption (SSE-S3)

## 💡 Key S3 Insights

1. **Static websites are ideal for S3** - no server-side processing needed
2. **Public access must be carefully configured** - balance accessibility with security
3. **Custom error pages improve user experience** over default S3 errors
4. **Edge locations serve dual purposes** - CloudFront for distribution, Transfer Acceleration for uploads
5. **S3 website hosting vs S3 REST endpoints** - different URL formats and capabilities
6. **Encryption is automatic** - all objects encrypted at rest by default

## 🚀 Future S3 Enhancements

- [ ] Add CloudFront distribution for HTTPS and global CDN
- [ ] Implement custom domain with Route 53
- [ ] Enable S3 access logging for analytics
- [ ] Configure lifecycle policies for cost optimization
- [ ] Set up versioning for content rollback capability
- [ ] Implement Transfer Acceleration for faster uploads

## 📈 S3 Cost Considerations

- **S3 Storage**: ~$0.023 per GB per month (Standard storage class)
- **Data Transfer**: First 1GB free per month, then ~$0.09 per GB
- **Requests**: GET requests are ~$0.0004 per 1,000 requests
- **Static Website**: Extremely cost-effective for low to medium traffic
- **Total Lab Cost**: Estimated under $1 per month for typical usage

## 🔗 AWS S3 Resources

- [AWS S3 Static Website Hosting Documentation](https://docs.aws.amazon.com/s3/)
- [S3 Pricing Calculator](https://aws.amazon.com/s3/pricing/)
- [S3 Best Practices Guide](https://docs.aws.amazon.com/s3/latest/userguide/optimizing-performance.html)

---

**Created by Jon Ong** | AWS S3 Static Website Lab | 2025