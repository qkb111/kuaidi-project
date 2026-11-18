# AGENTS.md — 给 AI 编码代理的协作规则

本仓库是三人协作的静态网页项目：`index.html` 是首页入口，三个功能页分别由三个人负责。

**你（AI 代理）在动手前，必须先确认：当前分支是哪条、负责的是哪个页面。** 只允许修改这个页面，其他文件一律不碰。

## 一、硬性规则

1. **一人一分支一文件**
   - `feature/pickup` → 只能改 `pickup.html`
   - `feature/barcode` → 只能改 `barcode.html`
   - `feature/map` → 只能改 `map.html`
   - 不在以上分支、或分支与文件对不上时，先停下来问组员，不要猜。

2. **禁止修改公共文件**（除非任务明确要求，并且组员已确认）
   - `style.css`、`index.html`、`template.html`
   - 其他队友负责的 HTML 页面
   - `README.md`、`CONTRIBUTING.md`

3. **只改 `<main id="app-content">` 里面的内容**
   - 页面外壳（`app-header`、`subscreen-head` 返回栏、`bottom-nav`、`toast`）已经写好，保持不动。
   - 页面脚本写在文件末尾的 `<script>` 里，只写本页需要的逻辑。

4. **复用 `style.css` 已有样式**，不要另起一套配色或字体。常用 class：
   - 卡片：`detail-card`、`detail-kicker`、`detail-grid`
   - 按钮：`wide-action`（主按钮）、`soft-action`（次要按钮）
   - 信息格：`meta-box` + `meta-label` / `meta-value`
   - 说明文字：`long-note`
   - 地图：`map-toolbar`、`zone-switch`、`zone-button`、`station-map`、`map-row`、`shelf-rect`、`map-summary`
   - 条形码：`barcode-box`、`barcode-label`

5. **确实需要新样式时**：写在页面内的 `<style>` 里，并且只作用于本页（class 加前缀，例如 `.pickup-xxx`），**不要改 `style.css`**。

6. **保持中文文案和暗色风格**，不要改站点名称、导航结构。

## 二、开发与自测

```bash
# 1. 先同步主分支
git checkout main && git pull origin main
git checkout feature/barcode        # 换成自己那条分支
git merge main                      # 把最新 main 合进来

# 2. 本地预览
python -m http.server 8000          # 浏览器打开 http://localhost:8000
```

自测要求：

- 手机宽度 **375px** 下布局正常
- 浏览器 F12 Console **没有红色报错**
- 页面内链接可点、按钮可用
- 删除所有调试用 `console.log`、写死的测试数据

## 三、提交与上传（不要直接改 main）

```bash
git add barcode.html                # 只加自己负责的文件
git commit -m "feat(barcode): 说明改了什么"
git push origin feature/barcode
```

然后在 GitHub 上：

1. 打开仓库 → **Pull requests** → **New pull request**
2. base 选 `main`，compare 选自己的 `feature/xxx`
3. 描述写清楚改了什么，加一行 `Closes #5`（换成自己的 Issue 号）
4. 等另一位队友 Review 通过后点 **Merge**

> `main` 有分支保护：协作者直接 push 会被拒绝，必须走 PR。**不要尝试强推或绕过保护。**

## 四、绝对不要提交的东西

- 临时文件、截图、测试数据、`node_modules`
- 调试代码、注释掉的旧代码
- 对 `style.css` / `index.html` / `template.html` 的顺手修改

## 五、交付时告诉组员

1. 改了哪个文件、加了什么功能
2. 自测结果（375px、Console、点击测试）
3. PR 链接
4. 如果有做不到的地方（比如需要新样式），明确说明，不要偷偷改公共文件