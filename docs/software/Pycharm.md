# Python开发工具的安装

## 1.首先我们要进行Pyhton解释器的下载

```python
print('Hello World')
```
Python不能直接在计算机中运行，因此需要Python语言的运行环境：Python解析器

下载地址：https://www.python.org/downloads/release/python-379/
当然你安装3.8或者3.9也是没问题的

查找目标文件：Windows x86-64 executable installer -- 单击即可下载。(格式不能找错)

## 2.Python解析器的安装

第一步：双击运行Python的解析器，选择==自定义安装==以及==添加Python到环境变量(这一步非常重要)==

第二步：选择所有要安装的功能菜单，默认全部勾选

第三步：设置Python解析器的安装路径，尽量不要安装在C盘，但需要知道自己安装的位置

第四步：测试Python解析器是否可以使用
方法：按Windows + R，输入cmd，打开Windows的DOS窗口，输入python（全部小写）,当出现下图就成功了

![image-python解释器.png](https://github.com/Shl1015CS/AI-learning/blob/master/%E5%9B%BE%E7%89%87/python%E8%A7%A3%E9%87%8A%E5%99%A8.png)

使用exit()退出

## 3. Python开发工具PyCharm(我下载的是2021.2.1)新版容易出现位置问题

在不涉及到人工智能的方向，推荐不用安装anaconda，直接安装PyCharm即可。它是目前功能最强大的IDE

PyCharm一共有两个版本：专业版（收费） 与 社区版（免费、开源）。我们选择后者

下载PyCharm。https://www.jetbrains.com/pycharm/download/

第二步：设置软件的安装路径，不用安装在C盘

第三步：PyCharm基本设置。如下图设置，不建议把pycharm添加到环境变量里面

![image-pycharm图片.png](https://github.com/Shl1015CS/AI-learning/blob/master/%E5%9B%BE%E7%89%87/pycharm%E5%9B%BE%E7%89%87.png)

## 4.创建Python项目

第一步：创建项目(Pycharm不要汉化！不要汉化！不要汉化！)

点开图标，初次点开会有一个提示窗口，不用管他，点击New Project

![image-Pycharm打开界面.png](https://github.com/Shl1015CS/AI-learning/blob/master/%E5%9B%BE%E7%89%87/Pycharm%E6%89%93%E5%BC%80%E7%95%8C%E9%9D%A2.png)

第二步：设置项目路径，尽量放到C盘以外（非常重要！！）

你会看到类似如下图片。(因为我使用的是虚拟机安装，只用于开发pycharm，只有一个盘所以放在了C盘)

![image-pycharm配置界面.png](https://github.com/Shl1015CS/AI-learning/blob/master/%E5%9B%BE%E7%89%87/pycharm%E9%85%8D%E7%BD%AE%E7%95%8C%E9%9D%A2.png)

其中base interpreter会自动感知到python.exe的位置，没感知到可以手动定位(找到python安装路径然后选定python.exe)

新建文件并书写代码

```python
print('Hello World')
```

进行运行，右上角绿色的三角符号Run。

结果如下，就完成啦。

![image-Pycharm的配置结果.png](https://github.com/Shl1015CS/AI-learning/blob/master/%E5%9B%BE%E7%89%87/Pycharm%E7%9A%84%E9%85%8D%E7%BD%AE%E7%BB%93%E6%9E%9C.png)
