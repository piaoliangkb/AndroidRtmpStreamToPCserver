#### 1. windwos端下载直接编译好的nginx-rtmp-server

> 作用：将本机作为server端接收rtmp流

[https://github.com/illuspas/nginx-rtmp-win32](https://github.com/illuspas/nginx-rtmp-win32)

使用方法网页中有，双击nginx.exe就会自动启动；关闭的时候可以在进程中找到两个nginx，直接杀死或者直接双击stop.bat。

进入localhost:8080可以看到自己的连接情况。

#### 2.下载ffmpeg

> 作用：从rtmp流中截取每一帧的图像保存下来

下载地址： [https://ffmpeg.zeranoe.com/builds/](https://ffmpeg.zeranoe.com/builds/)
最右边的link选择static版，download build

下载完成解压之后，将解压之后文件夹中的bin目录的路径添加到环境变量中的系统变量"path"中

![](https://upload-images.jianshu.io/upload_images/11146099-38223dce23d859a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加完之后打开控制台输入 ffmpeg -version 检查是否添加成功。

#### 3.安装yasea 手机端推流app

[https://github.com/begeekmyfriend/yasea](https://github.com/begeekmyfriend/yasea)

在左上方网址处输入rtmp://localhost/live/stream
localhost 改为内网pc端的的ip

左下角publish是推流，switch是改变摄像头方向，record是在手机上录制成mp4，最后一个是硬编码和软编码。

-------------------------------------------------------------
#### 使用方法：

1. 电脑端先开启nginxserver
2. 手机输入rtmp地址进行推流，使用电脑的浏览器进入localhost:8080的主界面，左上角点击play可以播放推流的视频。
3. 打开命令行，切换到保存图片的文件夹，输入以下命令保存图片


    ffmpeg -i rtmp://localhost/live/stream -r 30 -f image2 image-%d.jpeg 
    
其中 -r 后的参数表示帧率，就是从视频中每秒保存图片的数量； -f 为指定保存图片的格式； image-%d.jpeg 为保存图片的名称。



------------------------------------------------------------------
FFMPEG常用命令

	1. ffmpeg -i inputfile.avi -r 1 -f image2 image-%05d.jpeg 
    -r 指定抽取的帧率，即从视频中每秒钟抽取图片的数量。1代表每秒抽取一帧。 
    -f 指定保存图片使用的格式，可忽略。 
    image-%05d.jpeg，指定文件的输出名字。
    
    2. ffmpeg -i inputfile.avi -r 1 -s 4cif -f image2 image-%05d.jpeg 
    4cif 代表帧的尺寸为705x576.其他可用尺寸如下。
    
    3. ffmpeg -i inputfile.avi -r 1 -t 4 -f image2 image-%05d.jpeg 
    -t 代表持续时间，单位为秒。
    
    4. ffmpeg -i inputfile.avi -r 1 -ss 01:30:14 -f image2 image-%05d.jpeg 
    -ss 指定起始时间
    
    5.ffmpeg -i inputfile.avi -r 1 -ss 01:30:14 -vframes 120 4cif -f image2 image-%05d.jpeg 
    -vframes 指定抽取的帧数
    
    6. ffmpeg -i rtmp://server/live/streamName -c copy dump.flv 
    将直播媒体保存至本地文件


    






