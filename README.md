# 校园快递 · 取件助手（Campus Express）

三人协作的校园快递取件网页。原首页是「一个 index.html + 一个 app.js」的单页应用，现已按《首页代码拆分指南》拆成：

**公共样式 + 首页 + 三个独立功能页**，每人负责一个页面，互不干扰。

## 在线访问

- 拆分后的线上预览（GitHub Pages）：https://qkb111.github.io/kuaidi-project/
- 拆分前版本：https://cedar-frost-ai51h.ship.place/
- GitHub 仓库：https://github.com/qkb111/kuaidi-project

## 目录结构

```
项目根目录（仓库根）
├── style.css       公共样式：深色背景、磨砂卡片、字体配色，所有页面共用
├── index.html      首页：三个功能卡片入口
├── template.html   空白子页面模板：发给队友直接套用
├── pickup.html     取件码详情页（同学 A）
├── barcode.html    身份码页（同学 B）
├── map.html        驿站地图页（同学 C）
├── CONTRIBUTING.md 三人协作流程说明
└── README.md
```

## 本地预览

```bash
# 在项目根目录执行（任选其一）
python -m http.server 8000
# 然后浏览器打开 http://localhost:8000
```

直接双击 `index.html` 也能看，但建议用本地服务器，避免个别浏览器对本地文件的限制。

## 分工

| 文件 | 负责人 | 负责内容 | 分支 |
| --- | --- | --- | --- |
| `pickup.html` | 同学 A | 取件码详情、复制码、货架信息 | `feature/pickup` |
| `barcode.html` | 同学 B | 身份码/条形码展示与刷新 | `feature/barcode` |
| `map.html` | 同学 C | 驿站货架地图、选柜交互 | `feature/map` |
| `index.html` / `style.css` / `template.html` | 组长（仓库所有者） | 首页入口、公共样式、模板维护 | 直接改或走 PR |

## 协作规则（摘要）

1. **只改自己负责的页面**，比如同学 A 只动 `pickup.html`。
2. 每个人在**自己的分支**上开发，完成后发 Pull Request 到 `main`，至少由一位队友 Review 后合并。
3. `main` 分支已开启保护：协作者不能直接 push，必须走 PR（仓库所有者保留直接推送权限）。
4. 需要改 `style.css` 这类公共文件时，先在群里说一声，由组长统一改，避免冲突。

详细步骤见 [CONTRIBUTING.md](CONTRIBUTING.md)。