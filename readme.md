## 一、项目背景介绍
近年来由于校园火灾案例层出不穷，校园宿舍等人员密集型建筑火灾防控已成为高校园区安全防控的重点任务之一。但建筑之间复杂的地理环境致使常规灭火措施无法实现范围全覆盖。 利用计算机视觉的方法对起火点进行定位，使用无人机锁定起火点完成灭火 尽管无人机在消防行业应用方向已有应用，但目前市面上大部分消防无人机呈现出自动化程度低，作业效率低等特点。据此，本项目致力于利用多功能消防无人机建立一套无死角、高效率、自动识别，查打一体的消防无人机系统。为“安全校园”保驾护航。

## 二、数据介绍
火灾检测数据集，数据格式为VOC

![](https://ai-studio-static-online.cdn.bcebos.com/9459bb6ec614411e9a2515e520e725e0e0be52f50a5f46cea8e0d0fd46f83e5a)


## 三、模型介绍
MobileNet系列是谷歌为适配移动终端提供了一系列模型，包含图像分类：mobileNet v1，mobileNet v2，mobileNet v3，目标检测SSD mobileNet等。

## 四、模型训练

```python
#解压数据集
!tar -zxvf data/data117717/fire_detection.tar
```


```python
#解压PaddleDetection
!unzip PaddleDetection.zip
```


```python
#进入PaddleDetection目录
%cd /home/aistudio/PaddleDetection
```


```python
!pip install --upgrade pip
```


```python
#安装Python依赖库
!pip install -r requirements.txt
```


```python
#配置python环境变量
%env PYTHONPATH=/home/aistudio/PaddleDetection
```


```python
#测试项目环境
!export PYTHONPATH=`pwd`:$PYTHONPATH
!python ppdet/modeling/tests/test_architectures.py
```


```python
#开始训练
!cd /home/aistudio/PaddleDetection
```


```python
!python -u tools/train.py -c configs/ssd/ssd_mobilenet_v1_voc.yml #--use_tb=True --eval
```


```python
#!unzip fireData.zip -d data/firedata
```


```python
#测试，查看模型效果
%cd /home/aistudio/PaddleDetection/
!python tools/infer.py -c configs/ssd/ssd_mobilenet_v1_voc.yml --infer_img=/home/aistudio/2001.jpg
#infer_img输入需要预测图片的路径，看一下效果
```


```python
#转换模型
```


```python
#转化为预测模型
!python -u tools/export_model.py -c configs/ssd/ssd_mobilenet_v1_voc.yml --output_dir=./inference_model_final
```


```python
%cd /home/aistudio/
#复制opt文件到相应目录下
!cp opt /home/aistudio/PaddleDetection/inference_model_final/ssd_mobilenet_v1_voc
#进入预测模型文件夹
%cd /home/aistudio/PaddleDetection/inference_model_final/ssd_mobilenet_v1_voc
#下载opt文件
#!wget https://github.com/PaddlePaddle/Paddle-Lite/releases/download/v2.3.0/opt
#给opt加上可执行权限
!chmod +x opt
#使用opt进行模型转化,将__model__和__params__转化为model.nb
!./opt --model_file=__model__ --param_file=__params__ --optimize_out_type=naive_buffer   --optimize_out=./model
!ls
```


## 五、模型评估

https://www.bilibili.com/video/BV1bg411N7eq?share_source=copy_web

![](https://ai-studio-static-online.cdn.bcebos.com/93be25b91a214643b95bff01bc686ca7cc93bb9755454366b1cc8554000b64a9)
![](https://ai-studio-static-online.cdn.bcebos.com/167549a7a326434f839f521cb4bfee6fd41c016e260948e8bbda9691058a22a4)
![](https://ai-studio-static-online.cdn.bcebos.com/7a5a16ba3bd048649a6630df244334179d5a0686310542e6b8431e1d45a551d6)


## 六、个人总结
**姓名：王浩楠**

**华北水利水电大学**

**本科英语专业，目前在读大三**

是个喜欢人工智能和无人机的萌新小白，希望能与大家一起交流学习，欢迎加入华北水利水电大学飞桨领航团
![](https://ai-studio-static-online.cdn.bcebos.com/3edd23815c344203a9954ee6e8569d72a2a37efdf2ec464cb34845fa946393bb)




## 提交链接
aistudio链接：https://aistudio.baidu.com/aistudio/personalcenter/thirdview/938071

github链接：

gitee链接：
