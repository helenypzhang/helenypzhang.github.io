# 个人主页维护手册

这份手册适用于 Yupei Zhang 的个人主页：<https://helenypzhang.github.io/>。

项目主要内容位于以下目录：

- `content/`：英文内容
- `content_zh/`：中文内容
- `public/`：论文图片、头像、CV 等公开文件
- `src/`：页面组件和样式；日常更新通常不需要修改

除论文列表外，修改英文内容时通常也应同步修改 `content_zh/` 中的对应文件，以免中英文页面内容不一致。论文数据只维护一份 `content/publications.bib`，中英文页面会共用它。

## 1. 添加 News

英文新闻在 `content/news.toml`，中文新闻在 `content_zh/news.toml`。

把最新消息放在文件最上方：

```toml
[[news]]
date = "2026-09"
content = "Our paper was accepted by ..."
```

中文文件中添加对应内容：

```toml
[[news]]
date = "2026-09"
content = "我们的论文被……接收。"
```

日期建议使用 `YYYY-MM`，例如 `2026-09`。

## 2. 添加论文

所有论文都添加到 `content/publications.bib`。把新论文条目放在文件最上方；页面会根据年份和月份自动倒序排列。

### 期刊论文示例

```bibtex
@article{zhang2026example,
  selected = {true},
  title = {Paper Title},
  author = {Yupei Zhang# and Coauthor Name# and Senior Author},
  year = {2026},
  month = sep,
  journal = {Journal Name},
  url = {https://example.com/paper},
  code = {https://github.com/example/repository},
  preview = {example.png},
  description = {A short description of the paper.}
}
```

### 会议论文示例

将类型改为 `@inproceedings`，并用 `booktitle` 填写会议名称：

```bibtex
@inproceedings{zhang2026conference,
  title = {Paper Title},
  author = {Yupei Zhang and Coauthor Name and Senior Author},
  year = {2026},
  month = oct,
  booktitle = {Conference Name},
  url = {https://example.com/paper},
  preview = {conference-paper.png}
}
```

### 预印本示例

使用 `@misc` 或 `@unpublished`：

```bibtex
@misc{zhang2026preprint,
  title = {Paper Title},
  author = {Yupei Zhang and Coauthor Name and Senior Author},
  year = {2026},
  month = sep,
  url = {https://arxiv.org/abs/xxxx.xxxxx},
  preview = {preprint.png}
}
```

### 论文特殊字段说明

- `selected = {true}`：在主页的 Selected Publications 中展示。删除该行或改为 `false`，则只在 Publications 页面展示。
- `preview = {图片文件名}`：论文预览图，图片必须放到 `public/papers/`。
- `url`：Paper 按钮链接。没有普通链接时也可以只填写 `doi`，网站会自动生成 DOI 链接。
- `code`：Code 按钮链接；没有代码时删除该行。
- `journal`：期刊名称。
- `booktitle`：会议名称。
- `month`：建议写成 `jan`、`feb`、`mar` 等英文缩写，用于同一年内排序。
- `description`：简短论文介绍，可选。
- 每条论文开头的标识符，例如 `zhang2026example`，必须唯一，不能和其他论文重复。

### 作者标记

- 作者姓名后加 `#` 表示共同第一作者，网页显示为 `*`。
- 作者姓名后加 `*` 表示通讯作者，网页显示为 `†`。
- 如果没有手动添加通讯作者标记，系统默认最后一位作者为通讯作者。
- 作者之间必须使用 `and` 分隔。
- `Yupei Zhang` 会自动高亮。

例如：

```bibtex
author = {Yupei Zhang# and First Coauthor# and Senior Author*}
```

## 3. 添加或更换论文图片

将图片复制到：

```text
public/papers/
```

然后在论文条目中填写完全一致的文件名：

```bibtex
preview = {my-paper-figure.png}
```

建议：

- 使用 PNG、JPG 或 WebP。
- 推荐接近 `16:10` 的横向图片；其他比例也可以，页面会完整显示而不会裁切。
- 文件名尽量只使用英文小写字母、数字和连字符，例如 `tmi-2026-framework.png`。
- 替换已有图片时，保留原文件名最方便；浏览器可能有缓存，发布后可稍等或强制刷新。

## 4. 修改个人介绍与研究兴趣

- 英文个人介绍：`content/bio.md`
- 中文个人介绍：`content_zh/bio.md`
- 英文研究兴趣：`content/about.toml` 中的 `research_interests`
- 中文研究兴趣：`content_zh/about.toml` 中的 `research_interests`

