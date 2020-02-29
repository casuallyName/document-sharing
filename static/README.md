# 在启动visdom服务时遇到如下情况，长时间无反应
```powershell
Microsoft Windows [版本 10.0.18363.657]
(c) 2019 Microsoft Corporation。保留所有权利。

C:\Users\UserName>python -m visdom.server
D:\Anaconda3\lib\site-packages\visdom\server.py:39: DeprecationWarning: zmq.eventloop.ioloop is deprecated in pyzmq 17. pyzmq now works with default tornado and asyncio eventloops.
  ioloop.install()  # Needs to happen before any tornado imports!
Checking for scripts.
Downloading scripts, this may take a little while
```
# 解决办法

 1. 找到visdom模块安装位置
 	其位置为`python`或`anaconda`安装目录下`\Lib\site-packages\visdon`
  ```
  ├─static
│  ├─css
│  ├─fonts
│  └─js
├─__pycache__
├─__init__.py
├─__init__.pyi
├─py.typed
├─server.py
└─VERSION
  ```
 	可在`python`或`anaconda`安装目录下搜索找到
 2. 修改文件`server.py`
 修改函数`download_scripts_and_run`，将`download_scripts()`注释掉
 该函数位于全篇末尾，1917行


```python
def download_scripts_and_run():
    # download_scripts()
    main()


if __name__ == "__main__":
    download_scripts_and_run()
```

 3. 替换文件
    将文件覆盖到`\visdon\static`文件夹下






至此，该问题解决完毕。
使用命令`python -m visdom.server`开启服务

```powershell
Microsoft Windows [版本 10.0.18363.657]
(c) 2019 Microsoft Corporation。保留所有权利。

C:\Users\UserName>python -m visdom.server
D:\Anaconda3\lib\site-packages\visdom\server.py:39: DeprecationWarning: zmq.eventloop.ioloop is deprecated in pyzmq 17. pyzmq now works with default tornado and asyncio eventloops.
  ioloop.install()  # Needs to happen before any tornado imports!
It's Alive!
INFO:root:Application Started
You can navigate to http://localhost:8097
```
