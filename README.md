# huanqwer.github.io

老邋遢的个人博客站（<https://huanqwer.github.io/>）的**发布外壳**。

这个仓库本身不存文章，只有一条发布流水线：拉取内容仓库
[huanqwer/HarnessCraft](https://github.com/huanqwer/HarnessCraft) → 构建 → 发布到 GitHub Pages。

## 分工

| 你想做的事 | 去哪里做 |
| --- | --- |
| 写文章、改站点配置/样式 | HarnessCraft：`posts/`、`mkdocs.yml`、`site-assets/` |
| 站点怎么构建、怎么发布 | 本仓库：`.github/workflows/publish.yml` |

文章只有一个真源（HarnessCraft 的 `posts/`），本仓库不保存任何正文副本。

## 发布时机

- **默认**：`*/15 * * * *` 定时刷新——HarnessCraft 推完文章后，最长 15 分钟自动上线，不需要任何凭据。
- **即时**（可选，一次性配置）：在 HarnessCraft 仓库里加一个名为 `PAGES_DISPATCH_TOKEN` 的 secret
  （细粒度 PAT，对 `huanqwer.github.io` 有 Contents: Read and write），
  之后 HarnessCraft 的 push 会通过 `repository_dispatch` 立刻触发本仓库重建。
- 也可以随时在 Actions 页手动 `Run workflow`。

## 首次启用 Pages

本仓库 Settings → Pages → Source 选 **GitHub Actions**。之后每次发布都会走
`actions/deploy-pages`，站点根地址即 <https://huanqwer.github.io/>。

## 本地预览

站点内容不在本仓库，预览请到 HarnessCraft 里做：

```bash
cd HarnessCraft
python3 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt
python3 tools/build_site.py && mkdocs serve
```
