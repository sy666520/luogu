# 洛谷桌面版 · 下载安装页

静态站点，托管在 GitHub Pages，绑定自定义域名后即为下载页。

## 目录说明

```
index.html              下载安装页
logo.png                站点图标
screenshot.png          界面截图
download/LuoguSetup.exe 安装程序（1.98 MB，内嵌全部程序文件）
CNAME                   GitHub Pages 自定义域名（由 Settings 自动生成，勿手改）
```

## 绑定自定义域名

仓库 Settings → Pages → Custom domain 填入你的域名并保存，GitHub 会自动生成 `CNAME` 文件并签发 HTTPS 证书。

然后到你的 DNS 服务商添加记录：

- **主域名**（如 `luogu.example.com`）→ 添加 `CNAME` 记录，指向 `你的用户名.github.io`
- **根域名**（如 `example.com`）→ 添加 4 条 `A` 记录，指向：
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```

证书签发需要几分钟到十几分钟，期间访问可能报证书错误，等一会儿再试。

## 更新安装包

主程序重新编译后，把新的安装程序覆盖到 `download/LuoguSetup.exe`，提交并推送即可：

```bash
cp "D:\Luogu\洛谷桌面版安装程序.exe" download/LuoguSetup.exe
git add download/LuoguSetup.exe
git commit -m "更新安装包"
git push
```

页面里的「复制直链」按钮会根据当前域名自动生成链接，换域名无需改代码。

## 本地预览

```bash
python -m http.server 8000
# 浏览器打开 http://localhost:8000
```
