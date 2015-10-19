#study-scikit-learn-source

## 环境搭建
---------
scikit-learn 的源码下载，安装，环境搭建

 从 [GitHub][1] 下载源码
```
git clone git://github.com/scikit-learn/scikit-learn.git
```
cd 到scikit-learn 目录 安装
```
python setup.py develop
```
现在就可以运行下载的代码，或并修改后运行。建议使用ide 比如pycharm 这样在阅读代码的时候能快速跳转(按住 ctrl 左键单击函数就能跳转到函数定义的地方）
如有疑问可去[GitHub][2]查找或者[scikit-learn 官方网站][3]详细信息请阅读以下资料：[scikit-learn Contributing][4]

--------
## 阅读顺序
>* 按从相对简单到难的顺序阅读
>* 如果公司项目需要用到某部分 就提前阅读该部分

----------
## 笔记方法
>* 每个人一个目录，记录自己的笔记(其他人可查看，提出理解有异的地方）
>* 一个公共目录public记录需要讨论的问题，和进度信息
>* 采用markdown的方式记录笔记，这里有一个[markdown 的在线编辑工具][5]


---------
## 备注
scikit-learn 代码阅读主要两个为了 学习python 和算法  源码中会涉及到一些python 的细节问题，如果在代码的阅读过程中，陷入这些细节的部分，就不太好提高效率，和算法的学习。可先跳过这些细节，也可记录下，到后面这些问题遇到多了就能理解了。
尽量多的写代码，scikit-learn 有大量格式化的数据可用来使用




  [1]: https://github.com/scikit-learn/scikit-learn
  [2]: https://github.com/scikit-learn/scikit-learn
  [3]: http://scikit-learn.org/stable/index.html
  [4]: http://scikit-learn.org/stable/developers/index.html#testing-coverage
  [5]: https://www.zybuluo.com
  