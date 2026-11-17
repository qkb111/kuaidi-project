# 三人协作指南（CONTRIBUTING）

本项目按「一人一页、一页一文件」的方式协作：每个人只在**自己负责的 HTML 文件**里写功能，公共样式和首页由组长维护。这样即使三个人同时开发，也不会互相改到对方的代码。

## 0. 分工一览

| 成员 | 负责文件 | 固定分支 | 说明 |
| --- | --- | --- | --- |
| 同学 A | `pickup.html` | `feature/pickup` | 取件码详情页 |
| 同学 B | `barcode.html` | `feature/barcode` | 身份码 / 条形码页 |
| 同学 C | `map.html` | `feature/map` | 驿站地图页 |
| 组长 | `index.html`、`style.css`、`template.html` | `main` / 自己的分支 | 首页入口、公共样式、模板 |

> 新增页面时，先复制 `template.html`，再在组长那里登记文件名和分支，避免两个人抢同一个页面。

## 1. 第一次准备（每人只做一次）

1. 安装 Git：<https://git-scm.com/download/win>
2. 配置自己的提交身份（把名字和邮箱换成你自己的）：

   ```bash
   git config --global user.name "你的名字"
   git config --global user.email "你的邮箱"
   ```

3. 克隆仓库（需要组长把你加成协作者后才能推送）：

   ```bash
   git clone https://github.com/qkb111/kuaidi-project.git
   cd kuaidi-project
   ```

4. 切到自己的固定分支：

   ```bash
   git checkout feature/pickup    # 同学 A
   git checkout feature/barcode   # 同学 B
   git checkout feature/map       # 同学 C
   ```

5. 本地预览：

   ```bash
   python -m http.server 8000
   ```

   浏览器打开 <http://localhost:8000>，改完文件刷新即可看到效果。

## 2. 日常开发流程（每次写代码都按这个来）

```bash
# ① 先同步主分支的最新代码
git checkout main
git pull origin main

# ② 回到自己的分支，把 main 的更新合并进来
git checkout feature/pickup
git merge main

# ③ 写代码……（只改自己负责的那个 HTML 文件）

# ④ 提交并推送
git add pickup.html
git commit -m "feat(pickup): 增加复制成功提示"
git push origin feature/pickup
```

然后在 GitHub 网页上：

1. 打开仓库 → **Pull requests** → **New pull request**
2. 左边选 `main`，右边选你的 `feature/xxx` 分支
3. 标题写清楚改了什么，描述里勾选 PR 模板中的检查项
4. **Create pull request**
5. 等另一位队友点 **Approve** 后，点 **Merge pull request** 合入 `main`

`main` 已开启分支保护：**不能直接 push**，必须走 PR，且至少 1 人 Review 通过。

## 3. 每个人只能改自己的文件

| 可以改 | 不能直接改 |
| --- | --- |
| 自己负责的 HTML 页面 | 别人的 HTML 页面 |
| 自己页面里的 `<script>` | `style.css`、`index.html`、`template.html` |

- 需要加新样式时：**不要直接改 `style.css`**，先在群里说，由组长统一加；或者在自己的页面里用 `<style>` 写上只属于本页的样式（记得加注释说明）。
- 需要改首页入口（比如新增一个卡片）时：找组长改 `index.html`。
- 公共文件（`style.css`）一旦被两个人同时改，很容易冲突，所以统一归组长维护。

## 4. 提交信息（Commit message）约定

格式：`类型(范围): 说明`

| 类型 | 用途 |
| --- | --- |
| `feat` | 新功能 |
| `fix` | 修 bug |
| `style` | 只改样式/格式，不改逻辑 |
| `docs` | 改文档 |
| `refactor` | 重构，行为不变 |

示例：

- `feat(map): 支持 B 区货架切换`
- `fix(barcode): 刷新后尾号不更新`
- `style(pickup): 调整复制按钮间距`

## 5. 遇到冲突怎么办

```bash
git merge main
# 提示 CONFLICT 时，打开冲突文件，删掉 <<<<<<< ======= >>>>>>> 标记，
# 保留正确内容后：
git add 冲突文件
git commit
```

如果冲突发生在 `style.css` 或别人的页面上，**不要自己硬改**，先找组长确认。

## 6. 合并前自查清单

- [ ] 只改了自己负责的文件
- [ ] 本地预览正常，没有报错（F12 Console 无红色错误）
- [ ] 手机宽度（375px）下显示正常
- [ ] 没有把调试用的 `console.log`、测试数据留在代码里
- [ ] commit message 符合上面的格式