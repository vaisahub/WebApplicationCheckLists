**Web Application Check Lists**

1. **Image Optimisation**

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

**
import sharp from 'sharp';
import fs from 'fs';
import path from 'path';

export default async function handler(req, res) {
  try {
    const { imagePath } = req.query;

    // Ensure the image exists
    const imageFullPath = path.join(process.cwd(), 'public', imagePath);

    if (!fs.existsSync(imageFullPath)) {
      return res.status(404).json({ error: 'Image not found' });
    }

    // Read and convert the image
    const imageBuffer = fs.readFileSync(imageFullPath);

    const webpImageBuffer = await sharp(imageBuffer)
      .webp() // Convert to WebP
      .toBuffer();

    // Set appropriate headers for WebP image
    res.setHeader('Content-Type', 'image/webp');
    res.setHeader('Cache-Control', 'public, max-age=31536000, immutable');

    res.status(200).send(webpImageBuffer);
  } catch (error) {
    console.error('Error converting image: ', error);
    res.status(500).json({ error: 'Failed to convert image' });
  }
}
**
