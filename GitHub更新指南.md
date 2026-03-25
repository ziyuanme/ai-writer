# GitHub在线更新功能设置指南

## 完整操作步骤

### 第一步：创建GitHub仓库

1. 访问 https://github.com/new
2. 仓库名称：`ai-writer`（或你喜欢的名字）
3. 设置为 **Public**（公开仓库）
4. 勾选 "Add a README file"
5. 点击 "Create repository"

### 第二步：上传文件到GitHub

#### 方法A：通过网页上传（推荐新手）

1. 进入你刚创建的GitHub仓库
2. 点击 "Add file" -> "Upload files"
3. 拖拽以下文件到上传区域：
   - `version.json`
   - `README.md`
   - `本地AI写作助手.exe`（打包后的可执行文件）
4. 在 "Commit changes" 框中填写提交信息，如：`Initial release v1.0.0`
5. 点击 "Commit changes"

#### 方法B：通过Git命令行上传

```bash
# 1. 初始化Git仓库
git init

# 2. 添加所有文件
git add .

# 3. 提交更改
git commit -m "Initial release v1.0.0"

# 4. 添加远程仓库（替换为你的GitHub用户名）
git remote add origin https://github.com/你的用户名/ai-writer.git

# 5. 推送到GitHub
git branch -M main
git push -u origin main
```

### 第三步：创建GitHub Release（发布版本）

1. 在GitHub仓库页面，点击右侧的 "Releases"
2. 点击 "Create a new release"
3. 填写以下信息：
   - **Tag version**: `v1.0.0`（注意前面加v）
   - **Release title**: `本地AI写作助手 v1.0.0`
   - **Description**:
     ```
     ## 新功能
     - 支持单篇和批量文章生成
     - 模板管理功能
     - 生成记录管理
     - 在线更新功能
     - 美观的用户界面

     ## 系统要求
     - Windows 10/11
     - 已安装Ollama服务
     - 至少4GB内存
     ```
4. 在 "Binary files" 部分，点击 "Attach binaries"
5. 选择 `本地AI写作助手.exe` 文件
6. 点击 "Publish release"

### 第四步：更新version.json文件

将 `version.json` 中的内容更新为：

```json
{
  "version": "1.0.0",
  "download_url": "https://github.com/你的用户名/ai-writer/releases/latest/download/本地AI写作助手.exe",
  "release_notes": "1. 支持单篇和批量文章生成\n2. 模板管理功能\n3. 生成记录管理\n4. 在线更新功能\n5. 美观的用户界面"
}
```

**重要**：将 `你的用户名` 替换为你的实际GitHub用户名。

### 第五步：测试更新功能

1. 在另一台电脑上安装旧版本的软件
2. 启动软件，点击"检查更新"按钮
3. 软件应该会检测到新版本并提示下载
4. 点击下载后，会打开浏览器访问GitHub的下载页面
5. 下载并安装新版本

## 后续发布新版本的步骤

### 1. 更新软件版本号

在 `main.py` 中修改版本号：

```python
# 在 load_config 方法中找到这行
"version": "1.0.0",  # 改为新版本号，如 "1.0.1"
```

### 2. 重新打包软件

```bash
python build_exe.py
```

### 3. 更新version.json

```json
{
  "version": "1.0.1",  // 新版本号
  "download_url": "https://github.com/你的用户名/ai-writer/releases/latest/download/本地AI写作助手.exe",
  "release_notes": "1. 修复了某个bug\n2. 增加了新功能"  // 更新内容
}
```

### 4. 创建新的GitHub Release

1. 在GitHub仓库中点击 "Releases" -> "Draft a new release"
2. Tag version: `v1.0.1`
3. Release title: `本地AI写作助手 v1.0.1`
4. Description: 填写更新内容
5. 上传新的 `本地AI写作助手.exe`
6. 点击 "Publish release"

### 5. 上传更新后的version.json

将更新后的 `version.json` 文件上传到GitHub仓库的main分支。

## 重要提示

1. **GitHub用户名替换**：所有URL中的 `你的用户名` 都需要替换为你的实际GitHub用户名
2. **版本号格式**：版本号格式为 `主版本.次版本.修订号`，如 `1.0.0`、`1.0.1`、`2.0.0`
3. **文件命名**：确保可执行文件名在所有版本中保持一致
4. **公开仓库**：仓库必须设置为公开，否则用户无法访问
5. **网络连接**：用户需要能够访问GitHub才能使用在线更新功能

## 常见问题

### Q: 用户无法访问GitHub怎么办？
A: 如果用户在中国大陆，GitHub访问可能不稳定。可以考虑使用：
- GitHub镜像站
- CDN加速服务
- 或者在多个平台发布（如Gitee、码云等）

### Q: 如何设置自动更新？
A: 当前版本是手动更新（点击按钮检查）。要实现自动更新，需要：
1. 修改软件代码，在启动时自动检查更新
2. 下载更新文件
3. 自动替换旧版本

### Q: 如何回滚到旧版本？
A: GitHub会保留所有历史版本，用户可以访问：
`https://github.com/你的用户名/ai-writer/releases`
下载任意历史版本。

## 联系方式

如有问题，请联系：
- 作者：子渊
- 网站：https://ziyuan.me
- 微信：7665991