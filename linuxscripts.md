# Linux

    sort -t , -k14,14 -k15,15 -k8,8 540.nohead.csv > 540.nohead.sort.csv
    sort vip_cattree.20171211.csv.col12 | uniq -c > vip_cattree.20171211.csv.col12.uniq
    cut -d, -f 14,15 540.nohead.sort.csv > a
    sed 's/,/       /g' 70.nohead.sortbycol89.col789.csv > 70.nohead.sortbycol89.col789.tab.csv    
    sed -n 1,22p d > d00 # extract l1 to l22
    egrep '^-1,' query_tbcat.csv.new.output_1.tmpnew.autoeval > a2
    egrep '停用' vip_cattree.20171211.csv | wc -l # 计算包含该模式的行数
    
    
    iconv -c -f GB2312 -t utf-8 infile > outfile
    
    
    tar -xvzf *.tar.gz
    conda create --name py36 python=3.6 numpy scipy matplotlib pandas anaconda
    conda create --name py27 python=2.7 numpy scipy matplotlib pandas anaconda
    iconv -c -f GB2312 -t UTF-8 test_query.csv > test_query.csv.new
    iconv -c -f gb2312 -t utf-8 cat1_fabuleimu.csv > cat1_fabuleimu.csv.utf8 # the input is a result from web crawler
    ls -alh

# Python

```
l1 = [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
sorted(l1, key=lambda x:x[2], reverse=True)
```

# Anaconda
[Get hands dirty](https://conda.io/docs/user-guide/overview.html)

The conda command is the primary interface for managing installations of various packages. It can:

- Query and search the Anaconda package index and current Anaconda installation.
- Create new conda environments.
- Install and update packages into existing conda environments.

```
conda install [packagename]
conda --version # check conda version
conda update conda
conda create --name py36 python=3.6 numpy scipy matplotlib pandas statsmodels scikit-learn theano keras
conda install -c conda-forge tensorflow
source activate py27

```

[jupyter中添加conda环境](https://www.cnblogs.com/hgl0417/p/8204221.html)

安装完Anaconda利用conda创建了虚拟环境，但是启动jupyter notebook之后却找不到虚拟环境。

实际上是由于在虚拟环境下缺少kernel.json文件，解决方法如下：

 

首先安装ipykernel：conda install ipykernel

 

在虚拟环境下创建kernel文件：conda install -n 环境名称 ipykernel

 

激活conda环境： source activate 环境名称

 

将环境写入notebook的kernel中

python -m ipykernel install --user --name 环境名称 --display-name "Python (环境名称)"

 

打开notebook服务器：jupyter notebook

浏览器打开对应地址，新建python，就会有对应的环境提示了

 

如果经常需要用jupyter notebook，那么最好在创建虚拟环境的时候便安装好ipykernel，

命令：conda create -n 环境名称 python=3.5 ipykernel

 

删除kernel环境：

jupyter kernelspec remove 环境名称


[jupyter notebook选择conda环境](http://blog.csdn.net/u011606714/article/details/77741324)
