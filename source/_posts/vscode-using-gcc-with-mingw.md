---
title: Windows 下 VS code 配置 C/C++ 环境
date: 2022-04-19 09:34:45
categories: 教程
tags: 
- VS code
- C/C++
- Blog
---

阅读本文后应该可以顺利的在 Windows 系统下配置好 VS code 的 C/C++ 环境。
----
若是继续快速配置环境，可直接到 **[可直接使用的配置文件](#可直接使用的配置文件)** 处复制代码到对应文件，然后即可使用。

### 前提条件

默认已经安装好 `VS code` 和 `C/C++` 编译器 —— `MinGW`。

若是未能安装，那就自行安装吧。~~（自己找教程去）~~

(`ヮ´ ) 开摆！

安装好了的话，那就开整。

ᕕ( ᐛ )ᕗ

### 所需插件

配置环境只需要两个插件：

+ `C/C++` : 让 `VS code` 支持 `C/C++` 语法和编译调试
+ `C/C++ Extension Pack` : 暂时不知道

### 基础环境配置

配置好 `C/C++` 环境大致也就需要几个步骤：

#### 使用 `VS code` 打开一个文件夹作为**工作路径**
   
   该文件夹可以包含子文件夹，或是创建子文件夹，配置好环境后，该文件夹会多一个 `.vscode`，该文件夹会有几个 `json` 文件。
#### 在该文件夹目录中创建 `C/C++` 文件，并进行编辑
   
   简单的编辑一下就好，比如输出个 Hello World。
#### 首先进行配置生成任务
   
   选择已经编辑好的 C/C++ 文件，点击顶部菜单栏的 `终端(T) > 配置任务`。

   [![LDXoe1.png](https://s1.ax1x.com/2022/04/20/LDXoe1.png)](https://imgtu.com/i/LDXoe1)

   在选择 `C/C++: gcc.exe 生成活动文件`。
   > 因为自己使用 `C` 文件进行配置任务，因为配置任务时显示的是 `gcc.exe`。
   > 若是使用 `C++` 文件进行配置任务，会显示 `g++.exe`。
   > `gcc.exe` 是 `C` 的编译器
   > `g++.exe` 是 `C++` 的编译器，但是也可以编译 `C`
   > 不过这一点没什么大问题，都可以在后续的 `json` 文件中修改

   [![LDjiY8.png](https://s1.ax1x.com/2022/04/20/LDjiY8.png)](https://imgtu.com/i/LDjiY8)

   之后会自动生成一个 `task.json` 文件，位于 `.vacode` 文件夹，如图：

   [![LDxeI0.png](https://s1.ax1x.com/2022/04/20/LDxeI0.png)](https://imgtu.com/i/LDxeI0)

   进入 `task.json`:

   [![LDxBsH.png](https://s1.ax1x.com/2022/04/20/LDxBsH.png)](https://imgtu.com/i/LDxBsH)

   其中：
   + type: 要自定义的任务类型
       可支持类型： `cppbuild`, `shell`, `process`.
  
   + label: 任务名称。即是你将在任务列表中看到的值（就是上上上图中可见的：C/C++：gcc.exe 生成活动文件）；你可以给它取任何你喜欢的名字。
      > 该值还和后续调试任务有关

   + command: 执行编译器或编译脚本的路径。
   + args: 其他要传给编译器或者编译脚本的参数。
   + ~~options：其他命令选项。~~
     + ~~cwd: 已执行程序或脚本的当前工作目录。如果省略，则使用当前代码的工作区根。~~
   + problemMatcher: 要使用的问题匹配程序。可以是一个字符串或一个问题匹配程序定义，也可以是一个字符串数组和多个问题匹配程序。
   + group: build: 将任务标记为可通过“运行生成任务”命令访问的生成任务。
   + detail: 任务的其他详细信息。


   `task.json`: 
   ```json
   {
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: gcc.exe 生成活动文件",
			"command": "C:/MinGW/bin/gcc.exe",
                     
			"args": [
				"-fdiagnostics-color=always", // 彩色警告
				"-g",                         // 编译器编译时，产生调试信息
				"${file}",                    // 当前文件名(含有文件路径)
				"-o",                         // 编译时输出的位置
				"${fileDirname}/${fileBasenameNoExtension}.exe"
                                          // 编译输出的可执行文件
			],
			"problemMatcher": [
				"$gcc"
			],
			   "group": "build",
			   "detail": "编译器: C:/MinGW/bin/gcc.exe"
		   }
	   ]
   }
   ```

   然后点击 `终端(T) > 运行生成任务`，如图：
   > 当然可以使用快捷键 `Shift + Ctrl + B`，快速 `运行生成任务`。

   [![Lrokg1.png](https://s1.ax1x.com/2022/04/20/Lrokg1.png)](https://imgtu.com/i/Lrokg1)

   此时，VS code 下部的终端就会显示 `Executing task`， 即开始编译 C 文件并获得 exe 文件。
   > 从图中可见，运行的任务将 task.json 中的部分内容显示出来。
   > 如：
   > + label
   > + 编译的指令
   > > 成功执行指令后，会显示`生成已成功完成`。
   > > 未能成功执行时，则会显示`错误信息`。

   [![LrTcQI.png](https://s1.ax1x.com/2022/04/20/LrTcQI.png)](https://imgtu.com/i/LrTcQI)

   成功之后，在文件夹中会多出对应的 exe 文件，如图：
   [![LrL2a6.png](https://s1.ax1x.com/2022/04/20/LrL2a6.png)](https://imgtu.com/i/LrL2a6)

   强调一下，将上述任务完成后，我们只是利用 task.json 配置文件将 C 文件编译成了可执行的 exe 文件后续没有执行 该 exe 文件。想要查看运行结果的话：有两种办法：
   + 在 VS code 的终端中输入相应的指令以执行文件
   + 到对应的文件夹中找到该 exe 文件，直接执行。

   若是需要对代码进行调试，就需要配置接下来的 `launch.json` 文件。

#### 其次进行配置调试任务
   点击 `运行(R) > 添加配置`，如图:

   [![LrvNy4.png](https://s1.ax1x.com/2022/04/20/LrvNy4.png)](https://imgtu.com/i/LrvNy4)

   再次点击图中选项
   > 由于不明原因，我这点击该选项后，直接生成了 launch.json 文件，但是是空的，和其他教程不一样，不过问题不大，就是配置复杂了一点。
   > ↙(`ヮ´ )↗ 开摆！

   [![LrxiX4.png](https://s1.ax1x.com/2022/04/20/LrxiX4.png)](https://imgtu.com/i/LrxiX4)
   生成 launch.json 文件。
   [![Lrz3xU.png](https://s1.ax1x.com/2022/04/20/Lrz3xU.png)](https://imgtu.com/i/Lrz3xU)

   空的？没事，点击右边的 `添加配置`，选择 `C/C++: (gdb) 启动`。
   > 之所以选择该选项，是在我尝试了各选项的配置后做出的决定。
   > 原因吗：
   > + 功能刚好，基本满足要求
   > + 没有复杂 ~~（可能无用的）~~ 的配置选项 


   [![LskEHU.png](https://s1.ax1x.com/2022/04/20/LskEHU.png)](https://imgtu.com/i/LskEHU)

   然后生成的配置文件大致如图所示，不过还不能直接用，还需要修改其中部分字段。
   [![LsAaoF.png](https://s1.ax1x.com/2022/04/20/LsAaoF.png)](https://imgtu.com/i/LsAaoF)

   各字段的作用：
   + name: 配置名称，用于显示在启动配置的下拉菜单中。
   + type: 配置类型。
   + request: 请求配置类型。可是 `启动` 或 `附加`，对应 `launch` 和 `attach`。
   + program: 程序可执行的完整路径。
   + args: 传递给程序的命令行参数。
   + stopAtEntry: 可选参数。如果是为 true，则调试程序就会在目标的入口点处停止。如果传递了 processId，则不起任何作用。
   + cwd: 目标的工作目录。
   + environment: 要添加到程序环境的环境变量。
   + externalConsole: 如果为 true，则为调试对象启动控制台；为 false，则会在 linux 和 Windows 上显示在集成控制台中。
      > 意思就是：
      > true: 额外开启一个控制台来显示结果。
      > false: 直接在 VS code 的集成终端显示结果。 
   + MIMode: 指示 MIDebugEngine 要连接到的控制台调试程序。允许的值，`gdb`、`lldb`。
   + miDubuggerPath: MI 调试程序（如 gdb）的路径。如若未指定（如 gdb.exe），将首先在路径中搜索调试程序。
   + setupCommands: 为了安装基础调试程序而执行一个或多个 GDB/LLDB 命令。
     + description: 此命令的可选说明。
     + text: 要执行的调试命令。
     + ignoreFailures: 如果为 true，则会忽略该命令执行失败。默认值：false。

   对 `program`、`miDebuggerPath`、`externalConsole` 等字段进行修改后。
   可得正常使用的 `launch.json`:
   > 在该文件中，加了一新的字段 `preLaunchTask`，用于调试时从新生成 exe 文件，并根据新的 exe 文件进行调试。
   > 否则，在对代码进行修改后，直接使用调试功能，你会发现，执行的是之前的程序，而非修改后的程序。
   > 
   > preLaunchTask: 调试会话开始前要运行的任务。
   
   ```json
   {
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "preLaunchTask": "C/C++: gcc.exe 生成活动文件", // 在 launch 之前的任务名，
                                                           // 即 在launch 之前先执行 task.json 的任务
                                                           // 用于调试时从新生成 exe 文件，并根据新的 exe 文件进行调试
                                                           // 因而该字段内容需和 task.json 中的 label 一样，如此才能正确的先生成再调试
            "request": "launch",
            "program": "${workspaceFolder}/${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "C:/MinGW/bin/gdb.exe",
            "setupCommands": [
                  {
                     "description": "为 gdb 启用整齐打印",
                     "text": "-enable-pretty-printing",
                     "ignoreFailures": true
                  },
                  {
                     "description":  "将反汇编风格设置为 Intel",
                     "text": "-gdb-set disassembly-flavor intel",
                     "ignoreFailures": true
                   }
               ]
           }
       ]
   }
   ```
   此时会到 C 文件，就可以点击 `运行(R) > 启动调试` 来调试程序，快捷键：`F5`，或是 `运行(R) > 以非调试模式运行` 来运行程序（不调试），快捷键：`Ctrl + F5`。结果如图：

   [![LslIqH.png](https://s1.ax1x.com/2022/04/20/LslIqH.png)](https://imgtu.com/i/LslIqH)

至此，Windows 系统下 VS code 的 C/C++ 环境算是配置完成了。

好耶！

ᕕ( ᐛ )ᕗ

### 进阶环境配置



### 可直接使用的配置文件


### 参考
+ [Visual Studio Code 官方文档 | GCC on Windows](https://code.visualstudio.com/docs/cpp/config-mingw#_build-helloworldcpp)
+ [Visual Studio Code 官方文档 | Variables Reference](https://code.visualstudio.com/docs/editor/variables-reference)
+ [【开发环境】Ubuntu 中使用 VSCode 开发 C/C++ ⑤ ( tasks.json 中的 args 数组配置分析 | 编译并执行 C++ 程序 )](https://blog.51cto.com/u_14202100/5188327)