# pyRemoteControl
图形界面远程控制<br\>
qzane@live.com
# 特点

## 三种模式，适用于任何网络
### 直连模式
被控端具有公网IP，使用IP地址直连

### 被动模式
控制端具有公网IP，监听指定端口，等待被控端连接

### 中继模式
控制端和被控端均无公网IP，使用中继服务器，仍然可以连接

## 清晰度动态调整，网速自适应


## Fernet加密算法，阻止中间人攻击
提供二进制加密接口，可以方便的采用其它加密方式

# 操作截图

![开始界面](https://cloud.githubusercontent.com/assets/8392481/12008342/5f363c0c-ac70-11e5-8bd2-d6d177529c69.png)
开始界面
![模式选择](https://cloud.githubusercontent.com/assets/8392481/12008345/5f5895a4-ac70-11e5-9407-2d8454cf0017.png)
模式选择
![网络类型选择](https://cloud.githubusercontent.com/assets/8392481/12008343/5f420348-ac70-11e5-911c-118882393819.png)
网络类型选择
![远程桌面](https://cloud.githubusercontent.com/assets/8392481/12008346/5f59b48e-ac70-11e5-9ddb-41d4a14f841d.png)
远程桌面
![右键](https://cloud.githubusercontent.com/assets/8392481/12008344/5f4279b8-ac70-11e5-951d-874049869ea0.png)
右键
![拖拽](https://cloud.githubusercontent.com/assets/8392481/12008347/5f59c2f8-ac70-11e5-9482-48a1f043cef1.png)
拖拽
![危险操作](https://cloud.githubusercontent.com/assets/8392481/12008348/5f727f6e-ac70-11e5-8d6c-254dffdc2d52.png)
危险操作
![关机](https://cloud.githubusercontent.com/assets/8392481/12008349/5f73985e-ac70-11e5-8cb4-dc768f4f8f8d.png)
关机

# 代码说明

## net.py
* encode_byte,decode_byte: 加密功能的接口，输入输出均为二进制串，默认采用Fernet加密算法
* Net() 类为threading.Thread的继承类，在新线程提供网络通信。线程间的数据交换采用两个Queue队列实现。网络部分使用socket的TCP实现。


## RemoteControl.py
* 使用上述Net模块，通过应用层协议进行网络连接
* Remote: 控制类，包括了主控端以及被控端。
* Remote.contr: 主控端程序，包括远程桌面图像的显示以及鼠标控制命令的发送
* Remote.b_contr: 被控端程序，包括桌面截图、图像压缩以及鼠标控制的功能


## 网络协议说明
1. 应用层:<br\>
    格式: |type|data|<br\>
    其中type为3字节的类型标记，data为任意长度的二进制数据<br\>
    功能: 把不同类型的数据统一为二进制串<br\>
2. 表示层:<br\>
    格式: |--sizebegin|SIZE|sizeend|DATA|dataend--|<br\>
    其中SIZE为data长度，使用ascii编码，DATA为应用层数据经过加密后的数据<br\>
    功能: 加密数据，对数据合法性检测，阻止中间人攻击<br\> 
    
# 二进制文件下载
[64位Windows版](https://github.com/qzane/pyRemoteControl/releases)

需要其它版本或报告Bug请直接Email联系作者
