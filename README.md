# git-
git忽略文件的处理

在使用git做代码管理时，对于诸如UserInterfaceState.xcuserstate的文件，不让这样的文件提交到版本代码库中，因此在git提交时，要忽略掉这样的文件，
因此，需要配置.gitignore忽略文件来处理这些文件，使在代码提交时，不用再管理提交这些要忽略的文件。常见的配置.gitignore文件的时机分三种场景，如下：
1）项目初建时，当使用诸如coding或者gitlab等第三方代码存储库时，在创建项目时，会有添加.gitignore选项，直接选择添加忽略文件.gitignore选项就可以了
2）项目初建时没有.gitignore选项,需要自己创建.gitignore文件并填写忽略内容
3） 项目已经开发一段时间了，但一直没有添加.gitignore忽略文件，现在为了团队开发方便，需要添加忽略文件：此时已经远程库里已经存在xcuserstate等需要
忽略的文件，此时添加忽略文件的方法是，在.git文件同级并列目录下，自己创建.gitignore文件并填写忽略内容，然后将忽略文件上传push到远程服务器；紧接着，
删除本地的存在的xcuserstate等需要忽略的文件，然后push上传到远程库，就将远程库对应的xcuserstate等需要忽略的文件删除掉了，以后忽略文件就会自动忽略，
不用再管理了

下面介绍下第二种和第三种情况下，创建.gitignore文件的步骤：
1 首先cd到工程目录下，查看是否存在.gitignore文件：
终端指令：
cd /项目本地工程目录
ls -la (目的 查看工程目录下所有文件，查看是否有.gitignore文件）
终端中显示的文件目录层级如下：
total 56
drwxr-xr-x  15 lihaifeng  staff   510 12  6 10:16 .
drwxr-xr-x  17 lihaifeng  staff   578 12  6 16:06 ..
-rw-r--r--@  1 lihaifeng  staff  6148 12  8 17:33 .DS_Store
drwxr-xr-x  13 lihaifeng  staff   442 12  7 17:53 .git
-rw-r--r--@  1 lihaifeng  staff  1397 12  6 10:16 .gitignore
-rw-r--r--   1 lihaifeng  staff  1073 12  6 09:32 LICENSE
-rw-r--r--   1 lihaifeng  staff   693 12  6 09:32 Podfile
-rw-r--r--   1 lihaifeng  staff  1561 12  6 09:32 Podfile.lock
drwxr-xr-x  15 lihaifeng  staff   510 12  8 09:02 Pods
-rw-r--r--   1 lihaifeng  staff    26 12  6 09:32 README.md
drwxr-xr-x  12 lihaifeng  staff   408 12  6 09:32 债云端
drwxr-xr-x   5 lihaifeng  staff   170 12  6 09:32 债云端.xcodeproj
drwxr-xr-x   4 lihaifeng  staff   136 12  6 09:32 债云端.xcworkspace
drwxr-xr-x   4 lihaifeng  staff   136 12  6 09:32 债云端Tests
drwxr-xr-x   4 lihaifeng  staff   136 12  6 09:32 债云端UITests

2 经过ls -la可以确定.gitignore文件有无，如果有，可以直接使用终端输入指令open .gitignore，打开.gitignore文件，将要忽略的文件内容添加进去，
可以从https://github.com/github/gitignore博客中查找对应语言的忽略文件内容，粘贴到打开的.gitignore文件中即可；
即终端指令：open .gitignore
如果不存在.gitignore文件，则使用终端指令touch .gitignore，创建一个和.git同级目录下的空白.gitignore文件，然后终端指令open .gitignore，
打开空白的.gitignore文件，同样从https://github.com/github/gitignore博客中查找对应语言的忽略文件内容，粘贴到打开的.gitignore文件中即可；
忽略文件粘贴完成，将.gitignore文件提交push到远程代码库中即可了，这样，远程代码库中就存在.gitignore文件了，任何人拉取代码都会有.gitignore文件了
；第二种场景下的忽略文件就配置结束了，可以使用了

3 对于第三种场景下要忽略的xcuserstate文件已经存在的，到上面的第二部还没结束，必须要把远程库里已经存在的xcuserstate文件要删除掉才可以，因此，
远程库里上传完配置.gitignore文件后，要继续删除本地和远程库的xcuserstate等文件，执行终端指令先后顺序如下：
git rm --cached [YourProjectName].xcodeproj/project.xcworkspace/xcuserdata/[ YourUsername].xcuserdatad/UserInterfaceState.xcuserstate
注意：上面的[YourProjectName].xcodeproj/project.xcworkspace/xcuserdata/[ YourUsername].xcuserdatad/UserInterfaceState.xcuserstate是你本地
库中要忽略删除文件的地址，这个可以通过sourceTree查看，在sourceTree中选中要查看的文件，然后在sourceTree界面的右上方有个Finder按钮，点击就可以看到
文件在什么位置了
git commit -m "Removed file that shouldn't be tracked" 
git push 到远程库就可以了，这几个终端指令，也可以通过sourceTree中的移除文件，提交commit本地，提交push远程来完成
到此，一个完成的三种场景下忽略文件.gitignore的配置添加就完全结束了，希望能帮到你

如有不同意见，可互动探讨

     
