---
uid: bcce60d7-f5f4-49eb-b5c7-e6163e67d065
date created: 2026-11-22
aliases: []
date modified: 2026-11-22
---
#  💡Summary  

> [!Info]
> 一句话说清楚
> 



# 🧩 Cues

[[expo]]


# 🪞Notes
这两个东西不在同一层，不是二选一的关系。**Expo（EAS CLI）管的是怎么把 App 做出来**，**App Store Connect CLI（`asc`）管的是 App 做出来以后在 Apple 后台的事**。

## 一句话定位

| | **Expo / EAS CLI** (`eas`) | **App Store Connect CLI** (`asc`) |
|---|---|---|
| 本质 | React Native 开发框架，加上 Expo 的云端构建和发布服务 | 开源 Go 命令行工具，封装了 Apple 官方的 App Store Connect API |
| 出品方 | Expo 公司（不是 Apple） | 社区开源（rorkai/App-Store-Connect-CLI），不是 Apple 官方 |
| 平台 | iOS 和 Android 都支持 | 只支持 Apple 平台（iOS、macOS、tvOS、watchOS、visionOS） |
| 适用对象 | 用 Expo 或 React Native 写的 App | 任何技术栈做的 Apple App（Swift、Flutter、RN 都行） |
| 核心问题 | 写代码、编译、签名、打包、热更新 | 管理 Apple 后台：TestFlight、元数据、提审、发布 |

## 各自能做什么

**Expo / EAS**
- `npx expo start`：本地开发、调试
- `eas build`：在云端编译出 `.ipa` 或 `.apk`/`.aab`，没有 Mac 也能打 iOS 包
- `eas credentials`：自动管理证书和描述文件（Provisioning Profile）
- `eas submit`：把包上传到 App Store Connect 或 Google Play
- `eas update`：OTA 热更新 JS 代码，不用重新提审

**`asc`**
- `asc builds list` 和 `asc publish testflight`：管理构建版本，分发 TestFlight 测试组
- `asc metadata pull/plan/apply`：像管代码一样管商店的描述、截图、多语言
- `asc validate` 和 `asc submit`：检查能否提审，然后提交审核
- 覆盖 1200 多个 API 接口，比如用户、测试员、内购、证书等。输出 JSON，适合 CI 和 AI Agent 调用

## 重叠的地方

两者只有一小段重合：**上传包到 App Store Connect**（`eas submit` 对应 `asc publish`）和**签名证书管理**。EAS 在这部分只做把包送进去这一步。之后的 TestFlight 分组、商店元数据、提审、分阶段发布，EAS 基本不管，正是 `asc` 擅长的。

## 怎么选

- **用 Expo/RN 开发**：用 EAS 打包和提交，再用 `asc` 自动化商店元数据和提审。两者经常一起用。
- **原生 Swift 或 Flutter 项目**：Expo 用不上。打包用 Xcode、`xcodebuild` 或 Fastlane，后台管理用 `asc`。
- **想替代 Fastlane 的 `deliver`/`pilot`**：`asc` 是单个二进制文件，不依赖 Ruby，更轻量。

如果你说的 "apple connect cli" 是指 Apple 官方的工具（`xcrun altool`、`notarytool` 或 Transporter），它们只负责上传和公证，功能比 `asc` 少得多。