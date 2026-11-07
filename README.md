# A股量化研究项目集

本仓库是个人量化研究项目的导航页。各项目使用独立仓库管理代码、研究文档、结果与提交历史；本仓库不保存原始数据、券商研报或项目实现代码。

## 研究路线

| 序号 | 项目 | 状态 | 仓库 |
|---|---|---|---|
| 01 | SUE、PEAD事件因子与反转策略复现 | 已完成 | [a-share-sue-pead-replication](https://github.com/truematon94-svg/a-share-sue-pead-replication) |
| 02 | A股日频量价选股因子复现（多因子、单因子测试） | 已完成 | [a-share-daily-price-volume-factor-replication](https://github.com/truematon94-svg/a-share-daily-price-volume-factor-replication) |
| 03 | 机器学习股票收益预测 | 计划中 | 仓库将在项目启动时建立 |
| 04 | 多因子Alpha组合与策略回测 | 计划中 | 仓库将在项目启动时建立 |

## 已完成项目

### 01. SUE、PEAD事件因子与反转策略复现

基于财通证券《在下跌中寻找惊喜，业绩超预期与反转因子的融合》，在聚宽环境中完成：

- SUE1、SUE2、SUE3因子构建与RankIC检验；
- PEAD效应及反转因子的双变量分组；
- 月频多头策略、交易成本与基准对照；
- 2021年至2025年样本外检验；
- 对数据口径、实现差异和因子衰减进行解释。

项目仓库：[a-share-sue-pead-replication](https://github.com/truematon94-svg/a-share-sue-pead-replication)

### 02. A股日频量价选股因子复现

基于华泰证券《华泰单因子测试之动量类因子》，使用聚宽日频数据完成：

- 构建2005年至2016年全A股月频研究面板，覆盖140个截面、2793只股票；
- 复现简单收益、换手率加权及指数衰减加权动量/反转因子；
- 完成行业与市值中性化、IC/IR、WLS回归和五组/十组分层检验；
- 对照原研报关键指标，`return_1m` 的IR为0.637（原文0.63），五组多空年化超额为23.18%（原文26.18%）；
- 完成因子相关性、最大化IC_IR合成、纯多头组合与交易成本回测；
- 在2017年至2024年进行样本外检验，识别短期反转因子的系统性衰减，并记录优化尝试仍无法稳定取得超额收益的结果。

项目仓库：[a-share-daily-price-volume-factor-replication](https://github.com/truematon94-svg/a-share-daily-price-volume-factor-replication)

## 研究原则

- 严格区分研报复现、自主扩展和原创研究；
- 明确样本区间、股票池、数据可得时点与交易成本；
- 优先检查未来函数、幸存者偏差和数据泄露；
- 同时报告成功结果、复现偏差和样本外失效；
- 原始数据、研报原件和授权材料仅保存在本地。

## 主要工具

Python、pandas、NumPy、SciPy、Matplotlib、JoinQuant、Git/GitHub。

