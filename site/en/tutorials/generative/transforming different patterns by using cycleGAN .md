literature view 

1.Cross-Modality Image Synthesis from Unpaired Data Using CycleGAN

(https://link.springer.com/chapter/10.1007/978-3-030-00536-8_4)

利用梯度一致性损失扩展 cycleGAN 提高边界精度 

2.Attribute-Guided Face Generation Using Conditional CycleGAN

(https://openaccess.thecvf.com/content_ECCV_2018/html/Yongyi_Lu_Attribute-Guided_Face_Generation_ECCV_2018_paper.html)

属性为引导的图片定向生成

3.Generative Adversarial Networks for Image-to-Image Translation on Multi-Contrast MR Images - A Comparison of CycleGAN and UNIT

(https://arxiv.org/abs/1806.07777)

cycleGAN和UNIT的对比分析，对生成器的深入研究

4.Generating Handwritten Chinese Characters Using CycleGAN

(https://ieeexplore.ieee.org/abstract/document/8354132)

手写汉字的生成

5.Supervised learning with cyclegan for low-dose FDG PET image denoising

(https://www.sciencedirect.com/science/article/pii/S1361841520301341)

cycleWGAN

6.Identity-aware CycleGAN for face photo-sketch synthesis and recognition

(https://www.sciencedirect.com/science/article/pii/S0031320320300558)

考虑识别目的的对应图像生成

## 2021.12.4实验日志

### 1.colab的防止断连的js（实验中）

console端输入如下代码：

```
function getElementByXpath(path) {
       return document.evaluate(path, document, null, 
       XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue;
  }
 
function reconnect(){
	  console.log('working')
	  getElementByXpath("//div[@id='top-toolbar']/colab-connect-button").shadowRoot.querySelector('#connect').click()
}
var a = setInterval(reconnect, 1*60*1000);
function stop(){
	 clearInterval(a)
}
function start(){
	 a = setInterval(reconnect, 1*60*1000);
}
```

console端出现working表示成功。

### 2.原始代码修改

###### 已经保存为 cyclegan （horse2orange）.ipynb

实验目标：观测horse数据集和orange进行混合后的生成结果

代码修改：添加了apple2orange的下载代码，需要手动将数据集混合，将horse2zebra的数据集trainA和testA替换掉apple2orange中的相应数据。由于tf使用的是**tfrecord格式**的数据集（二进制方便存储）需要修改**dataset_info.json**文件,将其中的数据集大小信息统一化。

##### **$\color{red}Q1：$**此时进一步分析数据集，发现trainA和trainB的大小并不一致，且不同任务间的数据集大小也相差较为明显（主要集中在test集上），以horse2orange为例，testA（horse）有120张，但是testB（orange）有250+张。是否影响实验效果（存疑）

