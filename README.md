# 视觉目标跟踪 · 论文专栏（VOT Papers Archive）

> Visual Object Tracking · 中英双语论文档案库，每日自动更新。

本站点为「视觉目标跟踪（Visual Object Tracking, VOT）」方向的独立论文专栏，由
`build_tracking.py` 从 arXiv（主）与 Semantic Scholar（best-effort）抓取并生成。

主站（AI 资讯档案库）：https://TAI-GG.github.io/cv-papers-archive/

---

## 🔗 在线访问

| 页面 | 地址 | 说明 |
|------|------|------|
| 本周深度报告 | https://TAI-GG.github.io/vot-papers-archive/ | 近 7 天 VOT 论文（含汇总表 + 主题详情 + 类别分布） |
| 每日速览归档 | https://TAI-GG.github.io/vot-papers-archive/daily/index.html | 每日新增论文索引 |
| 历史报告总览 | https://TAI-GG.github.io/vot-papers-archive/reports/index.html | 全部报告内容**直接内联展示**，无需跳转 |

---

## 📁 仓库结构

```
vot-papers-archive/
├── index.html              # 本周深度报告（站点首页）
├── daily/
│   ├── index.html          # 每日速览归档索引
│   └── YYYY-MM-DD.html     # 每期日报
├── reports/
│   ├── index.html          # 报告总览（全部报告内容内联）
│   └── YYYY-MM-DD.html     # 独立周报页（含历史导入报告）
├── README.md               # 本说明
├── build_tracking.py       # 构建与推送脚本
└── push_utils.py           # 与主站共用的 git 发布模块
```

---

## 🧠 数据来源与筛选

- **数据源**：arXiv API（主，`cat:cs.CV OR cat:cs.RO` ＋ tracking 检索）＋ Semantic Scholar API（best-effort，限流时自动降级为 arXiv-only）；并合并原 `TAI-GG/visual-tracking-papers` 仓库的历史周报（4 期）。
- **严格相关性过滤**：标题 / 摘要须命中强信号短语（如 `object tracking`、`visual tracking`、`tracker`、`multi-object tracking`、`siamese`、`tracking benchmark`、`long-term tracking` 等），并排除 SLAM / 位姿估计 / 医学影像 / 手部·人脸·眼动跟踪 / 视频生成 / NLP 等相邻但非 VOT 的主题，避免假阳性。
- **分类**：多目标跟踪、单目标跟踪、3D / 4D 跟踪、多模态跟踪、域自适应与鲁棒、无人机跟踪、架构（SSM / 扩散）、数据集与基准、通用跟踪。
- **语言**：每篇论文提供英文原文 + 中文译文（带本地缓存以节省配额）。

---

## ✨ 页面特性

- **中英双语**：每篇论文含英文摘要与中文译文；
- **历史报告内联**：报告总览页直接呈现论文卡片内容，而非仅链接列表；
- **自愈机制**：导航链接按页面深度自动校正（子路径部署安全）；译文失败不写入缓存，后续构建会自动重试补齐。

---

## ⚙️ 更新机制

- **频率**：每日自动构建与推送；
- **上游容错**：arXiv 出现限流 / 5xx 时，先等待再分别探测代理与直连，仅当恢复后才重抓，最多 2 轮；持续不可用时以历史报告内联兜底，专栏不会空页；
- **推送方式**：`git fetch` + `reset --hard` 同步现有仓库 → 覆盖生成文件 → 普通 `commit` + `push`（**不 force**）。

---

## 🛠️ 本地构建

```bash
python build_tracking.py
```

前置条件：
- Windows 凭据管理器已保存 GitHub PAT（目标 `git:https://github.com`，需 `repo` 权限）；
- 推送目标仓库：`TAI-GG/vot-papers-archive`；
- 网络需可经本地出口代理访问 GitHub / arXiv（脚本内置代理注入，并在代理被限流时自动直连兜底）。

---

## ⚠️ 声明

- 论文版权归原作者与 arXiv / Semantic Scholar 所有，本站点仅作聚合索引，所有链接均指向原始出处；
- 中文译文由机器翻译自动生成，仅供参考，请以英文原文为准；
- 数据由自动化脚本筛选，可能存在漏判 / 误判。
