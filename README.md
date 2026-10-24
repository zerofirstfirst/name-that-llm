# Name That LLM

Kaggle 赛题 **Name That LLM**：判断一段短文本是由 18 个候选语言模型中的哪一个生成的。

## 赛题信息

| 项目 | 内容 |
| --- | --- |
| 任务 | 识别短文本对应的来源大模型（18 分类） |
| 训练集 | 2,699 条文本，150 个提示词 |
| 测试集 | 未见过的新提示词生成的文本 |
| 输入 | 短文本片段（无标签） |
| 输出 | 来源模型标签 |
| 指标 | Balanced Accuracy |
| 报名 | 2027-01-06 |
| 截止 | 2027-01-13 23:59 UTC |

## 目录结构

```text
.
├── README.md
├── requirements.txt
├── src/
│   ├── data.py           # 数据读取与切分
│   ├── features.py       # TF-IDF / 字符 n-gram 等特征
│   ├── train.py          # 模型训练与交叉验证
│   └── predict.py        # 生成 submission.csv
├── notebooks/
│   └── eda.ipynb         # 数据探索
├── data/                 # 本地数据（不提交原始数据）
└── submissions/          # 提交文件
```

## 快速开始

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
python -m src.train
python -m src.predict --output submissions/submission.csv
```

## 基线方案

1. **字符 n-gram + Logistic Regression**：适合作为首次提交。
2. **TF-IDF（词级 + 字符级）拼接 + Linear SVM**：通常优于纯词级特征。
3. **文本风格特征**：长度、标点、换行、emoji、大小写、句长分布。
4. **预训练句向量 + 浅层分类器**：用于提升泛化到未见提示词的能力。
5. **模型集成**：多模型概率平均。

## 实验结果

| 方案 | 本地 CV (Balanced Acc) | Kaggle Public | Kaggle Private |
| --- | --- | --- | --- |
| baseline: char n-gram + LR | - | - | - |
| TF-IDF words + SVM | - | - | - |
| + style features | - | - | - |
| ensemble | - | - | - |

## 说明

- 比赛数据受 Kaggle 条款约束，原始数据不放入仓库。
- 提交前检查 `submission.csv` 的列名与标签顺序是否与样例一致。
