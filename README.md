## 目的
网络上很多自动打包命令，但是百度之后很多都不能直接使用，所以创建一个Demo供大家使用，下载后可以直接运行的Demo

## 注意事项
以下纯个人设置，大家可以忽略，看项目需求
Dead Code Stripping 设置为NO
Mach-O Type 设置为 Static Library
Architectures 增加 armv7s

## 手动命令
合并
lipo -create /XXX /XXX -output /XXX
查看架构

## 常见问题
1、制作framework或者lib时，如果使用了category需要在该工程中 other linker flags 添加 -ObjC -all_load
2、图片资源需要打包成Bundle，和Framework共同引入项目中使用
3、新建文件的Target选中Demo工程跟打包脚本的Target

## 其他说明
#### －ObjC
链接器会把静态库中所有的Objective-C类和分类都加载到最后的可执行文件中
#### －all_load
链接器把所有找到的目标文件都加载到可执行文件中，但是千万不要随便使用这个参数.
假如你使用了不止一个静态库文件，然后又使用了这个参数，那么你很有可能会遇到ld: duplicate symbol错误.
因为不同的库文件里面可能会有相同的目标文件，所以建议在遇到-ObjC失效的情况下使用-force_load参数.
#### -force_load
做的事情跟-all_load是一样的，但是-force_load需要指定要进行全部加载的库文件的路径，这样的话，你就只是完全加载了一个库文件，不影响其余库文件.
