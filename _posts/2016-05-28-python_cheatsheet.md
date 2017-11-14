---
layout: post
title:  "python cheatsheet"
date:   2016-05-28 14:13:36 +0800
categories: python 
---
## format json


### python 中文输入， 注意是utf8
```
#encoding:utf8
#encoding=utf8
#-*-          注意，必须加在文件头部， 默认参数：自右向左
```


```shell
echo '{"foo": "lorem", "bar": "ipsum"}' | python -m json.tool
```
python -m json.tool my_json.json

alias prettyjson='python -m json.tool'

### reference

* http://github.com/ddopson/underscore-cli
* http://stackoverflow.com/questions/352098/how-can-i-pretty-print-json
* https://stedolan.github.io/jq/

## point
```
str.replace(old, new[, max])
# 删除非空目录
import shutil.rmtree
shutil.rmtree(path)
```
列出制定目录下的文件
```
os.listdir("dirname")
```
or
```
import glob
glob.glob("xx/*.txt")
```
计算两个数组的差集
```
>>> set([1,2,3,4]) - set([2,5])
set([1, 3, 4])
>>> set([2,5]) - set([1,2,3,4])
set([5])
```

### 判断元素是否在列表内
```python
theList = ['a','b','c']
if 'a' in theList:
    print 'a in the list'

if 'd' not in theList:
    print 'd is not in the list'
```

### 获取一字符串的长度用`len`函数，包括其他跟长度有关的都是这个函数
```python
array = [0,1,2,3,4,5]
print len(array)
```
6

### 返回元素在列表中出现的次数
list.count(obj)


### scrpy  connection refused 111
```
Mission 1: Scrapy will send a user gent with 'bot' in it. Sites might block based on user agent also.

Try over-riding USER_AGENT in settings.py

Eg: USER_AGENT = 'Mozilla/5.0 (X11; Linux x86_64; rv:7.0.1) Gecko/20100101 Firefox/7.7'

Mission 2: Try giving a delay between request, to spoof that a human is sending the request.

DOWNLOAD_DELAY = 0.25
Mission 3: If nothing works, install wireshark and see the difference in request header (or) post data while scrapy sends and when your browser sends.
```

### 取出list 的最后一个元素
listA[-1]

### i++ 不支持

Python doesn't support ++, but you can do:

number += 1

refer: https://mail.python.org/pipermail/python-list/2002-July/131960.html

### scrapy 分页抓取
```python
def parse(self, response):
       items = []
       validurls = []
       newurls = response.xpath("//div[@id='selectedgenre']/ul[@class='list paginate']/li/a[@class='paginate-more']/@href").extract()
       for url in newurls:
           validurls.append(url)
       # //循环抓取
       items.extend([self.make_requests_from_url(url).replace(callback=self.parse) for url in list(set(validurls))])
       iTunes = ItunesItem()
       iTunes['url'] = response.xpath("//div[@id='selectedcontent']/div[@class='column first']/ul/li/a/@href").extract()
       iTunes['title'] = response.xpath("//div[@id='selectedcontent']/div[@class='column first']/ul/li/a/text()").extract()
       iTunes['create_time'] = int(time.time())
       items.append(iTunes)
       return items
```

### yeild
http://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python

### protobuf 实践

#### protobuf 有异常， google.protobuf not found
```
生成pb.py文件有问题
可能是由于库文件版本不正确。
python setup.py build
python setup.py test
python setup.py install (as root)
```

#### repeated 赋值语法
方法一[官方写法]：
```python
li = garden_pb2.GardenListItem()

for i in range(2):
    it = li.item.add()
    it.district = 'aa'
    it.garden_name = 'aa'
    it.area = 'aaa-'+str(i)
```

方法二：
```python
li = garden_pb2.GardenListItem()

for i in range(2):
    it = garden_pb2.GardenItem()
    it.district = 'aa'
    it.garden_name = 'aa'
    it.area = 'aaa-'+str(i)
    li.item.extend([it])
```

### parseFromString
```python
file = open('../../pb_output_luan', 'rb')
li = garden_pb2.GardenListItem()
li.ParseFromString(file.read())
print li.item[0].garden_name
```


#### encode decode must be is unicode, especially chinese
对于两个相同的message 在使用C++或者其他语言encode后的，在decode后对其进行赋值给一个
protobuf field的字段的时候，需要注意类型是否是unicode
it.district = u'深圳'

#### notice
export PYTHONPATH=/usr/lib/python2.7/site-packages/protobuf-2.5.0-py2.7.egg:/usr/lib/python2.7/site-packages/setuptools-19.6.1-py2.7.egg


protoc -I=. --python_out=/data1/python_project/anjuke/anjuke/ garden.proto

python path
http://stackoverflow.com/questions/19917492/how-to-use-pythonpath

pip vs easy_install
http://python-packaging-user-guide.readthedocs.org/en/latest/pip_easy_install/

#### exception

1. It's used for raising your own errors.
```
if something:
    raise Exception('My error!')
```python

2. The second is to reraise the current exception in an exception handler, so that it can be handled further up the call stack.
```python
try:
  generate_exception()
except SomeException, e:
  if not can_handle(e):
    raise
  handle_exception(e)
```
> http://www.cnblogs.com/rubylouvre/archive/2011/06/22/2086644.html



## DSP部署问题

### 代码变更
1. 生成独立的密钥
2. 域名变更
3. CDN资源使用
4. mysql 及相关业务的授权帐号及密码

### 业务变更
1. ID分段， 使用同一套ADX出口
2. 充值接口，暂时是手动充值。
3. adx 的消耗区分
