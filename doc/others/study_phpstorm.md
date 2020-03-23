# study_phpstorm

[TOC]



## 终端设置为git

settings->tools->terminal->shell path

"C:\software\Git\bin\sh.exe" --login -i

![image-20191208163552516](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\image-20191208163552516.png)

## [PhpStorm 快捷键大全 PhpStorm 常用快捷键和配置](https://www.cnblogs.com/zmdComeOn/p/10676308.html)

**常用快捷键**

**设置快捷键：File -> Settings -> IDE Settings -> Keymap -> 选择“eclipse” -> 然后“Copy”一份 -> 再个性化设置（自己习惯的）快捷键**

**常用快捷键(keymaps:Default情况下)**



## 说明

此快捷键说明我是翻译官方的快捷键说明的，方便查看，基于PHPStorm的官方Help来翻译的，其他系列的JetBrains软件应该都是一样的道理，其中如有错误，欢迎斧正。

## 编辑

------

| 快捷键组合            | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| Ctrl + Space          | 代码自动完成提示（选择）                                     |
| Alt + Enter           | 显示意图动作和快速修复                                       |
| Ctrl + P              | 参数信息（在调用方法参数忘记的时候，提示）                   |
| Ctrl + Q              | 快速查找文件，可以查找当前类定义的文件等                     |
| Ctrl + 鼠标滑过       | 基本信息                                                     |
| Alt + Insert          | 生成代码...(细节需要多次操作会发现很有意思)                  |
| Ctrl + O              | 重写方法（在PHPStorm中是重写父类方法，会有选择框）           |
| Ctrl + I              | 实现方法（一般是指实现接口类或抽象类方法）                   |
| Ctrl + Alt + T        | 环绕代码块 (if..else, try..catch, for, 等)                   |
| Ctrl + /              | 单行注释(//)                                                 |
| Ctrl + Shift + /      | 块注释 (/**/)                                                |
| Ctrl + W              | 选择依次递增的代码块，具体使用目前来看比较少                 |
| Ctrl + Shift + W      | 去掉当前选择返回上一个选择，类似于撤销选择，与上面的相反     |
| Ctrl + Alt + L        | 格式化代码，一般来说，写的代码格式不整齐统一，这个很有用     |
| Ctrl + Alt + I        | 自啮合线，这个解释不太好解释，测试结果就是会自动根据代码来进行对齐 |
| Ctrl + D              | 复制当前行或选定的块                                         |
| Ctrl + Y              | 删除插入符号所在行                                           |
| Ctrl + Shift + J      | 智能线连接（HTML和JavaScript才有用）                         |
| Ctrl + Enter          | 智能分割线 (HTML 和 JavaScript 才有用)                       |
| Shift + Enter         | 开始新行，比如光标在当前行，不需要切换到行尾按Enter，直接按这个组合键即可 |
| Ctrl + Shift + U      | 切换选中的英文文字的大小写，此处其实用到挺多的               |
| Ctrl + Shift + ] 或 [ | 选择直到代码块的开始或结束，我之前不知道这个，其实很有用     |
| Ctrl + Delete         | 删除从当前光标到当前单词结尾                                 |
| Ctrl + Backspace      | 从光标位置删除到当前单词的开始                               |
| Ctrl + + 或 -         | 这里是ctrl和加号或者减号产生的组合，可以折叠或展开当前代码块 |
| Ctrl + F4             | 关闭活动中的tab                                              |
| Ctrl + Shift + V      | 从历史粘贴                                                   |

## 调试

------

*此处我是用得很少*

| 快捷键组合    | 说明       |
| ------------- | ---------- |
| F8            | 跳过       |
| F7            | 步进       |
| Shift + F8    | 跳出       |
| Alt + F8      | 表达式求值 |
| F9            | 恢复程序   |
| Ctrl + F8     | 切断断点   |
| Ctrl+Shift+F8 | 查看断点   |

## 运行

------

| 快捷键组合         | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| Shift + F10        | 运行                                                         |
| Shift + F9         | 调试                                                         |
| Ctrl + Shift + F10 | 从编辑器运行上下文配置（Run context configuration from editor），此处可能翻译不够准确 |
| Ctrl + Shift + X   | 在命令行运行                                                 |

## 搜索/替换

| 快捷键组合         | 说明              |
| ------------------ | ----------------- |
| Ctrl + F/R         | 查找/替换         |
| F3/Shift + F3      | 查找下一个/上一个 |
| Ctrl + Shift + F/R | 在目录中查找/替换 |

## 查找哪些地方使用

| 快捷键组合           | 说明                                        |
| -------------------- | ------------------------------------------- |
| Alt + F7 / Ctrl + F7 | 当前文件查找被使用/在文件中查找哪些地方使用 |
| Ctrl + Shift + F7    | 文件中搜索并在使用的地方高亮显示            |
| Ctrl + Alt + F7      | 显示哪些地方被使用                          |

## 导航

------

| 快捷键组合               | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| Ctrl + N                 | 跳转到指定类                                                 |
| Ctrl + Shift + N         | 跳转到文件                                                   |
| Ctrl + Alt + Shift + N   | 跳转到符号                                                   |
| Ctrl + G                 | 跳转到第几行                                                 |
| Alt + Right/Left         | 切换编辑器活动窗                                             |
| Esc                      | Go to editor (from tool window)                              |
| Ctrl + E                 | 弹出最近编辑文件，我也是在写这文档才知道，太方便了           |
| Ctrl + Alt + Left/Right  | 导航前进/后退                                                |
| Ctrl + Shift + Backspace | 跳转到最近编辑的代码位置                                     |
| Alt + F1                 | 在任何视图中选择当前文件或符号                               |
| Ctrl + B 或 Ctrl + Click | 跳到申明（如跳转到当前函数声明的地方，这个很常用，可以实操一下） |
| Ctrl + Alt + B           | 与上面相反，跳到执行位置                                     |
| Ctrl + Shift + I         | 打开快速定义查找                                             |
| Ctrl + Shift + B         | 跳转到类型声明                                               |
| Ctrl + U                 | 跳到超级方法(super-method)/超类 (super-class)                |
| Alt + Up/Down            | 跳转到上一个或者下一个方法，在编辑一个类的时候，方便一个一个的方法进行查看 |
| Ctrl + ] / [             | 跳转到代码块的开始或结束                                     |
| F2 / Shift + F2          | 跳转到上一个或下一个高亮错误地方，这个检查代码语法错误很有用 |
| F4 / Ctrl + Enter        | 编辑源代码/查看源代码                                        |

## 重构

------

| 快捷键组合             | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| F5/F6                  | 复制/移动                                                    |
| Alt + Delete           | 安全删除                                                     |
| Shift + F6             | 重命名                                                       |
| Ctrl + Alt + N         | 内联变量                                                     |
| Ctrl + Alt + M/V/F/C   | 提取方法/变量/字段/常数(Method/Variable/Field/Constant)      |
| Ctrl + Alt + Shift + T | 重构这段代码（显示所有可用的重构），比如if else if 这种语句转switch语句 |

## VCS/本地历史

------

| 快捷键组合       | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| Alt + 反引号 (`) | ‘VCS’ 快速弹出，此处需要注意这个反引号在最左上角，和那个~符号在一起的，ESC键下面 |
| Ctrl + K         | 提交项目到VCS                                                |
| Ctrl + T         | 从 VCS 更新项目                                              |
| Alt + Shift + C  | 显示最近更改                                                 |

## 常用操作

------

| 快捷键组合         | 说明                                                       |
| ------------------ | ---------------------------------------------------------- |
| 快速按两次 Shift   | 搜索任何一个地方                                           |
| Ctrl + Shift + A   | 查找方法(Action)                                           |
| Alt + #[0-9]       | 打开相应的工具窗口（这个我也没搞明白）                     |
| Ctrl + Alt + F11   | 开启或关闭全屏模式                                         |
| Ctrl + Shift + F12 | 开启或关闭最大化编辑                                       |
| Alt + Shift + F    | 添加到收藏列表（我觉得这个功能很神奇，不知道为啥要这么做） |
| Alt + Shift + I    | 检查当前文件以及当前配置文件                               |
| Ctrl + Alt + S     | 打开设置对话框（表示会与QQ默认快捷键冲突）                 |
| Ctrl + Tab         | 在 tabs 和工具窗口间切换                                   |

## 插入模板/片段(针对PHPstorm)	

------

| 快捷键组合 | 说明                                 |
| ---------- | ------------------------------------ |
| Alt + J    | 插入模板                             |
| eco        | ‘echo’ 语句                          |
| fore       | foreach(iterable_expr as $value) {…} |
| forek      | foreach(iterable_expr as value) {…}  |
| inc/inco   | ‘include’/‘include_once’ 语句        |
| prif       | private function                     |
| prof       | protected function                   |
| pubf       | public function                      |
| rqr/rqro   | ‘require’/‘require_once’ 语句        |
| 更多...    | 其他自己尝试                         |

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);

```
1 Esc键编辑器（从工具窗口）
2 F1   帮助 千万别按,很卡!
3 F2（Shift+F2）  下/上高亮错误或警告快速定位
4 F3   向下查找关键字出现位置
5 F4   查找变量来源
6 F5   复制文件/文件夹
7 F6   移动
8 F11  切换书签
9 F12  返回到以前的工具窗口
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

注意：部分快捷键，必须在没有更改快捷键的情况下才可以使用

查询快捷键

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 1 CTRL+N   查找类
 2 CTRL+SHIFT+N  查找文件，打开工程中的文件(类似于eclipse中的ctrl+shift+R)，目的是打开当前工程下任意目录的文件
 3 CTRL+SHIFT+ALT+N 查 找类中的方法或变量(JS)
 4 CIRL+B   找变量的来源，跳到变量申明处
 5 CTRL+ALT+B  找所有的子类
 6 CTRL+SHIFT+B  找变量的 类
 7 CTRL+G   定位行，跳转行
 8 CTRL+F   在当前窗口查找文本
 9 CTRL+SHIFT+F  在指定路径查找文本
10 CTRL+R   当前窗口替换文本
11 CTRL+SHIFT+R  在指定路径替换文本
12 ALT+SHIFT+C  查找修改的文件，最近变更历史
13 CTRL+E   最近打开的文件
14 F3   查找下一个
15 SHIFT+F3  查找上一个
16 F4   查找变量来源
17 CTRL+ALT+F7  选 中的字符 查找工程出现的地方
18 ALT+F7 直接查询选中的字符
19 Ctrl+F7  文件中查询选中字符
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

自动代码

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 1 ALT+回车  导入包,自动修正
 2 CTRL+ALT+L  格式化代码
 3 CTRL+ALT+I  自动缩进
 4 CTRL+ALT+O  优化导入的类和包
 5 CTRL+E  最近更改的文件/代码
 6 CTRL+SHIFT+SPACE 切换窗口
 7 CTRL+SPACE空格  代码自动完成，代码提示,一般与输入法冲突
 8 CTRL+ALT+SPACE  类 名或接口名提示（与系统冲突）
 9 CTRL+P   方法参数提示，显示默认参数
10 CTRL+J   自动代码提示，自动补全
11 CTRL+ALT+T  把选中的代码放在 TRY{} IF{} ELSE{} 里
12 ALT+INSERT  生成代码(如GET,SET方法,构造函数等)
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

复制快捷方式

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
1 F5   复制文件/文件夹
2 CTRL+C   复制
3 CTRL+V   粘贴
4 CTRL+X   剪 切,删除行
5 CTRL+D   复制行
6 Ctrl + Y    删除行插入符号
7 CTRL+SHIFT+V  可以复制多个文本
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

高亮

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
1 CTRL+F   选中的文字,高亮显示 上下跳到下一个或者上一个
2 F2（Shift+F2） 高亮错误或警告快速定位
3 SHIFT+F2  高亮错误或警告快速定位
4 CTRL+SHIFT+F7  高亮显示多个关键字. 
5 本地历史VCS/SVN
6 Alt +反引号（'） 快速弹出VCS菜单
7 Ctrl + K         提交项目VCS
8 Ctrl + T         更新项目从VCS
9 Alt + Shift + C  查看最近发生的变化
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

其他快捷方式

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 1 CTRL+Z        倒退(代码后悔)
 2 CTRL+SHIFT+Z  向前
 3 CTRL+H        显 示类结构图
 4 Ctrl +F12      文件结构弹出
 5 Ctrl+Shift+H  方法的层次结构
 6 Ctrl+Alt+H    呼叫层次
 7 CTRL+Q   显示代码注释
 8 CTRL+W   选中代码，连续按会 有其他效果
 9 Ctrl+Shift+W   减少当前选择到以前的状态
10 CTRL+B   转到声明，快速打开光标处的类或方法说明注释(CTRL + 鼠标单击 也可以)
11 CTRL+O   魔术方法
12 CTRL+/   注释//取消注释  
13 CTRL+SHIFT+/  注释/*...*/
14 CTRL+ []   光标移动到 {}[]开头或结尾位置
15 CTRL+SHIFT+[]    选中块代码，可以快速复制
16 ctrl + '-/+': 可以折叠项目中的任何代码块,包括htm中的任意nodetype=3的元素，function,或对象直接量等等。它不是选中折叠，而是自动识别折叠。
17 ctrl + '.': 折叠选中的代码的代码
18 Ctrl+Shift+U   选中的字符大小写转换
19 ctrl+shift+i      快速查看变量或方法定义源
20 CTRL+ALT+F12  资源管理器打开文件夹，跳转至当前文件在磁盘上的位置
21 ALT+F1   选择当前文件或菜单中的任何视图工具栏
22 SHIFT+ALT+INSERT 竖编辑模式
23 CTRL+ALT ←/→  返回上次编辑的位置
24 ALT+ ←/→  切换代码视图，标签切换
25 ALT+ ↑/↓  在方法间快速移动定位
26 alt + '7': 显示当前的类/函数结构。类似于eclipse中的outline的效果。试验了一下，要比aptana的给力一些，但还是不能完全显示prototype下面的方法名。
27 SHIFT+F6  重命名,重构 当前区域内变量重命名/重构
28 不但可以重命名文件名，而且可以命名函数名，函数名可以搜索引用的文件，还可以重命名局部变量。还可以重命名标签名。在sublime text中有个类似的快捷键：ctrl+shift+d。
29 ctrl+shift+enter(智能完善代码 如 if()) 
30 ctrl+shift+up/down(移动行、合并选中行，代码选中区域 向上/下移动) 
31 CTRL+UP/DOWN  光标跳转到编辑器显示区第一行或最后一行下
32 ESC   光标返回编辑框
33 SHIFT+ESC  光 标返回编辑框,关闭无用的窗口
34 CTRL+F4   关闭当前的编辑器或选项卡
35 Ctrl + Alt + V引入变量
36 Ctrl + Alt + F 类似引入变量
37 Ctrl + Alt + C引入常量
38 Ctrl + Tab   键切换选项卡和工具窗口
39 Ctrl + Shift + A  查找快捷键
40 Alt + ＃[0-9]      打开相应的工具窗口
41 Ctrl + Shift + F12 切换最大化编辑器
42 Alt + Shift + F    添加到收藏夹
43 Alt + Shift + I    检查当前文件与当前的配置文件
44 Ctrl +反引号（`）  快速切换目前的配色/代码方案/快捷键方案/界面方案
45 Ctrl + Alt + S     打开设置对话框（与QQ冲突）
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

运行

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
1 Alt + Shift + F10  选择的配置和运行
2 Alt + Shift + F9   选择配置和调试
3 Shift + F10        运行
4 Shift + F9调试
5 Ctrl + Shift + F10运行范围内配置编辑器
6 Ctrl + Shift + X运行命令行
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

调试

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
1 F8步过
2 F7步入
3 Shift + F7智能进入
4 Shift + F8步骤
5 ALT + F9运行到光标
6 Alt + F8计算表达式
7 F9恢复程序
8 Ctrl + F8切换断点
9 Ctrl + Shift + F8查看断点
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

导航

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
1 Shift + Esc键隐藏活动或最后一个激活的窗口
2 Ctrl + Shift + F4关闭活动运行/消息/ / ...选项卡
3 Ctrl + Shift + Backspace键导航到最后编辑的位置
4 Ctrl + Alt+B   到实施（S）
5 Ctrl + Shift+I  打开快速定义查询
6 Ctrl + U        转到super-method/super-class
7 Alt + Home      组合显示导航栏
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

书签

```
1 Ctrl + F11切换书签助记符
2 Ctrl +＃[0-9]转到编号书签
3 Shift + F11显示书签
```

编辑

```
1 Ctrl + Q      快速文档查询
2 ALT + INSERT  生成的代码...器（getter，setter方法，构造函数）
3 Ctrl + O      覆盖方法
4 Ctrl + I      实现方法
```

 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 1 Alt + Enter   显示意图的行动和快速修复
 2 Shift + Tab   键缩进/取消缩进选中的行
 3 Ctrl + Shift + J  智能线连接（仅适用于HTML和JavaScript）
 4 Ctrl + Enter      智能线分割（HTML和JavaScript）
 5 Shift + Enter     开始新的生产线
 6 Ctrl + Delete   删除字（word）
 7 Ctrl + Backspace删除字开始
 8 Ctrl +小键盘+ / - 展开/折叠代码块
 9 Ctrl + Shift +小键盘+展开全部
10 Ctrl + Shift +数字键盘关闭全部
```