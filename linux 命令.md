# 1、查询文件占用空间

~~~
du -sh * | sort -n
~~~

# 2、将 a 文件夹的内容（除 models）复制到 b文件夹

```python
cd a
cp -r `ls | grep -v models | xargs` ../b
```

# 3、同时open多个文件

zip 很好用

```python
with open('file1') as f1, open('file2') as f2, open('file3') as f3:
    for i,j,k in zip(f1.readlines(),f2.readlines(),f3.readlines())
```

# 4、py文件中运行指令

```python
import subprocess
subprocess.run(['python','./路径/a.py '--test_dir={}'.format(test_name)])
```

## 5、python 文件 设置argument

~~~python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument('--output_dir',help = 'output data path')
args = parser.parse_args()
output_path = args.output_dir
~~~

#  6、debug: UnicodeEncodeError: 'ascii' codec can't encode 

UnicodeEncodeError: 'ascii' codec can't encode character '\u5c9b' in position 1: ordinal not in range(128)

~~~python
系统编码
>>> import sys
>>> sys.getdefaultencoding()
'utf-8'

输出编码
>>> sys.stdout.encoding
'ANSI_X3.4-1968'

解决方法
运行程序的时候加上：
PYTHONIOENCODING=utf-8 python code.py

重新定义输出标准
import codecs
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach())
sys.stdout = io.TextIOWrapper(sys.stdout.buffer,encoding='utf-8')

locale
locale -a
apt-get -y install language-pack-zh-hans
参考详细解答 https://blog.csdn.net/j___t/article/details/97705231
    
vim ~/.bashrc
增加 export LC_ALL = zh_CN.utf8
~~~

# 7、pip安装pytorch 

注意cuda 版本，torch版本、python版本 对应，可去pytorch官网查看

~~~python
pip3 install http://download.pytorch.org/whl/cu80/torch-0.4.1-cp35-cp35m-linux_x86_64.whl
~~~



# 8、列表生成式双层循环

~~~python
a_list=[[1,2],[3,4],[5,6]]

b=[j for i in a_list for j in i]#注意两个for的顺序
~~~

# 9、查看cuda，cudnn版本

~~~
cat /usr/local/cuda/version.txt
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
~~~

# 10、pip 清华源 安装库

 ~~~python
pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple nltk
 ~~~

# 11、pickle数据存储

~~~python
#写文件
import pickle
with open('D:/tmp.pkl', 'w') as f:
     pickle.dump(data, f)
#读文件
import pickle
with open('D:/tmp.pkl', 'r') as f:
     data = pickle.load(f)
~~~

# 12、pandas 

## csv追加存储

~~~python
        file_name = "eval_log.csv"
        if os.path.exists(file_name):
            new_data.to_csv(file_name, index=False, mode="a", header=False, encoding="utf-8")
        else:
            new_data.to_csv(file_name, index=False, encoding="utf-8")
~~~






