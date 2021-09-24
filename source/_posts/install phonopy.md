由于服务器账号上的phonopy有bug：输入

```shell
phonopy-bandplot --gnuplot band.yaml > band.dat
```

后本应该生成含有声子数据的文件band.dat，但是其容量一直为0，于是重新装phonopy



先删除原有程序：

```shell
pip uninstall phonopy
```

在github上下载phonopy的包：https://github.com/phonopy/phonopy

解压在服务器上

然后首先用：

```shell
python setup.py install
```

显示成功后，尝试输入命令 `phonopy`，结果报错

![](F:\blog\source\_posts\picture\install phonopy1.png)

之后删除已安装的phonopy，重新使用命令：

```shell

pip install -e ./
```

结果安装顺利，运行成功