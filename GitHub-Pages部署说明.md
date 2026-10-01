# GitHub Pages 部署说明

## 一、要上传的文件

**全部** `github-pages-ready/` 里的内容，一字不差地传到仓库根目录：

```
index.html                    ← 主页面（必须叫这个名字，GitHub Pages 会自动识别为首页）
.nojekyll                     ← 空文件，别漏！告诉 GitHub 不要用 Jekyll 处理
assets/
  ├── audio/
  │   └── tebie_intro.mp3     ← 《特别的人》前奏（1.2M）
  └── img/
      ├── me_400.webp         ← 你的头像（webp，优先加载）
      ├── me_400.jpg          ← 你的头像（jpg 回退）
      ├── her_400.webp        ← 她的头像（webp，优先加载）
      └── her_400.png         ← 她的头像（png 回退）
```

**上传后仓库长这样：**

```
你的仓库/
├── index.html
├── .nojekyll
└── assets/
    ├── audio/tebie_intro.mp3
    └── img/
        ├── me_400.webp
        ├── me_400.jpg
        ├── her_400.webp
        └── her_400.png
```

> ⚠️ **`assets` 必须和 `index.html` 同级**。如果放进子文件夹，页面会加载不到音乐和头像。

---

## 二、两种上传方式

### 方式 A：网页拖拽（最简单，不用装任何东西）

1. 打开 GitHub，右上角 `+` → **New repository**
2. 仓库名随便起，比如 `for-yue`，选 **Public**（Pages 免费版只支持公开仓库）
3. 点 **Create repository**
4. 在空仓库页面点 **uploading an existing file**
5. 把 `index.html`、`.nojekyll` 拖进去
6. 再点 **Add file → Upload files**，把整个 `assets` 文件夹拖进去

   > 拖文件夹时保持结构：GitHub 网页上传会保留文件夹层级。
   > 如果拖不进去，就手动建 `assets` → `audio`、`img` 目录，逐个上传。

7. 底部填个 commit 信息，点 **Commit changes**

### 方式 B：命令行（快，适合文件多）

```bash
# 在你本地解压后的 github-pages-ready 目录里
cd github-pages-ready

git init
git add -A
git commit -m "birthday"
git branch -M main
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main
```

---

## 三、开启 Pages

1. 仓库页面 → **Settings**（顶部菜单）
2. 左侧栏找到 **Pages**
3. **Source** 选 `Deploy from a branch`
4. **Branch** 选 `main`，右边文件夹选 `/ (root)`
5. 点 **Save**
6. 等 1~2 分钟，刷新页面，顶部会出现绿色链接：

```
https://你的用户名.github.io/仓库名/
```

**这个链接就是你发给她的网址。**

---

## 四、手机上的注意事项（重要）

页面已经针对手机做了处理，但有两件事你要知道：

### 1. 麦克风吹蜡烛

| 情况 | 结果 |
|---|---|
| 用 **Safari / Chrome** 打开，允许麦克风 | ✅ 真实吹气，火焰随呼吸熄灭 |
| 微信内置浏览器 | ⚠️ 权限可能被拦，自动切 5 秒动画吹灭 |
| 拒绝授权 / 设备不支持 | ✅ 自动切 5 秒动画吹灭 |

**想要真实吹气效果 → 让她用系统浏览器打开，别在微信里点。**

链接发过去时可以说：「用浏览器打开，别在微信里点，效果不一样。」

### 2. 音量

iOS 的静音拨片会静音网页音频。如果她插着耳机听歌可能没声——建议提醒她**检查一下手机侧边的静音开关**。

---

## 五、想更好看？可以绑个短域名

默认链接是 `https://你的用户名.github.io/仓库名/`，有点长。如果你有自己的域名：

Settings → Pages → **Custom domain** 填进去，再按提示在域名商处加一条 CNAME 记录。

不绑也完全能用。

---

## 六、改成私密仓库怎么办

GitHub Pages 对**免费账号**只支持公开仓库。公开仓库意味着别人理论上能看到这个页面（但没人知道地址就找不到）。

如果你想让页面更隐蔽：

- **方案一**：仓库名起得随意一点，别用真名。地址本身就不容易被猜到。
- **方案二**：升级 GitHub Pro，支持私有仓库开 Pages。
- **方案三**：不用 Pages，直接把 `birthday` 文件夹打包发给她，让她本地打开（离线也能用，功能完全一样）。

---

## 七、上传前最后确认

- [ ] `index.html` 在仓库根目录
- [ ] `.nojekyll` 在仓库根目录（空文件也要有）
- [ ] `assets/audio/tebie_intro.mp3` 能访问
- [ ] `assets/img/` 里四个头像文件都在
- [ ] Settings → Pages 显示绿色成功提示
- [ ] 手机浏览器打开链接，**划到第②幕能看到雨和茉莉**
- [ ] 划到最后，**吹气或点火焰，蜡烛会灭**

---

## 八、`.nojekyll` 拖不上去怎么办？

这是唯一一个容易卡住的点。GitHub 网页上传**不接受以 `.` 开头的文件**，而 `.nojekyll` 正好是。

**办法一（推荐）**：用上面「方式 B」命令行推送，`git add -A` 会自动带上它。

**办法二**：在仓库页面点 **Add file → Create new file**，文件名输入框里打 `.nojekyll`（GitHub 会允许），内容留空，直接 Commit。

**办法三**：不建也行。这个文件的作用只是让 GitHub 跳过 Jekyll 处理——而本项目全是静态文件、没有下划线开头的目录，Jekyll 本来也不会捣乱。**少了它页面照样能跑**，只是多一层保险。

---

## 九、整个包只有 1.45MB

压缩包 `birthday-github-pages.zip` 共 12 个文件、1.45MB：

| 文件 | 体积 | 说明 |
|---|---:|---|
| `assets/audio/tebie_intro.mp3` | 1.2 MB | 128kbps，75 秒 |
| `assets/img/her_400.png` | 208 KB | 她的头像（回退格式） |
| `index.html` | 51 KB | 单文件，含全部 CSS/JS |
| `assets/img/her_400.webp` | 25 KB | 她的头像（主格式） |
| `assets/img/me_400.jpg` / `.webp` | 26 KB | 你的头像 |
| 其余（说明文档、`.nojekyll`） | ~8 KB | |

网页本身**零外部依赖**——没有 CDN、没有 Google Fonts、没有第三方库。断网也能玩，十年后链接还在也不会坏。
