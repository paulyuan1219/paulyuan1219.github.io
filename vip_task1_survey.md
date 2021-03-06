# [场景导购系列一：个性化服饰搭配在淘宝搜索的实践](https://yq.aliyun.com/articles/431602?spm=a2c4e.11153959.0.0.48ed6aa6WEsQwT)

过了一遍，还没有细看

# [京东商品搜索架构设计](http://www.cnblogs.com/huangfox/p/5111713.html)
电商搜索系统存在以下特点：
数据量庞大。（上亿级别）
高并发。（日均pv过亿、数十亿）
一条商品数据由商品基本信息、价格、库存、促销、评价等组成，这些数据存储在各自业务系统当中。（多数据源导致构建索引比较麻烦）
召回率要求高。（哪个商家发现搜不到自家的商品肯定要抓狂，哪怕有一个搜不到。）
时效性要求高，价格变动、库存变动、上下架等要求近实时。（更新时间过长虽然不会造成资损，但是会严重影响用户体验）
索引更新量庞大。（上千万级别）
排序！排序！排序！如何把用户最想要的排在前面，提升转化率，是搜索的核心价值。
个性化排序。对用户进行画像，然后抽取特征项参与排序。你对风格、材质、价格、品牌等因素的偏好都会影响排序结果。（千人千面）

关键点解读：
1）搜索分片、副本集
副本集：随着并发量越来越大，单机已不能胜任，可以考虑“横向扩展”（副本集）做负载均衡，提升整个搜索平台的并发能力。
分片：随着数据规模越来越大，单机的内存、计算资源吃紧，造成单次请求响应超时，可以考虑分片，将大索引切分成小索引，从而满足单机的性能。
将分片、副本集综合起来构建分布式搜索引擎，不管以后是搜索量增长还是数据量增长，都可以通过扩展来满足。

2）索引过程（全量索引、增量索引）
全量索引数据准备：上文提到“搜索系统中一条商品数据由商品基础信息、价格、库存、促销、评价等信息组成，这些数据都分布在不同的业务系统中”。为了便于索引处理，对多个系统的数据进行合并，生成商品宽表。然后在数据平台上对数据进行清洗，形成一份待全量索引数据。
全量索引：由于全量数据比较庞大，采用hadoop进行“并行”处理。其实全量索引重点就是分布式索引，简单方式可以根据一个数据切分规则，把数据分解成n块（n对应分片数），由不同的机器同时构建索引。如下图：

3）检索
一个检索请求过来，先到merger，由merger将检索请求分发给各个searcher节点，searcher节点进行检索并返回结果给merger，然后merger进行合并排序，最后返回。
那么这里涉及两次排序，第一次是在searcher里面排序，第二次是在merger做合并排序。（排序后面具体再说）

4）排序
上文提到一次搜索过程存在两次排序：search排序，merge排序。
searcher排序注重文本策略，这里主要包括文本域、价格、销量、好评等“商品综合分”排序。
merger排序根据多个结果集进行合并排序，主要包括：店铺多样性、品牌多样性、战略扶持品牌等业务规则。
各大电商公司的排序都不太一样，也会有“排序白皮书”供卖家进行参考，作为站内排序优化的参考书。
排序是电商搜索引擎的核心！

5）个性化搜索
个性化之前的搜索对于同一个查询，不同用户看到的结果是完全相同的。这可能并不符合所有用户的需求。在商品搜索中，这个问题尤为特出。因为商品搜索的用户可能特别青睐某些品牌、价格、店铺的商品，为了减少用户的筛选成本，需要对搜索结果按照用户进行个性化展示。
个性化的第一步是对用户和商品分别建模，第二步是将模型服务化。有了这两步之后，在用户进行查询时，merger同时调用用户模型服务和在线检索服务，用户模型服务返回用户维度特征，在线检索服务返回商品信息，排序模块运用这两部分数据对结果进行重排序，最后给用户返回个性化结果。

6）扩展搜索范围（Query Processer）
整合搜索用户在使用搜索时，其目的不仅仅是查找商品，还可能查询服务、活动等信息。为了满足这一类需求，首先在Query Processor中增加对应意图的识别。第二步是将服务、活动等一系列垂直搜索整合并服务化。一旦QP识别出这类查询意图，就条用整合服务，将对应的结果返回给用户。

7）其他
缓存设计（分级缓存）
Detail Server（补充展示字段）


# [京东基于大数据技术的个性化电商搜索引擎](http://www.infoq.com/cn/presentations/jingdong-personalized-search-engine-based-on-big-data-technology)
有录像 可以好好看看

0.3Billion query/day 
don't forget cats with less people

