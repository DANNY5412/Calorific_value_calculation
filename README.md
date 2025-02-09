# 热点信息条目热度分析

# 一、目前实现

## 1. 参数设置

```
time_subsection = 20  # 时间间隔数
time_sum = 0.4  # 每个间隔的时间长度
comment_data_location = r'data\test\comment_sum\\'  # 话题路径
title = '曾黎青衣惊艳时刻'  # 话题名称
```

目前程序需要更改所要检测的`话题名称`，并且可以根据所需设置检测的时间区间间隔。由于目前数据集是静态数据集，因此还要设置检测多少个时间间隔。

## 2. 输入信息

输入信息在读取时读取的是已有数据库中的单个话题，话题以excel文档形式存储。需要读取的信息有两部分：1）一个完整话题文件夹，文件夹内每条新闻的评论内容分别用一个表格存储。2）一个excel表格，其中包含话题下所有新闻的评论信息，汇总到一个表格内。

## 3. 输出信息

输出该事件每个时间节点的热度值、热点事件概率到表格中，通知保存热度值、热点事件概率图像。

输出数据结果

![image-20240422175047407](README/image-20240422175047407.png)

输出函数图像结果

![曾黎青衣惊艳时刻_trend](README/%E6%9B%BE%E9%BB%8E%E9%9D%92%E8%A1%A3%E6%83%8A%E8%89%B3%E6%97%B6%E5%88%BB_trend.png)

# 二、 程序使用

## 1. 环境配置

程序运行环境需要python3.8以上，pytorch2.2.0以上。
其他所需软件包：

```
tqdm>=4.64.1
joblib>=1.0.0
requests>=2.25.1
numpy>=1.19.5
torch>=2.0.0
transformers>=4.39.2
pandas~=2.0.3
openpyxl~=3.1.2
cemotion~=2.1.1
setuptools~=69.2.0
```

## 2. 代码运行

现有程序已经封装在了`demo.py`当中，可以直接运行使用。

程序中用到了以下超参数和参数：

```
###超参数（可自定义修改
time_subsection = 10  # 时间间隔数
time_sum = 1  # 每个间隔的时间长度
title = '单亲妈妈网恋遇假军官被骗15万'  # 话题名称

###参数（最好不修改）
hotspots_boundary = 10  # 热度概率计算调整值（上线60）
log_total = 10  # 总评论数计算公式log值
log_maxH = 10  # 最多小时评论数计算公式log值
par_U_dc = 1  # 总评论数参数
par_U_c = 1  # 最多小时评论数参数
par_N = 5  # 媒体关注度除法分母参数（不能为零）

```

其中超参数可以根据所要检测的话题和时间尺度进行修改，参数为调试过程中较为合适的比例参数，已经较为合适不用修改。

在演示demo中会将计算结果保存到表格并输出图像。



# 最新更改

1. 修改话题敏感度匹配多敏感词库求平均值的问题，改为按比例压缩。

2. 修改了时间分段的超参数，现有热度计算值不在跟切分时间间隔直接相关，有专门参数`time_sum`管理计算使用间隔长度
3. 修正观众热度值增长率计算公式，避免基数较大情况下增长率不增反减情况。
