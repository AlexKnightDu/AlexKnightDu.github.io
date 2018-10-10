---
title: ffmpeg入门的一点尝试
date: 2018-10-08 20:35:03
tags: [Tools]
---
慢慢地，也开始平淡于现实了啊……     

FFmpeg 即 Fast Forward Moving Pictures Experts Group，可以说是一个非常强大的音视频编解码框架了，主要包含以下模块：

- AVFormat：格式封装模块
- AVCodec：编解码模块
- AVFilter：滤镜模块
- swscale：视频图像转换计算模块，图像缩放和像素格式转换
- swresample：音频转换计算模块，允许操作音频采样、音频通道布局转换和布局调整等

相应的也会有编译好的工具：

- ffmpeg
- ffplay
- ffprobe：分析器

一些基本概念提一下：

- 封装格式：把视频和音频放到一个文件中，所以也可以认为是文件格式
- 视频格式：视频编码格式
- 视频码率：期望的压缩后视频的大小，用平均每秒多少bit来衡量一个视频大小

FFmpeg的功能主要分为媒体格式转封装、音视频编解码、传输协议转换、支持Filter处理等。

### FFmpeg 转封装
首先介绍一下几个格式：

- MP4：
	- MP4 文件有许多个Box与FullBox组成
	- 每个Box由Header和Data两部分组成
	- FullBox是Box的扩展，其在Box的基础上，在Header中增加8位version标志和24位的flags标志
	- Header包含了整个Box的长度的大小和类型
	- Data位Box的实际数据，可以是纯数据，也可以是更多的子Box
	- 当一个Box中的Data是一系列的子Box时，这个Box又可以称为Container Box
- FLV：FLV分为两部分，一部分为FLV文件头，一部分为FLV文件内容  

。。。未完待续

### FFmpeg 转码
### FFmpeg 流媒体
### FFmpeg 滤镜

读着读着越来越觉得，好像要做的事重点不是FFmpeg能解决的QAQ