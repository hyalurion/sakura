# Sakura 樱花飘落 Android 应用实现计划

根据 `todo` 文件中的要求和 `index.html` 中的网页示例，本项目旨在开发一个功能完善、性能优异的 Android 樱花飘落悬浮窗应用。

## 核心目标

实现一个在 Android 系统上以悬浮窗形式展示樱花飘落效果的应用，并满足多语言、自定义参数、稳定保活和广泛兼容性的要求。

## 实施阶段划分与详细步骤

### 阶段 1：项目环境准备与浮窗基础实现 (Phase 3)

| 步骤 | 描述 | 关键技术/文件 | 待办事项对应 |
| :--- | :--- | :--- | :--- |
| 1.1 | 确认项目结构，使用 Kotlin 语言进行开发。 | `app/build.gradle.kts` | - |
| 1.2 | 定义应用权限，特别是悬浮窗权限 (`SYSTEM_ALERT_WINDOW`)。 | `app/src/main/AndroidManifest.xml` | 2, 5 |
| 1.3 | 实现基础的 `FloatingService` (Service) 来管理悬浮窗生命周期。 | `app/src/main/kotlin/com/sakura/FloatingService.kt` | 2, 5 |
| 1.4 | 实现悬浮窗的 View (`FloatingView`)，并使用 `WindowManager` 添加到屏幕上。 | `app/src/main/kotlin/com/sakura/FloatingView.kt` | 2 |
| 1.5 | 实现主界面 (`MainActivity`) 用于请求悬浮窗权限和启动/停止服务。 | `app/src/main/kotlin/com/sakura/MainActivity.kt` | - |

### 阶段 2：樱花飘落动画逻辑移植与渲染 (Phase 4)

| 步骤 | 描述 | 关键技术/文件 | 待办事项对应 |
| :--- | :--- | :--- | :--- |
| 2.1 | 将 `index.html` 中的 `Petal` 类逻辑（位置、速度、旋转、摆动）移植到 Kotlin。 | `FloatingView.kt` | 2 |
| 2.2 | 实现樱花花瓣的绘制逻辑。使用 Canvas 绘制 SVG 路径，以提高性能。 | `FloatingView.kt` | 2 |
| 2.3 | 实现动画循环，使用 `Choreographer` 或 `ValueAnimator` 驱动花瓣的 `update()` 和 `draw()` 方法。 | `FloatingView.kt` | 2, 6 |
| 2.4 | 优化绘制性能，确保在大量花瓣下仍能流畅运行（60 FPS）。 | `FloatingView.kt` | 6 |

### 阶段 3：多语言支持、设置界面与主题优化 (Phase 5)

| 步骤 | 描述 | 关键技术/文件 | 待办事项对应 |
| :--- | :--- | :--- | :--- |
| 3.1 | 实现多语言资源文件（英语、日语、简体中文、繁体中文、韩语）。 | `res/values/strings.xml`, `res/values-xx/strings.xml` | 1 |
| 3.2 | 实现设置界面，包含开关服务、调整花瓣密度和速度的滑块。 | `SettingsActivity.kt`, `res/layout/activity_settings.xml` | 4 |
| 3.3 | 使用 `SharedPreferences` 或 `DataStore` 存储用户自定义参数。 | `SettingsManager.kt` | 4 |
| 3.4 | 应用粉色系主题，设计应用图标（仅描述或使用占位符）。 | `res/values/themes.xml`, `res/mipmap/ic_launcher.xml` | 3 |
| 3.5 | 确保所有代码注释使用英语。 | 所有 `.kt` 文件 | 1 |

### 阶段 4：保活机制与多版本兼容性优化 (Phase 6)

| 步骤 | 描述 | 关键技术/文件 | 待办事项对应 |
| :--- | :--- | :--- | :--- |
| 4.1 | 实现前台服务 (`startForeground`)，适配 Android 8.0 (Oreo) 及以上版本。 | `FloatingService.kt` | 5, 6 |
| 4.2 | 实现开机自启动 (`BroadcastReceiver` for `RECEIVE_BOOT_COMPLETED`)。 | `BootReceiver.kt`, `AndroidManifest.xml` | 5 |
| 4.3 | 引导用户将应用加入电池优化白名单（针对 Android 6.0+）。 | `MainActivity.kt` | 5, 6 |
| 4.4 | 检查并适配不同 Android 版本（API 24+）的悬浮窗权限请求和管理。 | `MainActivity.kt` | 6 |

### 阶段 5：最终代码审查、提交与报告 (Phase 7)

| 步骤 | 描述 | 关键技术/文件 | 待办事项对应 |
| :--- | :--- | :--- | :--- |
| 5.1 | 最终代码审查，确保代码质量、性能和注释规范。 | 所有文件 | 1, 6 |
| 5.2 | 提交代码到 GitHub 仓库。 | `git commit`, `git push` | - |
| 5.3 | 向用户报告工作完成情况。 | `message` | - |

## 樱花花瓣 SVG 路径

根据 `todo` 文件和 `index.html`，花瓣的 SVG 路径为：

```xml
<path fill="#f9c1d9" d="M15 2 C12 6, 8 8, 7 13 C6 18, 11 24, 15 28 C19 24, 24 18, 23 13 C22 8, 18 6, 15 2 Z"/>
```

在 Android 中，将使用 `Path` 对象来绘制这个形状。

## 语言支持列表

根据要求，将支持以下语言：

*   English (en)
*   Japanese (ja)
*   Simplified Chinese (zh-rCN)
*   Traditional Chinese (zh-rTW)
*   Korean (ko)

**应用名称固定为“桜”**，无需翻译。
