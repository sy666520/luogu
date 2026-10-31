# 洛谷桌面版 · 下载安装页

静态站点，托管在 GitHub Pages。

- **仓库**：https://github.com/sy666520/luogu
- **线上地址**：https://sy666520.github.io/luogu/
- **安装包直链**：https://sy666520.github.io/luogu/download/LuoguSetup.exe

## 目录说明

```
index.html               下载安装页
logo.png                 站点图标
screenshot.png           界面截图
download/LuoguSetup.exe  安装程序（1.98 MB，内嵌全部程序文件）
.nojekyll                跳过 Jekyll 处理
LICENSE                  MIT 开源许可证
```

## 开源许可

本项目以 **MIT License** 发布（见 `LICENSE`），可自由使用、修改与分发，
但必须保留版权声明与许可声明。洛谷（luogu.com.cn）为第三方网站，本软件
仅为官方站点的桌面端封装，与洛谷官方无隶属关系。

页面内所有资源都是相对路径，「复制直链」按钮用 `location.origin` 动态拼接，
**换域名不需要改任何代码**。

## 维护与发布（GitHub CLI）

日常维护只需要一个命令：`gh`（GitHub 官方命令行工具），不需要手动管理 Personal Access Token——
`gh` 用自己的 OAuth 令牌，存在系统钥匙串里。

```bash
gh auth login --web --git-protocol https   # 首次：浏览器授权，一次性
gh repo clone sy666520/luogu               # 首次：取仓库到本地（已有可跳过）
gh repo view sy666520/luogu --web          # 随时在浏览器打开仓库
```

Windows 上一键发布脚本（在本机 `D:\Luogu\Build\publish_gh.bat`，未放入仓库）：
双击即可完成「同步最新安装包 → 提交 → 推送 → 确认 Pages → 等构建 → 在线验收」全流程。

### 方式一：命令行推送（推荐）

```bash
winget install --id GitHub.cli --exact --accept-package-agreements   # 装 gh
gh auth login --web --git-protocol https
gh auth setup-git                  # 让 git push 走 gh 令牌，不用再配 PAT

cd <你的仓库目录>
git push -u origin main
```

### 方式二：网页上传（完全不用命令行）

1. GitHub 新建仓库，名字填 `luogu`，选 Public，**不要勾** README / .gitignore / License
2. 进入新仓库，点 `uploading an existing file`
3. 把 `index.html`、`logo.png`、`screenshot.png`、`README.md`、`LICENSE` 拖进去，
   再新建文件 `download/LuoguSetup.exe`（路径里带斜杠会自动建目录）
4. 提交后 Settings → Pages → Source 选 `Deploy from a branch`，
   Branch 选 `main`、目录 `/ (root)`，保存
5. 等 1~2 分钟，访问 https://sy666520.github.io/luogu/

## 更新安装包

主程序重新编译（`build_all.bat`）后：
双击 `publish_gh.bat`，或手动执行：

```bash
cd <你的仓库目录>
cp <新安装包路径> download/LuoguSetup.exe
git add download/LuoguSetup.exe
git commit -m "更新安装包"
git push
```

Pages 会在 1 分钟左右重新构建，之后再访问就是新包。

## 绑定自定义域名（可选，需要先买域名）

仓库 Settings → Pages → Custom domain 填入域名并保存，GitHub 会自动生成 `CNAME` 文件并签发 HTTPS 证书。

然后到 DNS 服务商添加记录：

- **子域名**（如 `luogu.example.com`）→ `CNAME` 记录，指向 `sy666520.github.io`
- **根域名**（如 `example.com`）→ 4 条 `A` 记录，指向：
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```

证书签发需要几分钟到十几分钟，期间访问可能报证书错误，等一会儿再试。

## 本地预览

```bash
python -m http.server 8000
# 浏览器打开 http://localhost:8000
```
