# AI Browser - 部署指南

本指南将详细介绍如何将AI Browser项目部署到GitHub并使用GitHub Actions生成APK文件。

## 1. 创建GitHub仓库

1. 登录GitHub账户
2. 点击"New repository"按钮
3. 输入仓库名，例如："ai-browser"
4. 选择"Public"或"Private"（根据需要）
5. 点击"Create repository"

## 2. 上传项目代码

1. 打开终端/命令提示符，进入项目根目录：
   ```bash
   cd /path/to/your/ai-browser-project
   ```

2. 初始化git仓库：
   ```bash
   git init
   git add .
   git commit -m "Initial commit: AI Browser project"
   ```

3. 连接远程仓库（替换 YOUR_USERNAME 为你的GitHub用户名）：
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/ai-browser.git
   ```

4. 推送代码：
   ```bash
   git branch -M main
   git push -u origin main
   ```

## 3. GitHub Actions构建配置

项目已包含GitHub Actions工作流配置文件 `.github/workflows/android_build.yml`，它将自动：

1. 设置Java开发环境
2. 配置Android SDK
3. 构建项目
4. 生成debug和release版本的APK文件
5. 上传APK作为构建产物

## 4. 查看构建结果

1. 在GitHub仓库页面，点击"Actions"标签
2. 选择最近的构建工作流
3. 等待构建完成
4. 构建成功后，可在"Artifacts"部分下载APK文件

## 5. APK文件说明

构建过程将生成两个APK文件：
- `app-debug-apk`: 调试版本，用于测试
- `app-release-apk`: 发布版本，用于分发

## 6. 可选：配置签名（用于发布版本）

如果你想为release版本APK添加签名，请在GitHub仓库的Settings -> Secrets and variables -> Actions中添加以下密钥：

- `SIGNING_KEY`: Base64编码的签名密钥
- `SIGNING_PASSWORD`: 签名密码
- `KEYSTORE_PASSWORD`: 密钥库密码
- `KEY_ALIAS`: 密钥别名

## 7. 故障排除

### 构建失败
- 检查代码中是否有语法错误
- 确认所有必需的文件都已提交
- 查看GitHub Actions日志以获取详细错误信息

### APK下载问题
- 确保工作流运行成功完成
- 检查是否有权限下载构建产物
- 确认没有下载限制

## 8. 项目维护

- 定期更新依赖库以获得最新功能和安全修复
- 测试不同Android版本的兼容性
- 优化UI/UX设计以提升用户体验

## 9. 扩展功能

AI Browser项目可以进一步扩展：
- 添加书签功能
- 实现历史记录管理
- 集成搜索建议
- 添加夜间模式
- 实现下载管理器
- 增加广告拦截功能

## 10. 技术支持

如遇到问题，请参考：
- GitHub Actions日志
- Android开发文档
- Gradle构建文档

本项目遵循开源软件最佳实践，欢迎提交Issue和Pull Request。
