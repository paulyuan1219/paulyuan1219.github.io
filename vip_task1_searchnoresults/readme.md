# Update according to the following memo
20180208与袁娜会议纪要
 
分析了1522数据集上准确率低的原因
- Tail query
- 标准比以前更严格，两轮
- 用的三级类目信息不是最新，与评测用的不一致
- Q->tbcat->vipcat的做法没有充分考虑Q本身的信息
 
确定了下一步工作(春节前)：
- 利用袁娜提供的最新vip类目表
- 采取(Q, tbcat)->vipcat的方式，暂定用简单的语言模型
- 之前7227的数据做training，这次1522数据做testing，目标准确率>=90%
