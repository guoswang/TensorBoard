使用最基础的识别手写字体的案例,建立一个简单的神经网络，让大家了解如何使用Tensorboard。
## Requirements
- Python
- [Tensorflow](https://github.com/tensorflow/tensorflow)
## Usage
**Step 1.** Download this repository with git or click the [download ZIP ](https://github.com/guoswang/TensorBoard/archive/master.zip)button

```
$ git clone https://github.com/guoswang/TensorBoard.git
$ cd TensorBoard
```
**Step 2.** Download [MNIST](http://yann.lecun.com/exdb/mnist/) dataset. In this step, you have two choices:  
- a) Automatic downloading with  ==download_data.py== script

```
$ python download_data.py  
```
- b) Manual downloading with wget or other tools, move and extract dataset into ==data/mnist== directory, for example:

```
$ mkdir -p data/mnist
$ wget -c -P data/mnist http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
$ wget -c -P data/mnist http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz
$ wget -c -P data/mnist http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz
$ wget -c -P data/mnist http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz
$ gunzip data/mnist/*.gz
```
**Step 3.** Start the training and testing(Using the MNIST dataset by default):

```
$ python main.py
$ tensorboard --logdir='log'
```
**Step 4.** You will get a website after Step 3. You can navigate to the website.
## Results
1. SCALARS
展示的是标量的信息，程序中用tf.summary.scalars()定义的信息都会在这个窗口。程序中定义的标量有：准确率accuracy,dropout的保留率，隐藏层中的参数信息，已经交叉熵损失。这些都在SCLARS窗口下显示出来了。  
点开accuracy,红线表示test集的结果，蓝线表示train集的结果，可以看到随着循环次数的增加，两者的准确度也在通趋势增加
![这里写图片描述](http://img.blog.csdn.net/20180122100335577)
点开dropout，红线表示的测试集上的保留率始终是1，蓝线始终是0.9  
![这里写图片描述](http://img.blog.csdn.net/20180122100613016)
点开layer1，查看第一个隐藏层的参数信息。 
![这里写图片描述](http://img.blog.csdn.net/20180122100802424)
从中我们可以看到偏执项b的信息，随着迭代的加深，最大值越来越大，最小值越来越小，与此同时，也伴随着方差越来越大，这样的情况是我们愿意看到的，神经元之间的参数差异越来越大。因为理想的情况下每个神经元都应该去关注不同的特征，所以他们的参数也应有所不同。     
权值w的信息，同理，最大值，最小值，标准差也都有与b相同的趋势，神经元之间的差异越来越明显。w的均值初始化的时候是0，随着迭代其绝对值也越来越大。  

   点开layer2
![这里写图片描述](http://img.blog.csdn.net/20180122100943794)
点开loss，可见损失的降低趋势。
![这里写图片描述](http://img.blog.csdn.net/20180122101408907)
## More information in faiculty:
![这里写图片描述](http://img.blog.csdn.net/20180122102309282)
