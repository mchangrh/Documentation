# file media files not encoded with specific codec (with ffprobe)

```
$ find -name \*.avi -o -name \*.mp4 \
    -exec ffprobe -v quiet -show_streams -show_format -of json {} \; |
  jq -c '.format.filename as $path |
         .streams[]? |
         select(.codec_type=="video" and .codec_name!="h264") |
         {codec: .codec_name, path: $path}'
 ```
 source: [AskUbuntu](https://askubuntu.com/questions/781408/how-can-i-find-media-files-not-encoded-with-a-specific-codec)

  # ChromeOS Recovery Images
 ```https://dl.google.com/dl/edgedl/chromeos/recovery/recovery.conf```

 [source](https://www.reddit.com/r/chromeos/comments/5c5ggd/manually_download_chrome_os_images_for_recovery/)

  # Kindle Software Updates

[Amazon](https://www.amazon.com/gp/help/customer/display.html/ref=hp_bc_nav?ie=UTF8&nodeId=200529680)