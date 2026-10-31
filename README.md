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

## 首次部署

### 方式一：网页上传（不需要命令行）

1. GitHub 新建仓库，名字填 `luogu`，选 Public，**不要勾** README / .gitignore / License
2. 进入新仓库，点 `uploading an existing file`
3. 把 `index.html`、`logo.png`、`screenshot.png`、`README.md` 拖进去，
   再新建文件 `download/LuoguSetup.exe`（路径里带斜杠会自动建目录）——
   或者直接把整个文件夹拖进浏览器，会保留目录结构
4. 提交后进入 Settings → Pages → Source 选 `Deploy from a branch`，
   Branch 选 `main`、目录 `/ (root)`，保存
5. 等 1~2 分钟，访问 https://sy666520.github.io/luogu/

### 方式二：命令行推送

```bash
cd D:\Luogu\GitHub\luogu
git push -u origin main
```

首次推送会要求登录。GitHub 已不支持密码，需要 Personal Access Token（PAT）：

- 生成：GitHub → Settings → Developer settings → Personal access tokens →
  Tokens (classic) → Generate new token，勾选 `repo` 权限
- 推送时用户名填 `sy666520`，密码位置粘贴 token

或者安装 [Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager)，
推送时会弹浏览器登录，更省事。

## 更新安装包

主程序重新编译后，覆盖 `download/LuoguSetup.exe` 并推送：

```bash
cd D:\Luogu\GitHub\luogu
cp "D:\Luogu\洛谷桌面版安装程序.exe" download/LuoguSetup.exe
git add download/LuoguSetup.exe
git commit -m "更新安装包"
git push
```

Pages 会在 1 分钟左右重新构建。

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

## 备用地址

`github.io` 在国内访问不够稳定，有时慢或打不开。
主下载页仍保留在：https://luogu-desktop-setup.app.workbuddy.host/

## 本地预览

```bash
python -m http.server 8000
# 浏览器打开 http://localhost:8000
```
