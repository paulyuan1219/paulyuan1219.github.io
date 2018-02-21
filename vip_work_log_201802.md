# 工作日志

## 20180212
上午重装了电脑以及备份，到下午三点才基本搞定

根据袁娜所说，每次用的vip的类目信息都不一样，所以我要先看一下之前的文件，看看到底有几个版本的vipcattree
Under VIPShop/Task1, create a new folder "redo", 意味着从这里开始，需要把之前的实验重新做一下，外加数据分析。
从今以后，所有东西都在redo目录下

data/raw/ 这里放置所有袁娜给我的数据，最原始的数据






Colons can be used to align columns.

| Table        | #line           | Remark  |
| ------------- |:-------------:| :-----|
| test.query.7227.utf8 <br /> (原来的Copy of UV大于10无结果词11.20-11.27(2)) | 7227      | 测试数据（只有query） 只有一列，每一行是一个query，无表头 | 
| test.query.7227.utf8.withtaobaolist.csv <br/> UV大于10无结果词11.20-11.27-宝贝发布类目建议12.04      | 7228      |   有表头，前四列为(c_type, sug_test,uv,pv)。第一列总是搜索为空，第二列是搜索无结果词，sort by uv pv。这里的Query与上一个文件里面的一一对应。<br /> 对每个Query，利用淘宝卖家中心发布宝贝的建议，追加了淘宝所推荐的所有类目。这事实上是一个类目列表，但是我们只有rank信息，没有具体权重信息 |
| train.query.150k.withviplist.csv <br /> 12.5搜索识别唯品主分类.xlsx | 153646      |    训练数据，有表头。(queryid, query, vipcat1, vipcat2...  <br /> 其中的vipcatid见下表|
| vip_cattree.20171211.csv | 4409 | 有表头。每一行含有一个三级分类 如下 271,鞋,272,男式鞋,276,男靴 注意，每个catid都是唯一的 <br /> 从3868行开始就是停用分类，所以实际有效的三级分类数量有3866个 含有停用的分类有542个|
| train.query.150k.withtaobaolist.csv <br /> 原12.5搜索识别唯品主分类_淘宝卖家宝贝发布类目建议_result_2_15w.v2.csv | 153646 | 以上训练数据的淘宝版本。对每一行的query，去淘宝找出类目推荐 <br /> 羽绒服 女装/女士精品>>羽绒服 户外/登山/野营/旅行用品>>户外服装>>羽绒服>>羽绒衣 男装>>羽绒服|

Remark
1. 注意，最开始的7227文件在mac中打开是乱码，需要用以下工具转换编码
```
iconv -c -f gb2312 -t utf-8 test.query.7227 > test.query.7227.utf8
```
2. 注意，12.5搜索识别唯品主分类_淘宝卖家宝贝发布类目建议_result_2_15w.v2.csv 用excel和shell打开都是乱码，需要用以下工具转换编码
```
iconv -c -f gb2312 -t utf-8 12.5搜索识别唯品主分类_淘宝卖家宝贝发布类目建议_result_2_15w.v2.csv > train.query.150k.withtaobaolist.csv
```
转换后，excel仍然是乱码，但是shell下打开正常


## 20180213
今天继续，把上面的表补充完整

1. 首先分析一下scheme1.concise-人工验证12.27-袁伟复查.xlsx 
这里用的vipcattree就是最原始的版本，对2134个query，对top5 的vipcat做了标注，
从这里，我们可以推导出一个(query, vipcat, label)的三元组列表，这个可以作为我们的baseline。利用excel本身的sort by color的功能，可以生成这个三元组。注意，把黄色cell放在top



## 20180214
对于表格，直接在markdown里面太慢，先在excel里面做好，再放进来吧，快一些。




注意，以后所有的人工验证标注都是在一些query上来的，需要把这些query整理一些，并且放入raw目录下。

在redo/eval1目录下放置我的第一次结果和袁娜的第一次feedback

| Table        | #line           | Remark  |
| ------------- |:-------------:| :-----|
| query_tbcat.csv | 7227 | test.query.7227.utf8.withtaobaolist.csv去掉表头就是这个文件 |
| scheme1.concise | 9737 | 20171222 mailed to yuanna <br/> 用shheme1生成的(tbcat, vipcat) mapping |
| query_tbcat.csv.scheme1_1 | 6091 | 20171222 mailed to yuanna <br/> 对每一个Query，选择top1的taobao_cat，然后去scheme1.concise里面找相对应的vip_cat，这样，可以为6091个query找到vip_cat |
| scheme1.concise-人工验证12.27.xlsx | 2134 | 20171227 received <br /> 总共6091个query中，处理了2134个，正确706，不正确1428。详细见内 <br /> 如果只看top1的话，大约 1400 正确，准确率大约三分之二 |




最早袁娜提供了一个vip cattree。然后，对于7227个query上的人工标注，



There must be at least 3 dashes separating each header cell.
The outer pipes (|) are optional, and you don't need to make the 
raw Markdown line up prettily. You can also use inline Markdown.

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3



