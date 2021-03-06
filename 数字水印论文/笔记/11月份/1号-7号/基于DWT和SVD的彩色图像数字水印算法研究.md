# 基于 DWT 和 SVD 的彩色图像数字水印算法研究

## 作者：梁欣 发表时间：2019年

## 期刊：计算机与数字工程 第8期第47卷

## 主要内容：

* 该文与本周阅读的上一篇论文中，所采用的方法类似，他们的差异只是在处理的图像上不同。
* 该文选取的原始图像和水印均为RGB彩色图像，先是通过对颜色模型的转换，再对其进行水印的嵌入和提取。

## 水印的嵌入和提取

### 1.嵌入算法

* 先将原始图像和水印图像分别从RGB颜色模型转换为YCbCr颜色模型
  * YCbCr颜色模型被称为YUV模型，是视频图像和数字图像中常见的色彩模型。在YCbCr模型中，Y代表亮度，Cb和Cr共同描述图像的色调（色差），其中Cb、Cr分别为蓝色分量和红色分量相对于参考值的坐标
* 对原始图像的Y分量进行二级离散小波变换，得到七个子带，然后该文选择了其中三个子带进行水印嵌入
* 对上述选出的三个子带进行奇异值分解，得到六个正交矩阵U和V，以及三个对角矩阵S
* 将水印图像的Y，Cb，Cr分量分别采用加性水印公式WM = S + a * W（a是嵌入水印强度。针对不同的子带采用不同的系数）叠加到上步得到的三个对角矩阵S上，再对新产生的WM进行奇异值分解。
* 将奇异值分解得到的值进行相乘，得到处理后嵌入水印的小波系数。对修改的后的小波系数进行小波反变换后得到Y分量，再结合原始图像的色度信息，即Cb分量和Cr分量转换到RGB颜色模型就可以得到含水印图像

### 2.提取算法

* 对含水印的图像进行颜色模型转换，由RGB转换为YCbCr，再利用DWT对转换后的含水印图像的Y分量进行二级小波变换，得到七个子带
* 对嵌入时选取的三个子带进行奇异值分解，利用公式分别求出水印的Y、Cb、Cr分量
* 根据得到的Y、Cb、Cr分量转换到RGB色彩空间即得到原水印彩色图像

## 总结

* 该文提出的方法经实验证明算法对常见攻击具有较强的鲁棒性。对 水印对角线方向失真现象也作了修改，在一定程度上改善了水印视觉效果。提高了水印的安全性和不可见性
* 与上一篇论文对比，两篇论文所采用的方法大同小异，唯一的区别就是彩色图像和灰度图像之间的处理问题，对彩色图像而言，水印的提取和嵌入较麻烦一些，需要对不同的分量做处理，不像灰度图像，做处理的只有图像本身而已。总的来看，这类算法数学背景清晰，有较强的实用性。