行为：最近搜了什么，加入什么购物车
偏好：用户画像
挖掘出来消费性别 >真实性别
实时偏好：3天 长期偏好：半年
偏好要有跨平台能力：pc，手机端，unify
地域建模：细化到小区，不同小区购买力，购买兴趣不同。富人区会买一千块以上的移动电源
兴趣偏好主要针对broad query, 比如“图书，连衣裙”等。在jd图书中，有40%不明确。
偏好来源：来自商品标签。商品有一些扩展属性，如64g,这些可能需要人工输入
主观商品标签：1 抽取优质品论，2 提取核心词和修饰词，比如“送丈母娘”“送老板”。。。并把这些呈献给用户
关联搜索其实是search 和推荐的集合。目前只用在book中，提升明显。搜索出的结果和关联推荐的结果不区分，放在一起呈现给用户看。注意，对用户买过的东西，不能再次推荐，此时要用产品词过滤，不能用类目过滤。
总体而言，对broad query做个性化推荐，如books dress。对于详细具体的query，暂时不做个性化搜索，但是会使用关联推荐等。

# [京东11.11：商品搜索系统架构设计](http://www.infoq.com/cn/articles/jingdong-11-11-commodity-search-system-architecture-design?utm_source=infoq&utm_campaign=user_page&utm_medium=link)

搜索已经成为我们日常不可或缺的应用，很难想象没有了Google、百度等搜索引擎，互联网会变成什么样。京东站内商品搜索对京东，就如同搜索引擎对互联网的关系。他们的共同之处：1. 海量的数据，亿级别的商品量；2. 高并发查询，日PV过亿；3. 请求需要快速响应。这些共同点使商品搜索使用了与大搜索类似的技术架构，将系统分为：1. 离线信息处理系统；2. 索引系统；3. 搜索服务系；4.反馈和排序系统。

同时，商品搜索具有商业属性，与大搜索有一些不同之处：1. 商品数据已经结构化，但散布在商品、库存、价格、促销、仓储等多个系统；2. 召回率要求高，保证每一个正常的商品均能够被搜索到；3. 为保证用户体验，商品信息变更（比如价格、库存的变化）实时性要求高，导致更新量大，每天的更新量为千万级别；4. 较强的个性化需求，由于是一个相对垂直的搜索领域，需要满足用户的个性化搜索意图，比如用户搜索“小说”有的用户希望找言情小说有的人需要找武侠小说有的人希望找到励志小说。另外不同的人消费能力、性别、对配送时间的忍耐程度、对促销的偏好程度以及对属性比如“风格”、“材质”等偏好不同。以上这些需要有比较完善的用户画像系统来提供支持。



# [深度学习在美团点评的应用](https://tech.meituan.com/deeplearning_application.html)
基于深度学习的语义匹配
语义匹配技术，在信息检索、搜索引擎中有着重要的地位，在结果召回、精准排序等环节发挥着重要作用。

传统意义上讲的语义匹配技术，更加注重文字层面的语义吻合程度，我们暂且称之为语言层的语义匹配；而在美团点评这样典型的O2O应用场景下，我们的结果呈现除了和用户表达的语言层语义强相关之外，还和用户意图、用户状态强相关。

用户意图即用户是来干什么的？比如用户在百度上搜索“关内关外”，他的意图可能是想知道关内和关外代表的地理区域范围，“关内”和“关外”被作为两个词进行检索，而在美团上搜索“关内关外”，用户想找的就是“关内关外”这家饭店，“关内关外”被作为一个词来对待。

再说用户状态，一个在北京和另一个在武汉的用户，在百度或淘宝上搜索任何一个词条，可能得到的结果不会差太多；但是在美团这样与地理位置强相关的场景下就会完全不一样。比如我在武汉搜“黄鹤楼”，用户找的可能是景点门票，而在北京搜索“黄鹤楼”，用户找的很可能是一家饭店。

如何结合语言层信息和用户意图、状态来做语义匹配呢？

我们的思路是在短文本外引入部分O2O业务场景特征，融合到所设计的深度学习语义匹配框架中，通过点击/下单数据来指引语义匹配模型的优化方向，最终把训练出的点击相关性模型应用到搜索相关业务中。下图是针对美团点评场景设计的点击相似度框架ClickNet，是比较轻量级的模型，兼顾了效果和性能两方面，能很好地推广到线上应用。

表示层
对Query和商家名分别用语义和业务特征表示，其中语义特征是核心，通过DNN/CNN/RNN/LSTM/GRU方法得到短文本的整体向量表示，另外会引入业务相关特征，比如用户或商家的相关信息，比如用户和商家距离、商家评价等，最终结合起来往上传。

学习层
通过多层全连接和非线性变化后，预测匹配得分，根据得分和Label来调整网络以学习出Query和商家名的点击匹配关系。

在该算法框架上要训练效果很好的语义模型，还需要根据场景做模型调优：首先，我们从训练语料做很多优化，比如考虑样本不均衡、样本重要度、位置Bias等方面问题。其次，在模型参数调优时，考虑不同的优化算法、网络大小层次、超参数的调整等问题。经过模型训练优化，我们的语义匹配模型已经在美团点评平台搜索、广告、酒店、旅游等召回和排序系统中上线，有效提升了访购率/收入/点击率等指标。

小结
深度学习应用在语义匹配上，需要针对业务场景设计合适的算法框架，此外，深度学习算法虽然减少了特征工程工作，但模型调优上难度会增加，因此可以从框架设计、业务语料处理、模型参数调优三方面综合起来考虑，实现一个效果和性能兼优的模型。
