# tensorflow.cifar10
The examples of image recognition with the dataset CIFAR10 via tensorflow.

CIFAR-10数据集是机器学习中的一个通用的用于图像识别的基础数据集，官网链接为：[The CIFAR-10 dataset](http://www.cs.toronto.edu/~kriz/cifar.html)

![cifar10](http://img.blog.csdn.net/20160226153743929)

下载使用的版本是：

![version](http://img.blog.csdn.net/20160226160254186)

将其解压后（代码中包含自动解压代码），内容为：

 ![cifar10 data](http://img.blog.csdn.net/20160226160343415)

![cifar10 data2](http://img.blog.csdn.net/20160226160405884)

测试代码公布在GitHub：[yhlleo](https://github.com/yhlleo/tensorflow.cifar10)

该部分的代码，介绍了如何使用TensorFlow在CPU和GPU上训练和评估卷积神经网络（convolutional neural network, CNN）。

更加详细地介绍说明，请浏览网页：[Convolutional Neural Networks](http://tensorflow.org/tutorials/deep_cnn/) 

中文网站极客学院也有该部分的汉译版：[卷积神经网络](http://wiki.jikexueyuan.com/project/tensorflow-zh/tutorials/deep_cnn.html)

代码源自tensorflow官网：[tensorflow/models/image/cifar10](https://tensorflow.googlesource.com/tensorflow/+/master/tensorflow/models/image/cifar10)

GitHub公布代码，主要进行了以下修正：

 - **`cifar10.py`**
 
```python
#indices = tf.reshape(tf.range(FLAGS.batch_size), [FLAGS.batch_size, 1])
indices = tf.reshape(range(FLAGS.batch_size), [FLAGS.batch_size, 1])
```

此处，源码编译时会出现以下错误：

```python
  ...
  File ".../cifar10.py", line 271, in loss
    indices = tf.reshape(tf.range(FLAGS.batch_size), [FLAGS.batch_size, 1])
TypeError: range() takes at least 2 arguments (1 given)
```

 - **`cifar10_input_test.py`**

```python
#self.assertEqual("%s:%d" % (filename, i), tf.compat.as_text(key))

import compat as cp
...

self.assertEqual("%s:%d" % (filename, i), cp.as_text(key))
```

不然的话，我测试的时候就会出现这的错误：

```python
AttributeError: 'module' object has no attribute 'compat'
```

