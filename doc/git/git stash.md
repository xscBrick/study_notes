# git stash 

### git stash

> 功能 : 将改动储藏起来
> 好处：不用add,commit后就可以切换到其特性分支进行其他特性开发

```shell
git stash -m "test_message"	//添加备份说明
git stash push -m "test_message_push" //将工作区储藏起来（可以指定路径）
git stash push testDir/test.txt 	//将testDIr文件夹下的test.txt 储藏起来，其他的工作区内容将不被储藏
git stash save "test_message_save"	//将工作区储藏起来，不需要-m参数，不推荐使用，不能储藏指定路径下的文件，将会储藏整个工作区内容
```



### git stash list

查看所有储藏内容，形成一个列表，最新的储藏再最上面

### git stash push

将工作区内容储藏起来

```shell
git stash push -m "test_message_push" //将工作区储藏起来（可以指定路径）
git stash push testDir/test.txt 	//将testDIr文件夹下的test.txt 储藏起来，其他的工作区内容将不被储藏
```

### git stash apply

将堆栈中的内容应用到当前目录，不同于git stash pop，该命令不会将内容从堆栈中删除，也就说该命令能够将堆栈的内容多次应用到工作目录中，适应于多个分支的情况。

> git stash apply stash@{0}

### git stash pop

将储藏内容弹出并应用，储藏内容会被从储藏列表中删除

> git stash pop  //返回上一个储藏，并移除
> pop [—index] [-q|—quiet] [stash]
> // 如指定 --index 不仅恢复工作区，也会恢复暂存区
> git stash pop stash@{$num} 

### git stash drop [-q | --quiet] [<stash>]

从存储条目列表中删除单个存储条目。如果没有`<stash>`给出，则删除最新的一个。即`stash@{0}`，否则`<stash>`必须是表单的有效存储日志引用`stash@{<revision>}`。

> git stash drop stash@{0}



### 删除所有储藏

> git stash clear

#### git stash show [stash]

显示和他parent的差异