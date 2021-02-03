Ubuntu / Debian
```
sudo apt-get install ffmpeg

```

MacOS
```
brew instal ffmpeg
```

I needed to cut the last six seconds off of a video file 

```
ffmpeg -i input_filename.mp4 -ss 6 -i input_filename.mp4 -c copy -map 1:0 -map 0 -shortest -f nut - | ffmpeg -f nut -i - -map 0 -map -0:0 -c copy output_filename.mp4
```
explanation of what it is doing:
-ss 3 is input option of second input.mp4. -map 1:0 -map 0 stdout, but output -map 1:0 is shorten 3 seconds, then output -map 0 is shorten by the last 3 seconds by -shortest. -map -0:0 is deleted from -map 1:0



I tried doing this first, but it only cut the first six seconds of the video instead 
```
ffmpeg -i input_filename.mp4 -ss 6 -c copy output_filename.mp4
```



(I did not try this one)
Here is another option:
Understanding there is not a native from end spec for duration you can detect the videos duration ourselfves and subtract the 6 seconds manually
ffprobe -i input.mp4 -show_entries format=duration -v quiet -of csv="p=0"



bash script here 
```
dur=$(ffprobe -i input.mp4 -show_entries format=duration -v quiet -of csv="p=0")
trim=$((dur - 3))
ffmpeg -t $trim -i input.mp4 output.mp4

```
