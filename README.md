# Online Retail Data Analysis

基于 UCI Online Retail 真实零售交易数据，完成从原始数据清洗、SQL 查询、Python 分析、RFM 客户分群到 Tableau 可视化看板的完整数据分析项目。

## 项目目标

围绕零售业务回答以下问题：

- 整体销售规模和取消/退货情况如何？
- 月度销售趋势是否存在明显波动？
- 哪些商品贡献了主要净销售额？
- 客户是否存在明显的价值分层？
- 高价值客户对整体销售的贡献有多大？
- 如何基于 RFM 分群制定差异化客户运营策略？

## 数据集

数据来源：UCI Online Retail 数据集。

原始数据时间范围：2010-12-01 至 2011-12-09。

原始数据共 **541,909** 条交易明细，主要字段包括：

- `InvoiceNo`：订单编号
- `StockCode`：商品编号
- `Description`：商品名称
- `Quantity`：商品数量
- `InvoiceDate`：交易时间
- `UnitPrice`：商品单价
- `CustomerID`：客户编号
- `Country`：国家/地区

## 数据清洗

使用 SQL 与 Python 对原始交易数据进行检查和清洗，主要规则包括：

- 去除 `Quantity <= 0` 的异常/退货记录
- 去除 `UnitPrice <= 0` 的异常价格记录
- 去除 `InvoiceNo` 以 `C` 开头的取消订单
- 保留原始表 `retail`
- 新建清洗表 `retail_clean`

清洗结果：

- 原始记录：**541,909**
- 清洗后记录：**524,878**
- 清洗后异常数量：**0**
- 清洗后异常价格：**0**
- 清洗后取消订单记录：**0**

## SQL 分析

使用 SQLite 完成主要业务查询，包括：

- 月度销售额、订单量与客单价
- 月度环比变化
- 国家/地区销售贡献
- Top 商品销售表现
- Top 客户销售表现
- 取消订单与异常交易检查
- 匿名客户销售占比分析

数据库文件：`database/online_retail.db`

其中包含：

- `retail`
- `retail_clean`

## Python 分析

主要使用：

- Pandas：数据处理与聚合
- NumPy：数值计算
- Matplotlib：数据可视化
- SQLite3：数据库连接与查询

分析内容包括：

- 销售趋势分析
- 取消金额率分析
- 商品净销售额分析
- 客户复购分析
- 客户价值集中度分析
- RFM 客户分群

## 核心业务指标

基于有效商品交易计算：

- Gross Sales：约 **£10.25M**
- Net Sales：约 **£9.77M**
- Cancelled / Returned Sales：约 **£479K**
- Cancellation Rate：约 **4.67%**

客户分析中：

- 有效客户数约 **4.3K**
- 复购客户数约 **2.8K**
- 复购率约 **65.27%**
- Top 10% 客户贡献约 **60.12%** 的客户净销售额

> 注：RFM 分析仅针对可识别 `CustomerID` 的客户，因此其客户净销售额口径与全部商品交易净销售额不同。

## RFM 客户分群

根据：

- **R（Recency）**：最近一次购买距分析时点的天数
- **F（Frequency）**：购买频次
- **M（Monetary）**：客户累计净消费金额

将客户划分为：

- High Value
- Loyal
- At Risk
- Regular
- Potential
- Hibernating
- New

关键结果：

- High Value 客户占比约 **20.81%**
- High Value 客户贡献约 **65.71%** 的客户净销售额
- High Value 客户平均价值约 **£6.04K**

业务建议：

- High Value：重点维护，提升留存和复购
- Loyal：通过会员权益和交叉销售提升客单价
- At Risk：重点召回，减少高价值客户流失
- Potential：通过优惠与推荐促进复购
- Hibernating：低成本唤醒或减少资源投入
- New：加强首购后的二次转化

## Tableau Dashboard

项目制作了两页 Tableau Dashboard。

### 1. Online Retail Sales Overview

<img width="1440" height="900" alt="截屏2026-08-04 19 35 51" src="https://github.com/user-attachments/assets/805e1aaa-e288-406f-803a-e9f438f16e78" />

包含：

- Gross Sales
- Net Sales
- Cancelled Sales
- Cancellation Rate
- Monthly Gross Sales vs Net Sales
- Monthly Cancellation Amount Rate
- Top 10 Products by Net Sales

### 2. Customer & RFM Analysis

包含：

- Customer Share vs Sales Share by RFM Segment
- Net Sales by RFM Segment
- Average Customer Value by RFM Segment
- RFM 分群联动筛选

Tableau 文件：`tableau/Online_Retail_Data_Analysis.twbx`

## 项目结构

```text
online-retail-data-analysis/
│
├── README.md
│
├── notebooks/
│   └── online_retail_analysis.ipynb
│
├── data/
│   ├── monthly_summary.csv
│   ├── product_net_sales.csv
│   ├── retail_transactions.csv
│   └── rfm_segments.csv
│
├── database/
│   └── online_retail.db
│
├── tableau/
│   └── Online_Retail_Data_Analysis.twbx
│
└── images/
    ├── 01_sales_overview.png
    └── 02_rfm_analysis.png
```

## 技术栈

- Excel
- SQL / SQLite
- Python
- Pandas
- NumPy
- Matplotlib
- Tableau
- Git / GitHub

## 项目亮点

- 使用真实零售交易数据完成端到端数据分析流程
- 将 SQL、Python、RFM 和 Tableau 串联为完整分析链路
- 同时覆盖数据清洗、业务指标、客户分层和可视化展示
- 对高价值客户识别、客户集中度和复购行为给出可落地的运营建议
- Tableau Dashboard 支持 RFM 分群联动筛选，便于交互式业务分析

## 运行方式

1. 打开 `notebooks/online_retail_analysis.ipynb`
2. 准备原始 `Online Retail.xlsx`
3. 按顺序运行数据清洗、SQL 查询、Python 分析和 RFM 分群代码
4. 输出分析 CSV 文件
5. 使用 `tableau/Online_Retail_Data_Analysis.twbx` 查看可视化结果

## 说明

本项目用于数据分析学习、作品集展示与求职项目实践。
