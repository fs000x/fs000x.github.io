# m3u8/ts视频下载

转自: [网页视频流m3u8/ts视频下载](https://segmentfault.com/a/1190000018170951)


### m3u8/ts 是什么

现在很多视频网站播放流视频，都不是采用mp4／flv文件直接播放，而是采用m3u8/ts这种方式播放。

简单说就是，网站后台把视频切片成成百上千个xx.ts文件，一般10秒一个，每个都几百kb很小。然后通过xx.m3u8播放列表把这些文件连接起来。

通过Chrome DevTool的Network栏，我们可以清楚的看到加载过程：



我们直接点击这个playlist.m3u8播放列表文件，在旁边的preview栏中查看内容，可以看到：

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-ALLOW-CACHE:YES
#EXT-X-TARGETDURATION:11
#EXTINF:5.250000,
out000.ts
#EXTINF:9.500000,
out001.ts
#EXTINF:8.375000,
out002.ts
#EXTINF:5.375000,
out003.ts
#EXTINF:9.000000,
out004.ts
...........
```

### 那我们怎么下载呢？

下载视频所有的ts切片文件一般的思路是，想办法把所有的ts切片文件下载下来，然后合成一个完整的视频。

然而，配合xx.m3u8播放列表文件，我们可以直接用ffmpeg在线下载播放列表中所有的视频，然后直接用ffmpeg合并为一个视频。

我们就直接执行这一句命令即可：
```sh
$ ffmpeg -i <m3u8-path> -c copy OUTPUT.mp4
$ ffmpeg -i <m3u8-path> -vcodec copy -acodec copy OUTPUT.mp4

# 例如：
ffmpeg -i https://cdn-6.haku99.com/hls/2019/06/06/K9MuzqsC/playlist.m3u8 -c copy  OUTPUT.mp4
```
