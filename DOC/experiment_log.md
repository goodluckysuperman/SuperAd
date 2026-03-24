# 实验记录

这份文档用于记录每一次有结论的探索、baseline 和后续实验。

建议每次记录尽量简短，但至少回答下面几个问题：

- 做了什么
- 用了什么数据或特征
- 结果怎样
- 下一步准备怎么改

---

## 2026-03-22

### 初始化目录约定

- 建立了 `NOTEBOOKS/01_eda`、`OUTPUTS/01_eda`、`DATA/interim`、`DATA/processed`
- 当前阶段准备先从 EDA 开始，后续 baseline 和特征工程按约定逐步扩展
- `SRC/` 暂不提前创建，等出现重复代码时再补

下一步建议：

- 在 `NOTEBOOKS/01_eda` 新建第一个数据概览 notebook
- 先完成字段、类型、样本量和基本结构检查

### 第一轮数据概览 EDA

- 在 `kddtaac` 环境中补齐了 `pandas`、`pyarrow`、`matplotlib`、`jupyter`，并同步更新了 `requirements.txt`
- 新建并执行了 `NOTEBOOKS/01_eda/01_data_overview.ipynb`
- 生成了 `OUTPUTS/01_eda` 下的摘要、字段统计、嵌套长度统计、标签动作计数、schema 文本和概览图

本轮主要发现：

- 示例数据共有 1000 行、7 列，顶层字段没有缺失值
- `user_id` 在样本内全唯一，`item_id` 有 927 个唯一值
- 时间范围大致覆盖 2026-02-07 到 2026-02-10
- `label` 每行固定 1 条，但 `action_type` 存在两类，分别是 1 和 2
- `user_feature` 平均长度约 38.66，`item_feature` 平均长度约 11.86
- `seq_content_seq` 和 `seq_item_seq` 长度固定，`seq_action_seq` 基本固定为 10，只有极少数短序列

下一步建议：

- 继续拆第二个 notebook，专门看 `label` 和 `timestamp`
- 再做第三个 notebook，细看 `user_feature`、`item_feature`、`seq_feature` 的内部 schema 和 `feature_id` 分布
