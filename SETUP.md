# 安装指南 (SETUP.md)

## 一、环境要求
- 安装 Go 1.17 或以上版本
- 安装 Make
- 安装 Go Modules

## 二、Make 配置
1. 克隆代码库：
   ```bash
   git clone https://github.com/martintoh96/property-image-processing.git
   cd property-image-processing
   ```
2. 安装依��：
   ```bash
   make install
   ```
3. 构建项目：
   ```bash
   make build
   ```

## 三、Google Sheets 设置
1. 创建一个新的 Google Sheets 文档。
2. 进入“扩展程序” > “Apps Script”。
3. 在底部的代码编辑器中粘贴 API 代码。
4. 保存并命名项目。
5. 进入“文件” > “项目属性”，记录项目的 Web 应用 URL。

## 四、Telegram Bot 设置
1. 在 Telegram 中搜索 "@BotFather"。
2. 发送 `/newbot` 来创建一个新机器人，并按照指示完成设置。
3. 记录你的 API 密钥。
4. 将 API 密钥添加到项目配置文件中。
   ```json
   {
       "telegramBotToken": "YOUR_API_TOKEN"
   }
   ```

## 五、运行项目
- 启动项目：
  ```bash
  make run
  ```

## 六、常见问题
- 如果遇到错误，请检查依赖项是否满足，还原版本配置。

**感谢您使用此项目！**