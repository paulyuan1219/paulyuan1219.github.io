# [场景导购系列一：个性化服饰搭配在淘宝搜索的实践](https://yq.aliyun.com/articles/431602?spm=a2c4e.11153959.0.0.48ed6aa6WEsQwT)

过了一遍，还没有细看



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

