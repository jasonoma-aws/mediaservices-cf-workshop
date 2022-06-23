# mediastreaming-cloudfront-workshop
[BETA] Augmented instructions for the AWS Media Filestreaming Workshop

Follow instructions from this lab:
https://catalog.us-east-1.prod.workshops.aws/workshops/cb172534-d59d-41d1-a9b3-371039593c63/en-US/000introduction

Pause after the Create IAM Role Step. Then follow these instructions:

**CloudFront Setup**
1. Head to CloudFront AWS Console: https://us-east-1.console.aws.amazon.com/cloudfront/v3/home?region=us-east-1#/distributions
2. Create Distribution
3. Origin Domain: Select the S3 Bucket
4. S3 bucket access - Yes use OAI
5. Yes update the bucket policy
4. Origin Path = Leave Blank
5. Enter Name for Origin: Auto-populate with S3 Bucket
6. Add custom headers - Skip this step
7. Enable origin shield - Yes - Region: US-East-1 (for demonstration purposes only)
8. Additional settings: Leave all as default
9. Click Create Distribution
10. While this is creating (~ 10 min) click on the Origin. 
11. Navigate to Error Pages. 
12. Click "Create Custom Error response: 
13. We will create 2 seperate error respones for 403 and 404 errors. Set TTL to 1 second. 
14. Customer error response = no
15. Create custom error response, repeate for second errror (404)

![CFBehaviorExample1](https://user-images.githubusercontent.com/95241370/175065692-b30a0602-0f31-4e57-a0a0-13605685e0d2.png)

Reference: 
[https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/live-streaming.html](https://d1.awsstatic.com/whitepapers/amazon-cloudfront-for-media.pdf)
    
  **Return to the Main Lab for Transcoding Section, but return here for "Playback" Section**
  
  1. Navigate to MediaConvert job
  2. Click on Job ID
  3. Scroll down to Ouputs
  4. Click on the blue Apple HLS - [Media Convert Job] link
  5. Inside the S3 folder you will see m3u8 and TS files. TS = 6 second MPEG Transport Stream segments with AVC/H264 video, the m3u8 files are the parent and child manifests
6. Optional: download the .TS (video/audio) and M3U8 to view locally. TS may require VLC player. M3U8 any plain text editor can view. 
7. Click on VANLIFE.m3u8
8. Copy the S3 URI: s3://[BUCKET]/assets/VANLIFE/HLS/VANLIFE.m3u8
9. Pzste into a notepad
10. Head to CloudFront Console: https://us-east-1.console.aws.amazon.com/cloudfront/v3/home?region=us-east-1#/distributions
11. Copy the Domain name to the same notepad: Ex. d1hp69r8hc134x.cloudfront.net
12. Copy the end path of the S3 URI /assets/VANLIFE/HLS/VANLIFE.m3u8 onto the end of the CloudFront URL. Ex. https://d1hp69r8hc134x.cloudfront.net/assets/VANLIFE/HLS/VANLIFE.m3u8
13. In a browser, navigate to JW Player's Stream Tester: https://developer-tools.jwplayer.com/stream-tester
14. Paste in the concatenated URL from Step 12 insto the "HLS Stream Url" 
15. Select Test Stream
16. You should see a 2:01 video of a van playing in your window. 
17. If any errors, please check that the file paths, CLoudFront Origin Access Identity, and cache key and origin request settings are configured correctly. s
