[一篇讲得很好的文章](http://www.cnblogs.com/HappyAngel/archive/2011/02/07/1949762.html)
问题起源于编程珠玑Column 12中的题目10，其描述如下：

　　How could you select one of n objects at random, where you see the objects sequentially but you do not know the value of n beforehand? For concreteness, how would you read a text file, and select and print one random line, when you don’t know the number of lines in advance?

　　问题定义可以简化如下：在不知道文件总行数的情况下，如何从文件中随机的抽取一行？

　　首先想到的是我们做过类似的题目吗?当然，在知道文件行数的情况下，我们可以很容易的用C运行库的rand函数随机的获得一个行数，从而随机的取出一行，但是，当前的情况是不知道行数，这样如何求呢？我们需要一个概念来帮助我们做出猜想，来使得对每一行取出的概率相等，也即随机。这个概念即蓄水池抽样（Reservoir Sampling）。

　　有了这个概念，我们便有了这样一个解决方案：定义取出的行号为choice，第一次直接以第一行作为取出行 choice ，而后第二次以二分之一概率决定是否用第二行替换 choice ，第三次以三分之一的概率决定是否以第三行替换 choice ……，以此类推，可用伪代码描述如下：
```
i = 0
while more input lines
    with probability 1.0/++i
         choice = this input line
print choice
```
　　这种方法的巧妙之处在于成功的构造出了一种方式使得最后可以证明对每一行的取出概率都为1/n（其中n为当前扫描到的文件行数），换句话说对每一行取出的概率均相等，也即完成了随机的选取。

　　证明如下：
  ![](http://upload-images.jianshu.io/upload_images/3174228-c86eb20164dcfd0a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


　　回顾这个问题，我们可以对其进行扩展，即如何从未知或者很大样本空间随机地取k个数？

　　类比下即可得到答案，即先把前k个数放入蓄水池，对第k+1，我们以k/(k+1)概率决定是否要把它换入蓄水池，换入时随机的选取一个作为替换项，这样一直做下去，对于任意的样本空间n，对每个数的选取概率都为k/n。也就是说对每个数选取概率相等。

　　伪代码：
```
Init : a reservoir with the size： k
for i= k+1 to N
    M=random(1, i);
    if( M < k)
       SWAP the Mth value and ith value
end for 
```
　　证明如下：
  ![](http://upload-images.jianshu.io/upload_images/3174228-6e4984f2b992039f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

　　蓄水池抽样问题是一类问题，在这里总结一下，并由衷的感叹这种方法之巧妙，不过对于这种思想产生的源头还是发觉不够，如果能够知道为什么以及怎么样想到这个解决方法的，定会更加有意义。
