#! https://zhuanlan.zhihu.com/p/226190284
# CS143：编译原理 | 环境搭建HelloWorld

本文是本人新开的坑的第一篇博客，另一个坑请看[MIT 6.828 实现操作系统](https://zhuanlan.zhihu.com/p/166413604)。从另一个坑的第一篇复制两段话：

>   写成博客的目的是防止自己走马观花，花了一堆时间还什么都没学到。

>   虽然我对我的表达能力很自信，但是我写博客的目的不是教给别人什么东西，而是逼迫自己认真操作、认真阅读。如果你的知识背景和我类似，你看我的博客将非常畅快，否则最好还是看原始的讲义。

So you have been warned.

CS143是斯坦福的编译原理导论课，常听说这个课的`Assignment`很难，值得一做。各个`Assignment`实现了一个`cool`语言编译器。`cool`语言不是真正使用在生产环境中的，只是一个教学用具，语法和`opencl`有点像，你可以使用`opencl`的语法高亮来阅读代码。做完之后，能够加深对编译原理的各个方面的理解。

本文只进行**环境搭建和材料准备**，具体实现在之后的文章中发出。

本文md文档源码链接：[AnBlogs](https://github.com/Anarion-zuo/AnBlogs/blob/master/cs143/pa0-setup.md)

# 官网材料下载

你可能需要两种材料，课程视频和课件作业。前者在B站可以找到，后者的大部分在[课程网站](http://web.stanford.edu/class/cs143/)。然而，斯坦福把这个课从`Cousera`和自家的MOOC上撤掉了，我花了些时间才找到编程作业，在[edx.org](https://courses.edx.org/courses/course-v1:StanfordOnline+SOE.YCSCS1+2T2020/course/)，不知道将来会不会把这个也撤了。如果你真的找不到一些素材，可以在评论区提醒我。

你可以在以上两个链接里面到处看看。

![Table of Content](pa0-setup.assets/image-20200908213805651.png)

我的博客记录我实现各个`Programming Assignment`的历程，当然要引用编译原理的知识，但是不会系统讲解，也不会看`Written Assignment`。如果你还没有系统学习过编译原理，可以参考课程视频进行学习，或配合着一些教科书。

每个`Assignment`有对应的说明`handout`和一些已经写好了的代码，这些都可以在以上两个链接中找到。

# 环境搭建

在[edx.org](https://courses.edx.org/courses/course-v1:StanfordOnline+SOE.YCSCS1+2T2020/course/)中，提供了两种搭建环境的方法，分别是使用虚拟机，和直接在Linux下配置。

如果你目前正在使用Windows作为主要开发环境，可以在`VirtualBox`中导入[提供的虚拟机](https://stanford.box.com/s/28bcmqycmsxme77gi1ep1yo9lo27znrz)。这是个古老的发行版，我没有深入研究过，应该近似`Ubuntu 10.04`或`11.10`。运行这个虚拟机，就可以直接获得配置好的环境。你可以通过`VSCode`远程开发插件在虚拟机上写代码。

如果你目前正在使用Linux作为主要开发环境，可以不使用这个虚拟机。我的`VirtualBox`貌似不能兼容最新版本的Linux内核，而我又不小心更新了，也就没有使用虚拟机。以下是Linux下的环境搭建。

在[edx.org](https://courses.edx.org/courses/course-v1:StanfordOnline+SOE.YCSCS1+2T2020/course/)中，提供了一个压缩包[下载链接](https://courses.edx.org/asset-v1:StanfordOnline+SOE.YCSCS1+1T2020+type@asset+block@student-dist.tar.gz)，`wget`这个链接，解压到目录`/usr/class`下。这是官方配置方式。

从我目前为止的使用来看，我们可以把其它文件留在我们想要的地方，而将`bin`子目录下的内容加入环境变量，就可以正常使用课程需要的一些可执行文件，没必要维持那个目录结构。

设置好环境变量后，在命令行输入`coolc`，应该可以看到`cool`编译器的输出，提示`Main`入口类不存在。

```shell
Class Main is not defined.
Compilation halted due to static semantic errors.
```

我用`VSCode`，所有`Assignment`都在目录`assignment`下，现在就可以开始了。

![VSCode](pa0-setup.assets/image-20200908215942454.png)

# 象征性HelloWorld

你可以自己写一个`Cool`程序，然后用`coolc`编译，用`spim`执行得到的汇编代码。如果要认真操作，你还需研究`coolc`和`spim`的使用。可以暂时不那么复杂，咱就想试一下配置是否正确而已。

进入`assignments/PA1`目录，在这个目录下运行`make test`，可以看到一行输出`Nothing implemented`。这是在文件`stack.cl`下写的，你可以看看`Makefile`。

```java
// stack.cl
class Main inherits IO {
   main() : Object {
      out_string("Nothing implemented\n")
   };
};

// Makefile
test:	compile
	@echo stack.test
	${CLASSDIR}/bin/spim -file stack.s < stack.test
```

能够正确输出，就是配置基本完成了。

之后可能有所调整，不过大概就是这样。