# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 提供在此代码库中工作的指导。

## 项目概述

Motrix 是一个基于 Electron、Vue.js 和 Aria2 构建的全功能下载管理器。支持 HTTP、FTP、BitTorrent、磁力链接和其他下载协议。

## 开发命令

### 核心开发
- `yarn run dev` - 启动带热重载的开发模式
- `yarn run build` - 构建生产应用
- `yarn run build:applesilicon` - 为 Apple Silicon (ARM64) 构建
- `yarn run build:dir` - 构建但不打包

### 代码质量
- `yarn run lint` - 在源文件上运行 ESLint
- `yarn run lint:fix` - 自动修复 ESLint 问题

### Webpack 构建
- `yarn run pack` - 构建主进程和渲染进程
- `yarn run pack:main` - 仅构建主进程
- `yarn run pack:renderer` - 仅构建渲染进程

## 架构

### 主进程 (Electron)
位于 `src/main/`:
- `Application.js` - 管理所有组件的核心应用类
- `Launcher.js` - 应用启动器和单例管理
- `core/` - 核心服务 (Engine、Config、Update 等)
- `ui/` - UI 管理器 (Window、Menu、Tray、Theme 等)

### 渲染进程 (Vue.js)
位于 `src/renderer/`:
- Vue 2.x 配合 Vuex 进行状态管理
- Element UI 组件库
- 按功能组织的页面和组件

### 共享代码
位于 `src/shared/`:
- 常量和配置键
- Aria2 客户端实现
- 国际化 (i18n) 支持

### 关键组件
- **Engine**: 通过 JSON-RPC 管理 Aria2 下载引擎
- **ConfigManager**: 处理用户和系统配置
- **WindowManager**: 管理应用窗口
- **TrayManager**: 系统托盘集成
- **ProtocolManager**: 处理自定义协议 (磁力链接、种子等)

## 构建系统

- 使用 `.electron-vue/` 中的自定义 webpack 配置
- 主进程和渲染进程分别构建
- 平台特定构建由 electron-builder 处理
- Aria2 二进制文件包含在平台特定的 `extra/` 目录中

## 开发说明

- 使用 Electron 22.x 和 Node.js >= 16.0.0
- Vue 2.x 配合 Vuex 进行状态管理
- 通过 i18next 实现国际化
- 使用 electron-store 存储配置
- Aria2 引擎通过 WebSocket 上的 JSON-RPC 通信
- 开发服务器运行在端口 9080