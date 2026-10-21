# 暖暖狗儿 (NuanNuanGouer)

基于 SwiftUI 的 iOS 视频聚合播放器，兼容 TVBox / 猫爪 JSON 配置格式，支持多源订阅、多站点切换、视频与音频播放、直播。

> 本项目仅提供播放器框架本身。默认订阅源为 `http://www.y456y.com`（直播立即可用）；点播源由用户自行在 App 内添加。

## 应用信息

| 项 | 值 |
|---|---|
| 应用名 | 暖暖狗儿 |
| Bundle ID | `com.nuannuangouer.tv` |
| 版本 | 1.0.0 (1) |
| 最低系统 | iOS 16.0 |
| 架构 | iPhone / iPad（arm64） |

## 功能特性

- **多源订阅管理**：支持导入 TVBox / 猫爪标准 JSON 配置（URL 订阅）
- **直播**：默认源内置直播频道（m3u8/标准流）
- **点播**：支持 type=0/1（XML/JSON CMS）站点；type=4/JS 采集模块经内置 JavaScriptCore 引擎运行
- **视频播放**：多线路、多集数选择，自动记录并续播进度
- **音频播放**：后台播放、锁屏控制、播放模式切换、定时关闭
- **收藏与历史**：本地收藏夹与播放历史记录
- **深色主题 UI**：默认深色风格

> 说明：iOS 受系统沙盒限制，**不支持 type=3（Android Java Spider/Jar）源**。默认源 y456y 的点播站点均为该类型，需在 App 内自行添加 type=0/1/4 类点播源。

## 云端构建 IPA（无需 Mac）

仓库内置 GitHub Actions 工作流（`.github/workflows/build-ipa.yml`）：

1. 每次推送 / 手动触发时，在 **macOS runner** 上执行 `xcodegen generate` + `xcodebuild archive`（`CODE_SIGNING_ALLOWED=NO`）；
2. 打包为**未签名 IPA**，上传为 Artifact 并创建 GitHub Release；
3. 全程免费（公开仓库 macOS 构建不限时长），不需要 Apple 开发者账号。

本地手动构建（需要 Mac + Xcode 15+）：

```bash
brew install xcodegen
./build_ipa.sh
# 产物：build/ipa/NuanNuanGouer.ipa
```

## 安装到 iPhone（Sideloadly，免费 Apple ID）

1. Windows 电脑安装 **Sideloadly**（sideloadly.io）与**网页版 iTunes & iCloud**（非 Microsoft Store 版）；
2. iPhone 数据线连接电脑，解锁并点“信任”；
3. Sideloadly 拖入下载的 `NuanNuanGouer.ipa`，登录**免费 Apple ID**（仅本地用于签名）；
4. 安装完成后：`设置 → 通用 → VPN与设备管理 → 你的 Apple ID → 信任`；
5. iOS 16+ 需在 `设置 → 隐私与安全性 → 开发者模式` 打开并重启。

**有效期**：免费 Apple ID 签名 **7 天**有效。Sideloadly 开启"自动刷新"后，电脑与手机同网络会到期前自动续签；也可每周手动重拖一次 IPA 刷新。付费开发者账号（$99/年）可延长至 1 年。

## 源码结构

```
NuanNuanGouer/            # SwiftUI 源码（App 入口 / 视图 / 视图模型 / 服务 / 模型）
project.yml               # XcodeGen 工程定义（Bundle ID、版本、Info.plist 键值）
build_ipa.sh              # 本地未签名 IPA 构建脚本
.github/workflows/        # GitHub Actions 云端构建
```

## 许可证与署名

- 播放器框架基于 **yangxiying/MyTVBox**（MIT License）修改，保留其版权声明，见 [LICENSE](LICENSE)；
- 本仓库为修改版，以 MIT 许可分发；
- 内置引擎依赖 Apple JavaScriptCore（系统框架）；
- TVBox / 猫爪配置格式为社区开放格式，配置内容由订阅源提供方负责，本项目不内置、不分发任何内容。

## 免责声明

本项目仅供个人学习与技术研究使用。用户自行添加的订阅源及其内容与本项目无关，请遵守当地法律法规，并于试用后 24 小时内自行删除。
