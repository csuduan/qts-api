# Python版CTPAPI

## 直接使用

openctp提供了pip install和文件下载两种方法安装CTPAPI-Python库，可以直接使用，均支持6.3.15~6.7.2各个版本。

### pip install方式

```bash
pip install openctp-ctp==6.3.15.* -i https://pypi.tuna.tsinghua.edu.cn/simple --trusted-host=pypi.tuna.tsinghua.edu.cn
```

### 文件下载方式

[CTPAPI-Python接口下载](http://openctp.cn/CTPAPI-Python.html)

## 自己编译

CTPAPI-Python使用Swig技术开发，可以自己按以下步骤编译，需要安装swig等组件，详细攻略见：[CTPAPI-Python开发攻略](https://zhuanlan.zhihu.com/p/688672132)。

本仓库选用的是CTPAPI-6.3.15，如需编译其它版本，请下载相应的CTPAPI文件覆盖对应目录下的CTPAPI文件。

### Windows编译

- 安装VirtualStudio、Swig、Python3、boost、cmake，boost库用到的是locale库，用来转换字符集。
- 设置BOOST_INCLUDE、BOOST_LIB环境变量分别指向相应库的头文件及库目录，如E:\boost_1_73_0、E:\boost_1_73_0\stage\lib。
- 设置PYTHON_INCLUDE、PYTHON_LIB环境变量分别指向相应库的头文件及库目录，如C:\Program Files\Python312\include、C:\Program Files\Python312\libs。

#### 编译

```
cd CTPAPI
mkdir build
cd build
cmake -A x64 ..
cmake --build . --config Release
```

#### 使用
编译成功后，将生成的文件连同CTPAPI的dll（thosttraderapi.dll、thostmduserapi.dll）拷贝到你的程序运行目录下即可：

- thosttraderapi.py
- thostmduserapi.py
- _thostmduserapi.pyd
- _thosttraderapi.pyd

### Linux编译
linux环境中需要安装cmake,swig,boost

设置环境变量：  
export PYTHON_INCLUDE=/opt/app/miniconda3/include/python3.13
export PYTHON_LIB=/opt/app/miniconda3/lib

linux库规范名称需要以lib开头，进行重命名：
```
mv thostmduserapi_se.so libthostmduserapi_se.so
mv thosttraderapi_se.so libthosttraderapi_se.so
```

#### 编译

```
cd CTPAPI
mkdir build
cd build
cmake ..
make
```

#### 使用
编译成功后，将生成的文件连同CTPAPI的so文件（thosttraderapi.so、thostmduserapi.so）拷贝到你的程序运行目录下即可：
- thosttraderapi.py
- thostmduserapi.py
- _thostmduserapi.so
- _thosttraderapi.so
- libthosttraderapi.so
- libthostmduserapi.so
融航系统需要额外文件：
- librohonbase.so
- libLinuxDataCollect.so
并执行：
```bash
ln -s libthosttraderapi_se.so thosttraderapi_se_6.7.2.so
patchelf --set-rpath '$ORIGIN' libthosttraderapi_se.so
```
  
