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
