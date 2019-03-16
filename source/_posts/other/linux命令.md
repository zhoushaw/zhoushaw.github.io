## 文件常见操作



创建目录                        make directory                            mkdir file1
删除                                remove                                         rm -rf file1
移动 / 重命名                move                                             mv file2 file3 
复制                                copy                                              cp
罗列                                list                                                  ls
链接                                link                                                 ln *

## 显示系统的隐藏文件方法：

> 在终端上输入：

defaults write com.apple.finder AppleShowAllFiles TRUE; killall Finder

>即为显示隐藏文件:

如果不要显示系统的这些隐藏文件，修改后面的true为false就好：
defaults write com.apple.finder AppleShowAllFiles FALSE; killall Finder


前后端统一使用Base64 -> AES (key>:keyname, iv:ivnum) -> gzip的方式来，进行加密、解密。来确保数据安全

ifconfig ip地址查询

一、使用新的端口:
  1.aides dev --port 8800，把-p后面的8800改成您要自定义的端口号

二、关闭被占用的端口:
  1.查看使用8800端口的进程方法：lsof -i :8800
  2.关闭使用某端口的进程方法：kill -9 PID，注：PID是进程ID

