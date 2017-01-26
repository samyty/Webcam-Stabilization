# Video Input
vid = VideoWriter('videoname.avi');
open(vid);
clear cam
cam = webcam;
for i = 1:100 
img = snapshot(cam);
writeVideo(vid, img);
close(vid);
clear cam

# Facial Detection
faceDetector = vision.CascadeObjectDetector();

%Detect face   
bbox = step(faceDetector, img);
if size(bbox,1) == 0
    	continue     
end

# Facial Detection bbox
img = insertShape(img, ‘Square’, bbox);
title('Detected face');

if i == 1
    X = bbox(1);
    Y = bbox(2);
end

img = stabilize(X, Y, img, bbox(3));
imshow(img);
end

# Stabilization
function [ steady ] = stabilize( bb1x ,bb1y, im, length)

   xDiff = ((640-length)/2) - bb1x;
   yDiff = ((480-length)/2) - bb1y;
   xDiff = round(xDiff); % Integer
   yDiff = round(yDiff);
   steady = circshift(im, [yDiff, xDiff]);
   
end
