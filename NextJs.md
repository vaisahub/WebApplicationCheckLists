# Web Application Check Lists

### Image Optimisations 

# Use Case Scenarios  

# Public Profiles / Static Images:
    If performance is a priority,
    the Next.js Image component will generally be faster and more bandwidth-efficient for public, 
    frequently accessed profile images.
# Authenticated Images or Private S3 Access: 
    If your images require authentication or are only visible to specific users,
    StorageImage might be simpler because it manages signed URLs and access controls directly with Amplify’s storage.

# Most efficient way is to convert images and store them as 'webp' then if auth is required use 'StorageImage'
