JVC introductory video
======================
I'm really into meta thing.

Thus, the video introduction to JVC was created with JVC.

# Input Assets
The files in `assets` are what I started with:

  * `jvc-slides.odp` is a presentation created in LibreOffice
  * `jvc-slidesNN.png` are PNG images of each slide, exported manually from LibreOffice
  * `iphone_NN*.mp4` are videos I took with my iPhone
     * I used `jrmtrack infile.MOV assets/iphone_NN_desc.mp4 other` to remove data tracks
       and repackage from .mov to .mp4
  * `build_screencast.mp4` is a portion of a screencast I created using [OBS Studio](https://obsproject.com/)
     * I used `jtrim infile.mkv assets/build_screencast.mp4` to crop the
       original screencast, which was over 250MB
  * Some video files are re-created from sub-parts (`.1`, `.2`, etc.) because
    GitHub does not allow files larger than 100MB

# Build
To create the video, run:
```shell script
./make-jvc-vid
```
This will take a long time, especially if it has to build jvc first.

Also, you'll need to the `HEAD` version of ffmpeg.
The `duration` option for `anullsrc` is not yet supported in latest official ffmpeg release,
this is required for `overlay` and `merge-audio` operations.

You can read through the `make-jvc-vid` script to see how the video is put together.

The basic steps are:

 * For each iphone video, crop out the footage of "I'm touching the screen to start/stop recording"
 * For each slide image, use the ken-burns effect with no zoom or pan to create a video of a duration
   that is about 1 to 1.5 seconds longer than the corresponding iphone video.
 * For each slide video, overlay the corresponding iphone video, creating an "overlay" output video.
 * Prepare and overlay the "clone and build" screencast video.
 * Lastly, concatenate all overlay output videos to produce the final output video.

# Watch the video!
Assuming you have [VLC](https://www.videolan.org/vlc/) installed, run:
```shell script
vlc output/jvc-video.mp4
```