研究兴趣示例：

```toml
[profile]
research_interests = [
  "Multimodal Learning in Medicine",
  "Computational Pathology",
  "Medical Image Analysis",
  "Translational AI"
]
```

## 5. 修改姓名、职位、联系方式和社交链接

英文信息在 `content/config.toml`，中文姓名、职位等翻译在 `content_zh/config.toml`。

常用位置：

- `[author]`：姓名、职位、学校、头像
- `[social]`：Email、Google Scholar、GitHub、LinkedIn、地点
- `[site]`：网站标题、说明和最后更新时间

头像文件目前由 `avatar = "/bio.png"` 指定，对应 `public/bio.png`。

## 6. 修改导航栏

英文导航在 `content/config.toml` 的 `[[navigation]]`，中文导航在 `content_zh/config.toml`。

### 添加外部链接

例如添加 Google Scholar：

```toml
[[navigation]]
title = "Google Scholar"
type = "link"
target = "google_scholar"
href = "https://scholar.google.com/..."
```

中文配置中也添加同一项，并把 `title` 翻译成中文。

### 调整导航顺序

直接调整各个 `[[navigation]]` 区块在文件中的先后顺序即可。

### 暂时隐藏导航项

删除或注释掉英文和中文配置中的对应 `[[navigation]]` 区块。内容文件可以保留，以后需要时再把导航配置加回来。Awards 页面目前就是以这种方式保留但不显示。

## 7. 新增普通页面

最简单的是新增 Markdown 文本页面。假设要添加 Teaching 页面：

1. 新建 `content/teaching.md`，填写英文正文。
2. 新建 `content_zh/teaching.md`，填写中文正文。
3. 新建 `content/teaching.toml`：

```toml
type = "text"
title = "Teaching"
description = "Teaching experience and activities."
source = "teaching.md"
```

4. 新建 `content_zh/teaching.toml`：

```toml
type = "text"
title = "教学"
description = "教学经历与活动。"
source = "teaching.md"
```

5. 在英文 `content/config.toml` 添加：

```toml
[[navigation]]
title = "Teaching"
type = "page"
target = "teaching"
href = "/teaching"
```

6. 在中文 `content_zh/config.toml` 添加相同配置，并翻译 `title`。`target` 和 `href` 不要翻译。

发布后页面地址会是 `/teaching/`。

## 8. 更新 Services

- 英文页面：`content/services.md`
- 中文页面：`content_zh/services.md`
- 页面标题和说明：对应目录中的 `services.toml`

按照现有 Markdown 格式增加 Conference Reviewer 或 Journal Reviewer 条目即可。

## 9. 更新 CV

当前 CV 文件位于：

```text
public/data/cv_yupeizhang_2025.pdf
```

如果想保持现有链接不变，直接用新 PDF 替换这个文件即可。如果更改文件名，还需要同步修改 `content/cv.md` 和 `content_zh/cv.md` 中的链接。

## 10. 本地预览

在项目目录运行：

```bash
pnpm install
pnpm dev
```

然后打开终端显示的本地网址，通常是 <http://localhost:3000/>。

检查完成后，在终端按 `Control + C` 停止预览。

正式提交前建议运行：

```bash
pnpm build
```

如果构建成功，说明静态页面可以正常生成。

## 11. 发布到 GitHub

网站会在 `main` 分支更新后自动发布。常用命令：

```bash
git status
git add content content_zh public
git commit -m "Update publications and news"
git push origin main
```

如果还修改了其他文件，也要把它们加入 `git add`，或者确认内容无误后使用 `git add -A`。

推送后可在 GitHub 仓库的 Actions 页面查看发布进度。通常稍等片刻，再访问 <https://helenypzhang.github.io/> 并刷新即可看到更新。

## 12. 发布前检查清单

- 英文和中文内容是否都已更新。
- 新论文的年份、月份、期刊或会议名称是否正确。
- `selected` 是否符合是否展示在主页的预期。
- Paper、Code 和 DOI 链接是否正确。
- 论文图片是否放在 `public/papers/`，文件名是否与 BibTeX 一致。
- 共同第一作者 `#` 与通讯作者 `*` 是否标记正确。
- 导航栏英文版和中文版是否一致。
- `pnpm build` 是否成功。
- `git status` 中是否只有本次希望发布的修改。
