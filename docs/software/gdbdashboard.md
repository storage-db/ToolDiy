# GDB-dashboard

## 简介

使用 python 配置了 gdb 调试界面，完全可以自己写代码去定义整个调试界面可以说是堪比 IDE ，显示也非常好看，完全基于终端,作为底层的调试软件可以帮助开发者更好的查看变量、寄存器、单步执行等。

## 安装(linux环境)

+ 开源地址 <https://github.com/cyrus-and/gdb-dashboard.git>

+ 获取
  
  ```sh
  wget -P ~ https://git.io/.gdbinit #如果网速较慢可以直接新建同名文件.gdbinit之后复制粘贴过来
  ```

+ 效果图
  ![gdb效果图](https://raw.githubusercontent.com/wiki/cyrus-and/gdb-dashboard/Screenshot.png)

## 推荐理由

目前 IDE 集成了很多的调试工具，但是在一些内核编程或者其他的底层开发领域 gdb 仍然具备不可替代的作用，为此我们希望在原本枯燥的调试终端找到更加便于观察的页面好在已经有人帮我们实现了这一工具为此我们希望把这样的便捷带给每一个人。

## 运行调试基本指令

参考 [gdb调试常见指令](https://www.jianshu.com/p/5663e4a55202)

## 注意

在使用该插件时需要查看当前所使用的 gdb 是否支持 python 脚本，当出现 `Scripting in the "Python" language is not supported in this copy of GDB.`  时则表明该 gdb 不支持 python 脚本，无法使用该插件。另外，也需要注意 gdb 与 python 的版本是否匹配的问题，见 [issue](https://github.com/cyrus-and/gdb-dashboard/issues/147)
