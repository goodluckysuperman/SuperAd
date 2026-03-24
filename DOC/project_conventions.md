# KDDTAAC 项目约定

这份文档用来固定当前项目的开发和整理方式，目标不是一开始把流程做得很复杂，而是尽量避免后期文件越堆越乱。

如果后面项目规模变大，优先在现有约定上扩展，而不是频繁推翻目录结构。

## 1. 环境约定

- 当前项目默认使用 Conda 虚拟环境 `kddtaac`
- Python 相关命令统一使用：

```powershell
conda run -n kddtaac --no-capture-output ...
```

- 不依赖“当前终端是否已经激活环境”来判断执行环境
- 新增、删除或升级 Python 包时，必须同步更新仓库根目录的 `requirements.txt`

这样做的好处是：

- 运行环境更明确
- 更不容易因为终端状态不同而报错
- 以后别人接手时更容易复现

## 2. 项目目录约定

项目后续建议逐步维护成下面这种职责分离的结构：

```text
KDDTAAC/
├─ DATA/
├─ DOC/
├─ NOTEBOOKS/
├─ SRC/
├─ OUTPUTS/
├─ requirements.txt
└─ AGENTS.md
```

每个目录的职责如下：

- `DATA/`：输入数据和数据处理中间产物
- `DOC/`：项目说明、学习笔记、实验记录、约定文档
- `NOTEBOOKS/`：探索性分析和阶段性实验 notebook
- `SRC/`：可复用的 Python 代码
- `OUTPUTS/`：图表、统计结果、模型输出、提交文件等运行产物

核心原则是：

- 探索过程和正式代码分开
- 输入数据和输出结果分开
- 结果文件不要散落在 notebook 旁边

## 3. 阶段目录约定

为了避免后面同类文件越来越多，建议按阶段维护目录，并使用数字前缀保证顺序清晰。

推荐结构：

```text
NOTEBOOKS/
├─ 01_eda/
├─ 02_baseline/
├─ 03_features/
└─ 04_modeling/

OUTPUTS/
├─ 01_eda/
├─ 02_baseline/
├─ 03_features/
└─ 04_modeling/
```

各阶段建议含义如下：

- `01_eda`：看数据结构、字段类型、标签分布、时间分布、缺失情况
- `02_baseline`：最小可运行 baseline，先打通训练和验证流程
- `03_features`：补充统计特征、交叉特征、历史行为特征
- `04_modeling`：更复杂的模型方案、调参、对比实验

这样维护的好处是：

- 回头看项目时，能快速知道每个文件属于哪个阶段
- 不会把“刚开始的探索”和“后期正式实验”混在一起
- 产出物也能和阶段一一对应

## 4. Notebook 约定

- notebook 文件名使用“编号 + 主题”的形式
- 示例：
  - `01_data_overview.ipynb`
  - `02_label_and_time.ipynb`
  - `03_feature_schema.ipynb`
- 一个 notebook 尽量只解决一个明确问题
- 不要为了每个小想法都新建一个顶层目录
- 如果同一段代码在多个 notebook 里反复复制，就应该移到 `SRC/`

对于当前 EDA 阶段，建议先控制在 3 个 notebook 左右，不要一开始写成一个很长的大杂烩文件。

## 5. 输出结果约定

- notebook 里生成的图、表、统计结果，统一放到 `OUTPUTS/` 对应阶段目录
- 不把导出的 csv、png、html、模型文件直接丢在仓库根目录
- 输出目录按阶段分类后，后面清理和回看都会轻松很多

例如：

```text
OUTPUTS/01_eda/
├─ label_distribution.csv
├─ timestamp_hist.png
└─ feature_count_summary.csv
```

## 6. 数据目录约定

当前已有示例数据：

- `DATA/data_sample_1000`

后续如果项目继续推进，建议逐步整理为：

```text
DATA/
├─ raw/
├─ interim/
├─ processed/
└─ data_sample_1000/
```

含义可以这样理解：

- `raw/`：原始数据，尽量不直接改
- `interim/`：清洗或展开后的中间结果
- `processed/`：可以直接用于训练或验证的数据

当前阶段不必急着搬动现有示例数据，但后面如果加入正式数据，建议按这个思路管理。

## 7. 文档记录约定

- 重要实验或阶段结论，优先记录到 `DOC/`
- 如果后面实验开始变多，建议新增：

```text
DOC/experiment_log.md
```

每次记录不需要很长，能回答下面几个问题就够了：

- 做了什么
- 用了什么数据或特征
- 结果怎样
- 下一步准备怎么改

## 8. 当前阶段最适合怎么做

以你现在的项目状态，最稳妥的推进方式是：

1. 先保留现有 `DATA/` 和 `DOC/` 不大动
2. 开始时新增 `NOTEBOOKS/01_eda/`
3. 同时新增 `OUTPUTS/01_eda/`
4. 等 notebook 里出现重复代码后，再新增 `SRC/`

这样不会一上来把工程搭得太复杂，也能提前给后面的 baseline 和建模留好位置。

## 9. 一句话原则

先按职责分目录，再按阶段分内容；探索、代码、结果三者分开，项目后期就不容易乱。
