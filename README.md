# A股量化研究项目集

本仓库是个人量化研究项目的导航页。各项目使用独立仓库管理代码、研究文档、结果与提交历史；本仓库不保存原始数据、券商研报或项目实现代码。

## 研究路线

| 序号 | 项目 | 状态 | 仓库 |
|---|---|---|---|
| 01 | SUE、PEAD事件因子与反转策略复现 | 已完成 | [a-share-sue-pead-replication](https://github.com/truematon94-svg/a-share-sue-pead-replication) |
| 02 | A股日频量价选股因子复现与策略优化 | 已完成 | [a-share-daily-price-volume-factor-replication](https://github.com/truematon94-svg/a-share-daily-price-volume-factor-replication) |
| 03 | 市场感知与多股票关联的机器学习选股策略 | 已完成 | [a-share-ml-return-prediction](https://github.com/truematon94-svg/a-share-ml-return-prediction) |
| 04 | 沪深300多因子 Alpha 研究与约束型指数增强 | 已完成 | [csi300-multifactor-alpha-enhancement](https://github.com/truematon94-svg/csi300-multifactor-alpha-enhancement) |
| 05 | 自主Alpha因子挖掘与持续性验证 | 持续进行中 | 私有开发仓库 |
| 06 | 订单簿微观结构驱动的高频交易策略 | 计划中 | 暂不开设独立仓库 |
| 07 | 波动率曲面与衍生品相对价值策略 | 计划中 | 暂不开设独立仓库 |

## 已完成项目

### 01. SUE、PEAD事件因子与反转策略复现

基于财通证券《在下跌中寻找惊喜，业绩超预期与反转因子的融合》，在聚宽环境中完成：

- SUE1、SUE2、SUE3因子构建与RankIC检验；
- PEAD效应及反转因子的双变量分组；
- 月频多头策略、交易成本与基准对照；
- 2021年至2025年样本外检验；
- 对数据口径、实现差异和因子衰减进行解释。

项目仓库：[a-share-sue-pead-replication](https://github.com/truematon94-svg/a-share-sue-pead-replication)

### 02. A股日频量价选股因子复现与策略优化

基于华泰证券《华泰单因子测试之动量类因子》，使用聚宽日频数据完成：

- 构建2005年至2016年全A股月频研究面板，覆盖140个截面、2793只股票；
- 复现简单收益、换手率加权及指数衰减加权动量/反转因子；
- 完成行业与市值中性化、IC/IR、WLS回归和五组/十组分层检验；
- 对照原研报关键指标，`return_1m` 的IR为0.637（原文0.63），五组多空年化超额为23.18%（原文26.18%）；
- 完成因子相关性、最大化IC_IR合成、纯多头组合与交易成本回测；
- 在2017年至2024年进行样本外检验，识别短期反转因子的系统性衰减；通过“中证800股票池 + 反转转动量”优化，使策略年化收益由-4.05%提升至+1.08%，改善5.13个百分点并由负转正。

项目仓库：[a-share-daily-price-volume-factor-replication](https://github.com/truematon94-svg/a-share-daily-price-volume-factor-replication)

### 03. 市场感知与多股票关联的机器学习选股策略

参考 AAAI 2024 的 MASTER（Market-Guided Stock Transformer），在自建的A股时点正确数据上完成从预测研究到真实交易验证的完整链路：

- 使用统一信息集公平比较 OLS、Ridge、LightGBM、XGBoost、Random Forest、MLP、Transformer 和 MASTER 八类模型；
- 通过三随机种子、MASTER结构消融和特征组消融，检验市场门控、股票间动态关系及项目二量价因子的边际贡献；
- 使用扩展窗口滚动训练、RankICIR、Newey-West日度配对检验与市场状态分段，识别模型增量的稳定性和适用阶段；
- 严格分离论文对齐回测与真实可执行回测，纳入次日开盘成交、停牌涨跌停、交易成本和换手约束；
- 在2022年底冻结全部模型与组合规则，仅开启一次2023—2025锁箱，并在聚宽使用相同Top-30、5日调仓规则验证；
- 固定切分中 Random Forest 的三种子 Test RankIC 为 `0.0535 ± 0.0026`，MASTER 为神经网络中最好，Test RankIC 为 `0.0457 ± 0.0034`；
- 锁箱期内 MASTER 的平均日度 RankIC 略高但差异不显著；可交易回测中 Random Forest 年化收益为15.38%、信息比率为0.825，明显高于 MASTER 的7.81%和0.130，揭示预测排序能力与组合经济价值并不等价。

项目保留复杂模型未最终胜出的结果，并通过强基线、消融、滚动样本外和冻结锁箱控制研究者自由度。

项目仓库：[a-share-ml-return-prediction](https://github.com/truematon94-svg/a-share-ml-return-prediction)

### 04. 沪深300多因子 Alpha 研究与约束型指数增强

在历史时点沪深300成分股内，独立完成从候选因子检验、多因子合成到约束型指数增强的完整研究链路：

- 使用2008年至2022年历史成分股和按公告日对齐的财务数据，避免以当前成分股回填历史；
- 从价值、质量、成长、动量/反转、低波和流动性等9个候选因子出发，经训练期RankICIR和分组收益检验保留6个正式因子；
- 比较等权、训练期IC加权和IC协方差调整三种合成方法，等权Alpha在2020年至2022年测试期取得0.853的RankICIR；
- 在同一Alpha下比较沪深300基准近似、Top-50等权和约束型指数增强组合；约束型组合在2008年至2022年本地回测中取得4.86%年化收益、0.211 Sharpe和-38.53%最大回撤，月均换手率由Top-50的44.75%降至31.64%；
- 完成Top-K敏感性、年度IC、因子暴露和失效期分析，并使用聚宽对2023年至2025年扩展样本外进行独立验证；
- 明确记录静态2025版行业映射、截面市值基准权重和本地成交成本近似等研究边界，不将当前版本描述为商业级风险模型或可直接实盘系统。

项目仓库：[csi300-multifactor-alpha-enhancement](https://github.com/truematon94-svg/csi300-multifactor-alpha-enhancement)

## 持续进行中的项目

### 05. 自主Alpha因子挖掘与持续性验证

持续提出和登记自主Alpha假设，统一完成时点审计、横截面检验、成本评估、滚动样本外和因子衰减跟踪。项目同时保留有效、失效和重复信号，避免只展示正结果。目前使用私有仓库维护，待形成稳定研究成果后再决定是否公开。

## 计划中的项目

### 06. 订单簿微观结构驱动的高频交易策略

计划在获得可靠的逐笔成交与订单簿数据后启动，重点研究微观结构信号、执行成本、延迟和容量约束。目前不创建独立仓库。

### 07. 波动率曲面与衍生品相对价值策略

计划围绕期权隐含波动率、期限结构、偏度与相对价值机会建立研究流程。目前处于知识与数据准备阶段，不创建独立仓库。

## 研究原则

- 严格区分研报复现、自主扩展和原创研究；
- 明确样本区间、股票池、数据可得时点与交易成本；
- 优先检查未来函数、幸存者偏差和数据泄露；
- 同时报告成功结果、复现偏差和样本外失效；
- 原始数据、研报原件和授权材料仅保存在本地。

## 主要工具

Python、pandas、NumPy、SciPy、statsmodels、scikit-learn、LightGBM、XGBoost、PyTorch、cvxpy、PyArrow、Matplotlib、Seaborn、JupyterLab、pytest、JoinQuant、Git/GitHub。

