<details style="display:none">
<summary>AI Agent Notice</summary>
AI collaborators: please read AGENTS.md for project-specific instructions, architecture details, and safety constraints.
</details>

# 空间归档 (QzoneArchive)

[![Rust](https://img.shields.io/badge/Rust-1.77%2B-orange)](https://www.rust-lang.org/)
[![Tauri](https://img.shields.io/badge/Tauri-2.0-blue)](https://v2.tauri.app/)
[![Vue](https://img.shields.io/badge/Vue-3.5-green)](https://vuejs.org/)
[![License](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)

将 QQ 空间动态、照片、视频与互动记录安全归档到本地的桌面 / 移动端工具。

> [!NOTE]
> **衍生版本说明（Modified fork，非官方版本）**
> 本版本基于上游 [Gaoshu705/QzoneArchive](https://github.com/Gaoshu705/QzoneArchive)（GPL-3.0）修改而来，并非上游官方发布。按 GPL-3.0 要求，全部修改后的源码同样以 GPL-3.0 开放，任何人都可在此基础上继续修改或移除本版本新增内容。
> **修改范围**：仅在「概览」首页新增一条可关闭的推广横幅组件 `src/components/PromoBanner.vue`（含二维码与海报弹层，素材位于 `src/assets/promo/`），未改动任何登录、抓取、归档、数据库与导出逻辑。
> 需要官方原版请前往上游仓库获取，请勿将本衍生版与官方版本混淆。

[**详细使用教程**](https://www.bilibili.com/video/BV1p7MZ6xEfk) 
[**网盘下载地址**](https://pan.quark.cn/s/69baf8c8aadc)

> [!CAUTION]
> **近期出现因使用非仓库来源软件而导致账号信息泄露的情况，请务必仔细甄别软件来源。除本仓库发布的内容外，任何其他来源的程序均不可信，请勿下载或使用。**

<a href="https://www.star-history.com/?repos=Gaoshu705%2FQzoneArchive&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=Gaoshu705/QzoneArchive&type=date&theme=dark&legend=top-left&sealed_token=VVJL1S9RMakv50gmYM8C74miiTpiN4O14StqOWLkzBbJNM_ksdUxftRGOvO_1_fnDnEscvd9qj6qqnS-9dOYZkIrJhVYFxgmxN_0xduxtjm1eICUxBdfIQ" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=Gaoshu705/QzoneArchive&type=date&legend=top-left&sealed_token=VVJL1S9RMakv50gmYM8C74miiTpiN4O14StqOWLkzBbJNM_ksdUxftRGOvO_1_fnDnEscvd9qj6qqnS-9dOYZkIrJhVYFxgmxN_0xduxtjm1eICUxBdfIQ" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=Gaoshu705/QzoneArchive&type=date&legend=top-left&sealed_token=VVJL1S9RMakv50gmYM8C74miiTpiN4O14StqOWLkzBbJNM_ksdUxftRGOvO_1_fnDnEscvd9qj6qqnS-9dOYZkIrJhVYFxgmxN_0xduxtjm1eICUxBdfIQ" />
 </picture>
</a>

## 功能

- **完整归档**：还原原始动态正文、图片、视频和评论，按「本人动态」「好友动态」「留言」分类整理
- **断点续传**：中断后自动从上次位置继续，已归档的内容不会丢失
- **频率保护**：每 10 分钟最多请求 300 页，触发限流后安全暂停，倒计时结束即可继续
- **互动还原**：查看每条动态的点赞用户和评论回复，支持互动排行榜
- **本地存储**：所有数据以 SQLite 保存在本地应用数据目录，不上传任何服务器
- **HTML 导出**：支持按分类或选中导出为独立 HTML 文件，可离线浏览
- **媒体时光轴**：按年份浏览归档的照片和视频，视频支持按需缓存
- **暗色模式**：跟随系统或手动切换
- **跨平台**：Windows / macOS / Linux 桌面端 + Android 移动端

## 截图

| 仪表盘 | 归档内容 |
|--------|----------|
| ![仪表盘](public/runtime/仪表盘.png) | ![归档内容](public/runtime/归档内容.png) |

| 媒体时光轴 | 归档任务 |
|-----------|----------|
| ![媒体时光轴](public/runtime/媒体时光轴.png) | ![归档任务](public/runtime/归档任务.png) |

## 技术栈

| 层 | 技术 |
|---|------|
| 桌面框架 | Tauri 2 |
| 前端 | Vue 3 + TypeScript + Vite |
| UI 组件 | PrimeVue 4 |
| 状态管理 | Pinia |
| 后端数据库 | SQLite (rusqlite) |
| HTTP 客户端 | reqwest (rustls-tls) |
| 打包 | NSIS (Windows) / Android APK |

## 开发

### 前置要求

- [Rust](https://www.rust-lang.org/tools/install) 1.77+
- [Node.js](https://nodejs.org/) 20+
- Windows: [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/)（Windows 10+ 自带）
- Android: [Android Studio](https://developer.android.com/studio) + Android SDK + NDK

### 启动开发环境

```bash
# 安装前端依赖
npm install

# 启动开发服务器（桌面端）
npm run tauri dev

# Android 构建
npm run tauri android dev
```

### 构建

```bash
# Windows NSIS 安装包
npm run tauri:build:windows

# Windows NSIS + MSI
npm run tauri:build:windows:all

# Android APK
npm run tauri android build
```

### 项目结构

```
├── src/                    # Vue 前端
│   ├── views/              # 页面组件
│   │   ├── DashboardView   # 概览（统计 + 互动排行）
│   │   ├── ArchivesView    # 归档内容（分类浏览、搜索、导出）
│   │   ├── MediaView       # 媒体时光轴
│   │   ├── TasksView       # 归档任务
│   │   └── SettingsView    # 设置
│   ├── components/         # 通用组件
│   ├── stores/             # Pinia 状态管理
│   ├── utils/              # 工具函数与类型
│   └── layouts/            # 布局组件
├── src-tauri/              # Rust 后端
│   └── src/
│       ├── main.rs         # 入口
│       ├── lib.rs          # Tauri 命令注册
│       ├── qlogin.rs       # QQ 登录（二维码 + 网页）
│       ├── qzone.rs        # QQ 空间接口
│       └── archive.rs      # 归档引擎 + 数据库
└── src-tauri/capabilities/ # Tauri 权限配置
```

## 原理

### 数据来源

归档基于 QQ 空间的**移动端互动列表接口** (`mobile.qzone.qq.com/get_feeds`)。该接口返回当前账号收到的所有互动通知——包括好友发布的新动态、点赞、评论、回复、留言等。程序从中提取原始动态内容并存入本地数据库。

**没有被点赞或评论过的动态无法被恢复**，因为它们不会出现在互动列表中。

### 登录方式

- **二维码登录**：调用 QQ 空间移动端扫码登录流程，全程不接触密码
- **网页登录**（桌面端）：打开独立窗口加载 QQ 登录页，通过 WebView Cookie API 提取登录凭证

登录凭证（Cookie）仅存储在 Rust 后端内存中，不会写入控制台或日志。

## 注意事项

- 请只归档本人或已获得授权的账号内容
- 归档过程中不要切换 QQ 客户端账号，否则可能有冻结风险
- 出现频繁提示时建议换个时间段继续，程序支持断点续传
- QQ 的视频签名有时效性，过期后需要重新归档以更新视频地址
- 数据默认保存在应用数据目录，建议定期将重要资料额外备份

## 免责声明

本软件是用于整理和备份个人 QQ 空间资料的本地工具，与腾讯公司、QQ、QQ 空间及其关联主体不存在隶属、授权、合作关系。使用者应在合法授权范围内使用，并自行承担使用风险。详见应用内《免责声明与使用须知》。

## 赞赏

如果这个项目对你有帮助，欢迎请开发者喝杯咖啡 ☕

| 微信 | 支付宝 |
|------|--------|
| ![微信赞赏](public/sponsor/wx.jpg) | ![支付宝赞赏](public/sponsor/zfb.jpg) |

## 友情链接

* [LINUX DO](https://linux.do/) - 新的理想型社区

## 许可证

本项目采用 [GPLv3](LICENSE) 许可证。
