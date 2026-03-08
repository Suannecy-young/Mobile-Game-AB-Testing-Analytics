[English](README.md) | [简体中文](README_zh.md)

---

# 🎲 移动端游戏 A/B 测试分析

![Python](https://img.shields.io/badge/Python-Pandas%20%7C%20SciPy-blue)
![Statistics](https://img.shields.io/badge/Statistics-A%2FB%20Test%20%7C%20Z--Test-green)
![Data Quality](https://img.shields.io/badge/Data%20Quality-AI%20Assisted%20Cleaning-orange)
![Decision](https://img.shields.io/badge/Business%20Decision-NO--GO-red)

## 📖 项目背景
本项目通过 A/B 测试评估了一项游戏内的关卡更新。产品团队提议将游戏中的第一个“强制等待关卡（Time-gate）”从 **Level 30 推迟到 Level 40**。

作为数据分析师，我分析了超过 **90,000 条**玩家测试数据，评估这次更新对用户留存率的具体影响，并给出相应的业务建议。

---

## 🛠️ 1. 数据清洗与异常值处理
**问题：** 原始数据集中存在极端的异常值（比如疑似脚本刷出的上万局游戏记录），这些脏数据会直接影响假设检验 P-value 的准确性。

**解决方案：** 为了避免人工主观设定过滤阈值，我使用 **GitHub Copilot** 辅助编写了基于 **IQR (四分位距)** 算法的异常值处理逻辑。

**结果：**
* 自动排除了无效的极端样本。
* 数据清洗代码的编写效率提升了约 40%。
* 保证了后续统计检验的样本质量和结论可靠性。

---

## 📊 2. 留存率分析 (Bootstrapping & Z-Test)
为了评估次日留存（1-day）和 7日留存表现，我使用了两种统计方法进行交叉验证：

### Bootstrapping (自助法重采样 - 1,000 次)
通过对样本进行 1,000 次放回重采样，观察留存率差异的分布。结果显示，如果将关卡保持在 Level 30，7日留存率高于 Level 40 的概率为 **99.9%**。

### Z-Test 双样本检验
* **Z-Statistic:** `3.7041`
* **P-Value:** `0.00021`
* **结论:** P值 `p < 0.001` (远低于常规的 0.05 显著性水平)。这说明 Level 40 组的留存率下降在统计学上是显著的，并非随机误差。

---

## 🚫 3. 结论与建议：不建议上线 (NO-GO)

基于上述数据结果，我建议产品团队**放弃该版本更新**，保持原有的 Level 30 关卡设计。

**原因分析：** 为什么让玩家“玩得更久才遇到阻碍”反而降低了留存？这个现象符合行为心理学中的 **享乐适应 (Hedonic Adaptation)** 理论。在 Level 30 设置关卡能强制玩家适时休息，拉长对游戏的新鲜感；如果推迟到 Level 40，玩家前期连续游玩时间过长，容易提早产生疲劳感，从而导致流失。

---

## 📂 仓库结构
* `/data/cookie_cats.csv`: 原始数据集 (包含 90,189 条玩家日志)。
* `/ab_test_analysis.ipynb`: 核心分析代码 (包含异常值清洗、EDA、Bootstrapping 模拟与假设检验)。
