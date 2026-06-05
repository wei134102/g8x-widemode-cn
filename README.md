# WideMode for LG（LG 宽屏模式）

[English](#english) | [中文](#中文)

LG 双屏手机的 **Wide Mode（宽屏模式）** 切换工具。通过反射调用 LG 系统 API，在副屏（Cover Display）上快速开启或关闭宽屏显示。

Fork 自 [tmyt/g8x-widemode](https://github.com/tmyt/g8x-widemode)，增加了**简体中文**界面与 GitHub Actions 自动构建。

---

## 中文

### 简介

本应用面向 LG 双屏机型（如 **LG G8 ThinQ**、**LG V50 ThinQ** 等），用于在副屏上切换 **Wide Mode**。开启后，副屏上的应用可以横向铺满显示，获得更宽的视野。

应用本身不提供复杂界面，主要通过以下方式使用：

- 快捷设置磁贴（Quick Settings Tile）
- LG QSlide 菜单
- Tasker / Locale 插件自动化

界面语言跟随系统：支持**简体中文**、**日语**和**英语**。

### 适用设备

- LG 双屏手机，且系统提供 `com.lge.sui` 框架
- Android 9（API 28）及以上
- **仅能在真机上运行**，模拟器无法测试宽屏模式

> 若设备不支持，应用会提示「您的设备不支持宽屏模式」。

### 安装

1. 从 [Releases](https://github.com/wei134102/g8x-widemode-cn/releases) 或 GitHub Actions 构建产物下载 APK
2. 在 LG 双屏手机上安装
3. 按下方「使用前准备」完成系统设置

### 使用前准备

切换宽屏模式前，需满足以下**任一**条件：

| 方式 | 说明 |
|------|------|
| **推荐** | 进入系统 **设置 → 显示 → 副屏**，开启 **「与主屏幕保持相同亮度」**（Keep the same as main screen） |
| 高级 | 通过 ADB 授予 `WRITE_SECURE_SETTINGS` 权限（见下文） |
| 实验性 | 在应用设置中开启 **「忽略系统设置检查」** |

未满足条件时，点击磁贴会提示：

> 请在系统设置中开启「与主屏幕保持相同亮度」。

### 使用方法

#### 1. 快捷设置磁贴

1. 从屏幕顶部下拉打开快捷设置
2. 点击 **编辑** / **添加磁贴**
3. 找到 **「宽屏模式」**（Wide Mode）并添加
4. 点击磁贴即可切换宽屏模式开/关

磁贴状态说明：

| 状态 | 含义 |
|------|------|
| 灰色（未激活） | 宽屏模式关闭 |
| 高亮（激活） | 宽屏模式开启 |
| 不可用 | 副屏未启用 |

#### 2. QSlide 菜单

在 LG QSlide 应用列表中找到 **「宽屏模式」** 图标，点击即可切换。

#### 3. Tasker / Locale 插件

1. 在 Tasker 中添加 **Locale / Tasker Plugin** 动作
2. 选择 **「切换宽屏模式」**
3. 选择模式：**开启** / **关闭** / **切换**

### 应用设置

打开桌面上的 **WideMode for LG** 应用进入设置页：

| 选项 | 说明 |
|------|------|
| **忽略系统设置检查**（实验性功能） | 跳过「与主屏幕保持相同亮度」等前置检查，强制允许切换。仅在系统设置无法满足时使用 |

### ADB 授权（可选）

若无法或不方便修改系统显示设置，可通过 ADB 授予安全设置写入权限：

```bash
adb shell pm grant net.refy.android.g8x.widemode android.permission.WRITE_SECURE_SETTINGS
```

撤销权限：

```bash
adb shell pm revoke net.refy.android.g8x.widemode android.permission.WRITE_SECURE_SETTINGS
```

### 常见问题

**Q：点击磁贴没有反应，或提示需要开启系统设置？**  
A：请先开启「与主屏幕保持相同亮度」，或在设置中启用「忽略系统设置检查」。

**Q：提示设备不支持？**  
A：本应用仅支持 LG 双屏机型，且依赖 LG 私有 API，其他品牌或单屏手机无法使用。

**Q：副屏未打开时磁贴不可用？**  
A：这是正常行为，副屏启用后才能切换宽屏模式。

### 从源码构建

#### 环境要求

- JDK 11
- Android SDK（API 29，Build Tools 29.0.3）
- 配置 `local.properties`：

```properties
sdk.dir=/path/to/Android/Sdk
```

#### 本地编译

```bash
# Windows
gradlew.bat assembleDebug

# Linux / macOS
./gradlew assembleDebug
```

输出 APK 位于：

```
app/build/outputs/apk/debug/app-debug.apk
```

Release 版本：

```bash
./gradlew assembleRelease
```

#### GitHub Actions 自动构建

推送至 `master` 或 `main` 分支后，[Actions](https://github.com/wei134102/g8x-widemode-cn/actions) 会自动：

1. 安装 Android SDK
2. 编译 Debug APK
3. 运行单元测试
4. 上传 APK 为 Artifact（可在对应 Workflow Run 页面下载）

### 语言支持

| 语言 | 资源目录 |
|------|----------|
| 英语（默认） | `values/strings.xml` |
| 简体中文 | `values-zh-rCN/strings.xml` |
| 日语 | `values-ja/strings.xml` |

---

## English

### Introduction

A **Wide Mode** toggle utility for LG dual-screen phones. It uses reflection to call LG system APIs and switch wide-screen display on the cover (secondary) display.

Forked from [tmyt/g8x-widemode](https://github.com/tmyt/g8x-widemode) with **Simplified Chinese** localization and GitHub Actions CI.

### Features

- Quick Settings tile for one-tap toggle
- QSlide integration
- Tasker / Locale plugin (ON / OFF / Toggle)
- Simplified Chinese, Japanese, and English UI

### Supported Devices

- LG dual-screen phones with `com.lge.sui` framework (e.g. LG G8 ThinQ, LG V50 ThinQ)
- Android 9 (API 28)+
- **Real device only** — emulators cannot test Wide Mode

### Installation

1. Download APK from [Releases](https://github.com/wei134102/g8x-widemode-cn/releases) or GitHub Actions artifacts
2. Install on your LG dual-screen phone
3. Complete the prerequisites below

### Prerequisites

At least **one** of the following must be satisfied before switching Wide Mode:

| Method | Description |
|--------|-------------|
| **Recommended** | **Settings → Display → Cover display** → enable **"Keep the same as main screen"** |
| Advanced | Grant `WRITE_SECURE_SETTINGS` via ADB (see below) |
| Experimental | Enable **"Ignore system settings check"** in app settings |

### Usage

#### Quick Settings Tile

1. Pull down the notification shade
2. Edit tiles and add **"Wide Mode"**
3. Tap the tile to toggle Wide Mode on/off

#### QSlide

Find **"Wide Mode"** in the LG QSlide app list and tap to toggle.

#### Tasker / Locale Plugin

1. Add a **Locale / Tasker Plugin** action in Tasker
2. Select **"Switch Wide Mode"**
3. Choose **Turn ON**, **Turn OFF**, or **Toggle**

### App Settings

Launch **WideMode for LG** from the app drawer:

| Option | Description |
|--------|-------------|
| **Ignore system settings check** (Experimental) | Skip the brightness-sync prerequisite and allow switching anyway |

### ADB Permission (Optional)

```bash
adb shell pm grant net.refy.android.g8x.widemode android.permission.WRITE_SECURE_SETTINGS
```

Revoke:

```bash
adb shell pm revoke net.refy.android.g8x.widemode android.permission.WRITE_SECURE_SETTINGS
```

### Build from Source

**Requirements:** JDK 11, Android SDK API 29

```bash
./gradlew assembleDebug
```

APK output: `app/build/outputs/apk/debug/app-debug.apk`

CI builds run automatically on push to `master`/`main` via [GitHub Actions](https://github.com/wei134102/g8x-widemode-cn/actions).

### FAQ

**Q: Tile does nothing or shows a settings error?**  
A: Enable "Keep the same as main screen" in system settings, or use the experimental ignore option.

**Q: "Not Supported" dialog?**  
A: This app only works on LG dual-screen devices with LG private APIs.

---

## License

MIT License — see [LICENSE](LICENSE).

Original project © 2019 [Yutaka Tsumori (tmyt)](https://github.com/tmyt/g8x-widemode).
