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

# 以下是具体步骤
1. 根据之前准备的excel表，把d00情况的(query, tb_cat) 放到一个文件中

    cut -f 1,2 d00.concise | sed 's/     /,/' > d00.concise.q_tb





1 袁娜新给了一个vip类目表。使用之前，首先要看一下这个表和之前她给的是否一样。(等等，这样做太慢了，先看一下LM如何应用，效果如何)
写一个工具来看
输入：原始vip类目标
输出：vipcatid, vipcat_fullpath

