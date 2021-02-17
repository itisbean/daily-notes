# ffmpeg

- 使用m3u8文件下载视频
  
```bash
ffmpeg \
-headers "User-Agent: "$'\r\n' \
-i 'https://domain/index.m3u8' \
-c copy 'output.mp4' \
-v trace
```

- 转换视频
  
```bash
ffmpeg \
-i input.mp4 \
-c:v libx264 -crf 18 \
-c:a copy output.mp4
```
