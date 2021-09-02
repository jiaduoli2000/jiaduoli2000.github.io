---
title: 用python将视频生成帧图
author: 阿狸的Blog
date: '2021-08-01'
slug: python-video to img
categories:
  - 效率工具
tags:
  - python
---
# 用python将视频生成帧图

## 安装`opencv-python`

首先，打开`Anaconda Prompt(Anaconda3)`, 

![20210801205916](https://gitee.com/alingyisheng/tupian/raw/master/img/20210801205916.png)

输入命令：`pip install opencv-python`，

![20210801210229](https://gitee.com/alingyisheng/tupian/raw/master/img/20210801210229.png)

安装成功之后，关闭。

## 打开pycharm
如果在打开`pycharm`过程中，要求填入激活码，可打开[**Pycharm激活码**在线生成地址](www.vrg123.com)。

打开`pycharm`后，新建项目，然后新建`.py`文件。粘贴以下内容，然后运行即可。注意：
1. 视频存储位置：C://Users/jiadu/Desktop/video/mm.mp4
2. 图片存储位置：C://Users/jiadu/Desktop/video


```
import os  
import cv2  
  
"""  
功能：将视频转成图片(提取视频的每一帧图片)  
 1.能够设置多少帧提取一帧图片  
 2.可以设置输出图片的大小及灰度图  
 3.手动设置输出图片的命名格式  
"""  
def ExtractVideoFrame(video_input,output_path):  
 # 输出文件夹不存在，则创建输出文件夹  
 if not os.path.exists(output_path):  
 os.mkdir(output_path)  
  
 times = 0 # 用来记录帧  
 frame_frequency = 10 # 提取视频的频率，每frameFrequency帧提取一张图片，提取完整视频帧设置为1  
 count = 0 # 计数用，分割的图片按照count来命名  
 cap = cv2.VideoCapture(video_input) # 读取视频文件  
  
 print('开始提取', video_input, '视频的图片')  
 while True:  
 times += 1  
 res, image = cap.read() # 读出图片。res表示是否读取到图片，image表示读取到的每一帧图片  
 if not res:  
 print('图片提取结束')  
 break  
 if times % frame_frequency == 0:  
 # picture_gray = CV2.cvtColor(image, CV2.COLOR_BGR2GRAY)  # 将图片转成灰度图  
 # image_resize = CV2.resize(image, (368, 640))            # 修改图片的大小  
 img_name = str(count).zfill(6)+'.jpg'  
 cv2.imwrite(output_path + os.sep + img_name, image)  
 count += 1  
  
 print(output_path + os.sep + img_name) # 输出提示  
 cap.release()  
  
"""  
功能：获取视频的指定帧并进行显示  
"""  
def ShowSpecialFrame(file_path,frame_index):  
 cap = cv2.VideoCapture(file_path) # 读取视频文件  
 cap.set(cv2.CAP_PROP_POS_FRAMES, float(frame_index))  
 if cap.isOpened(): # 判断是否正常打开  
 rval, frame = cap.read()  
 cv2.imshow("image:"+frame_index,frame)  
 cv2.waitKey()  
 cap.release()  
  
"""  
功能：切割视频的指定帧。比如切割视频从100帧到第200帧的图片  
 1.能够设置多少帧提取一帧图片  
 2.可以设置输出图片的大小及灰度图  
 3.手动设置输出图片的命名格式  
"""  
def ExtractVideoBySpecialFrame(video_input,output_path,start_frame_index,end_frame_index = -1):  
 # 输出文件夹不存在，则创建输出文件夹  
 if not os.path.exists(output_path):  
 os.mkdir(output_path)  
  
 cap = cv2.VideoCapture(video_input) # 读取视频文件  
 cap.set(cv2.CAP_PROP_POS_FRAMES, float(start_frame_index)) # 从指定帧开始读取文件  
 times = 0 # 用来记录帧  
 frame_frequency = 10 # 提取视频的频率，每frameFrequency帧提取一张图片，提取完整视频帧设置为1  
 count = 0 # 计数用，分割的图片按照count来命名  
  
 # 未给定结束帧就从start_frame_index帧切割到最后一帧  
 if end_frame_index == -1:  
 print('开始提取', video_input, '视频从第',start_frame_index,'帧到最后一帧的图片！！')  
 while True:  
 times += 1  
 res, image = cap.read() # 读出图片  
 if not res:  
 print('图片提取结束！！')  
 break  
 if times % frame_frequency == 0:  
 # picture_gray = CV2.cvtColor(image, CV2.COLOR_BGR2GRAY)  # 将图片转成灰度图  
 # image_resize = CV2.resize(image, (368, 640))            # 修改图片的大小  
 img_name = str(count).zfill(6) + '.jpg'  
 cv2.imwrite(output_path + os.sep + img_name, image)  
 count += 1  
 print(output_path + os.sep + img_name) # 输出提示  
 else:  
 print('开始提取', video_input, '视频从第', start_frame_index, '帧到第',end_frame_index,'帧的图片！！')  
 k = end_frame_index - start_frame_index + 1  
 while(k >= 0):  
 times += 1  
 k -= 1  
 res, image = cap.read() # 读出图片  
 if not res:  
 print('图片提取结束！！')  
 break  
 if times % frame_frequency == 0:  
 # picture_gray = CV2.cvtColor(image, CV2.COLOR_BGR2GRAY)  # 将图片转成灰度图  
 # image_resize = CV2.resize(image, (368, 640))            # 修改图片的大小  
 img_name = str(count).zfill(6) + '.jpg'  
 cv2.imwrite(output_path + os.sep + img_name, image)  
 count += 1  
 print(output_path + os.sep + img_name) # 输出提示  
 print('图片提取结束！！')  
 cap.release()  
  
  
if __name__ == "__main__":  
 # 视频路径  
 video_input = 'C://Users/jiadu/Desktop/video/mm.mp4'  
 # 图片输出路径  
 output_path = r'C://Users/jiadu/Desktop/video'  
  
 # 提取视频图片  
 ExtractVideoFrame(video_input, output_path)  
  
 # 显示视频第100帧的图片  
 # ShowSpecialFrame(video_input, 1500)  
  
 # 获取视频第100帧到第200帧的图片  
 #ExtractVideoBySpecialFrame(video_input, output_path, 100, 200) 

```
