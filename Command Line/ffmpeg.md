
## Snippets
牺牲画质，快速压缩
```zsh
ffmpeg -i input.mov -vcodec libx264 -crf 24 -preset veryfast -vf scale=1920:1080 output.mp4
```