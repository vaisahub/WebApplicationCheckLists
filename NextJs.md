**Web Application Check Lists**

**Image Optimisation**

 Use Case Scenarios  

- **Public Profiles / Static Images:**
    If performance is a priority,
    the Next.js Image component will generally be faster and more bandwidth-efficient for public, 
    frequently accessed profile images.
- **Authenticated Images or Private S3 Access:**
    If your images require authentication or are only visible to specific users,
    StorageImage might be simpler because it manages signed URLs and access controls directly with Amplify’s storage.

**Most efficient way is to convert images and store them as 'webp' then if auth is required use 'StorageImage'**

Additional Info

-  CloudFront is a content delivery network (CDN) that caches content at edge locations around the world

- Tools like **Cloudinary, Shark.ai, or ImageKit**
  offer image optimization services that can integrate with your CloudFront distribution.
