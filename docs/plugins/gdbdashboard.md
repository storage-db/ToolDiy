# GDB-dashboard 
## 使用python配置了gdb调试界面，完全可以自己写代码去定义整个调试界面可以说是堪比IDE，显示也非常好看，完全基于终端,作为底层的调试软件可以帮助开发者更好的查看变量、寄存器、单步执行等
## 安装(linux环境)
+ 开源地址 https://github.com/cyrus-and/gdb-dashboard.git
+ 获取
    ```sh
    wget -P ~ https://git.io/.gdbinit #如果网速较慢可以直接新建同名文件.gdbinit之后复制粘贴过来
    ```
+ 效果图 ![gdb效果图](https://raw.githubusercontent.com/wiki/cyrus-and/gdb-dashboard/Screenshot.png)

## 推荐理由
目前的确ide集成了很多的调试工具但是在一些内核编程或者其他的底层开发领域gdb仍然具备不可替代的作用，为此我们希望在原本枯燥的调试终端找到更加便于观察的页面好在已经有人帮我们实现了这一工具为此我们希望把这样的便捷带给每一个人。

## 运行调试基本指令 [gdb调试常见指令](https://www.jianshu.com/p/5663e4a55202)


