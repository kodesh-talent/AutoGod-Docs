# AutoGod 文档中心

> AutoGod 脚本 API 与 UI 框架的中文文档索引。
>
> 本文档库覆盖自动化控制、图色与 AI 识别、文件与数据、网络通信、界面开发等能力。

[![文档](https://img.shields.io/badge/文档-中文-blue)](#api-参考)
[![English](https://img.shields.io/badge/docs-English-lightgrey)](api_en/ag.md)
[![UI](https://img.shields.io/badge/UI-Material%203-6750A4)](ui_cn/index.md)

## 项目简介

AutoGod-Docs 是 AutoGod 的配套文档仓库，当前包含四个文档分区：

| 分区 | 内容 | 文档数量 |
| --- | --- | ---: |
| [`api_cn`](api_cn/ag.md) | 中文 API 参考，按脚本对象、数据类型和专题组织 | 97 |
| [`api_en`](api_en/ag.md) | 英文目录的 API 参考，结构同中文目录 | 97 |
| [`ui_cn`](ui_cn/index.md) | 中文 UI 框架、布局、控件和示例 | 83 |
| [`ui_en`](ui_en/index.md) | 英文目录的 UI 框架文档 | 83 |

> 本仓库只包含文档与配图，不包含 AutoGod 客户端或可执行程序。
>
> `api_en`、`ui_en` 与中文目录一一对应，但部分英文页面可能仍保留中文说明，实际内容以页面正文为准。

## 快速导航

| 我想…… | 建议从这里开始 |
| --- | --- |
| 了解 UI 框架的整体设计 | [UI 框架总览](ui_cn/index.md) → [XView 控件父类](ui_cn/XView.md) |
| 创建第一个界面 | [界面交互 `$ui`](ui_cn/ui.md) → [UI 界面对象](ui_cn/ui/UI.md) |
| 学习布局写法 | [布局父类](ui_cn/layout.md) → [线性布局](ui_cn/layout/linear.md) |
| 查找某个控件 | [控件速查](#控件速查) |
| 实现点击、滑动和按键 | [`$act` 手势动作](api_cn/act.md) → [`$touch` 触摸驱动](api_cn/touch.md) |
| 实现找图、找色 | [`$ag` 图色框架](api_cn/ag.md) → [`$img` 图片操作](api_cn/img.md) |
| 实现 OCR 或目标检测 | [`$ocr` 文字识别](api_cn/ocr.md) → [`$yolo` 目标检测](api_cn/yolo.md) |
| 发起网络请求 | [`$http` 网络请求](api_cn/http.md) → [`$ws` WebSocket](api_cn/ws.md) |
| 读写文件或数据库 | [`$file` 文件系统](api_cn/file.md) → [`$sqlite` 数据库](api_cn/sqlite.md) |
| 编写多线程或定时任务 | [`$thread` 并发编程](api_cn/thread.md) → [`$timer` 定时任务](api_cn/timer.md) |

## 推荐阅读路径

### 路径一：从零开始开发 UI

1. 先阅读 [UI 框架总览](ui_cn/index.md)，了解 Material 3 扩展和控件体系。
2. 阅读 [XView 控件父类](ui_cn/XView.md) 与 [布局父类](ui_cn/layout.md)，理解公共属性和布局继承关系。
3. 从 [线性布局](ui_cn/layout/linear.md) 或 [相对布局](ui_cn/layout/relative.md) 开始搭建页面。
4. 参考 [按钮](ui_cn/button.md) 与 [按钮综合案例](ui_cn/button/demo.md) 添加交互。
5. 使用 [`$ui` 界面交互](ui_cn/ui.md) 显示页面，用 [UI 界面对象](ui_cn/ui/UI.md) 查找和操作控件。
6. 需要底部弹窗时阅读 [Sheet 底部弹窗](ui_cn/ui/Sheet.md)。

### 路径二：开发自动化脚本

1. [手势动作 `$act`](api_cn/act.md) 负责点击、滑动和按键，复杂轨迹见 [手势路径](api_cn/ActPath.md)。
2. 权限与输入方式可进一步查看 [`$touch`](api_cn/touch.md)、[`$hid`](api_cn/hid.md)、[`$root`](api_cn/root.md) 和 [`$szk`](api_cn/szk.md)。
3. 使用 [`$ag` 图色框架](api_cn/ag.md) 完成找图、找色和多点找色。
4. 使用 [`$img`](api_cn/img.md) 处理图片，使用 [`$ocr`](api_cn/ocr.md) 识别文字，使用 [`$yolo`](api_cn/yolo.md) 做目标检测。
5. 用 [`$draw`](api_cn/draw.md) 标记识别结果，或用 [`$floaty`](api_cn/floaty.md) 显示悬浮控件。
6. 用 [`$event`](api_cn/event.md) 监听系统事件，用 [`$thread`](api_cn/thread.md) 管理耗时任务。

### 路径三：应用、文件与数据处理

1. 使用 [`$app`](api_cn/app.md) 启动、停止和查询应用。
2. 使用 [`$file`](api_cn/file.md)、[`$res`](api_cn/res.md) 和 [`$storage`](api_cn/storage.md) 管理文件与配置。
3. 使用 [`$sqlite`](api_cn/sqlite.md) 或 [`$excel`](api_cn/excel.md) 保存结构化数据。
4. 使用 [`$http`](api_cn/http.md)、[`$ws`](api_cn/ws.md) 和 [`$html`](api_cn/html.md) 接入网络服务。
5. 使用 [`$crypt`](api_cn/crypt.md)、[`$str`](api_cn/str.md)、[`$date`](api_cn/date.md) 处理文本、时间和加密数据。

### 路径四：扩展脚本能力

1. 用 [`$engine`](api_cn/engine.md) 运行和管理脚本任务。
2. 用 [`$thread`](api_cn/thread.md)、[`$timer`](api_cn/timer.md) 组织并发与定时逻辑。
3. 用 [`$plugin`](api_cn/plugin.md) 加载插件 App，用 [`$ext`](api_cn/ext.md) 加载 Dex、APK、JAR 或 SO。
4. 使用 [`$log`](api_cn/log.md) 排查问题，使用 [`$mem`](api_cn/mem.md) 进行内存读写。
5. Web 插件开发参见 [Web 插件引擎](api_cn/web-plugin/engine.md)、[文件管理](api_cn/web-plugin/file.md) 和 [日志](api_cn/web-plugin/log.md)。

## API 参考

API 文档以脚本中的全局对象命名。例如 [`api_cn/ag.md`](api_cn/ag.md) 对应脚本里的 `$ag`。对象目录下的其他文件通常是配置类型、结果类型或配套专题。

### 自动化与设备控制

| 入口 | 能力简介 | 关联文档 |
| --- | --- | --- |
| [`$act` 手势动作](api_cn/act.md) | 点击、长按、滑动、按键及手势路径 | [手势路径](api_cn/ActPath.md)、[Node 节点信息](api_cn/act/Node.md)、[UiSelector 选择器](api_cn/act/UiSelector.md) |
| [`$touch` 触摸驱动](api_cn/touch.md) | 基于无障碍服务的点击、长按、滑动和按键 | — |
| [`$hid` 键鼠触控](api_cn/hid.md) | 通过外接 HID 设备模拟输入 | — |
| [`$root` Root 与 Shell](api_cn/root.md) | Root 权限检查、Shell 命令和系统操作 | — |
| [`$szk` Shizuku 工具](api_cn/szk.md) | 通过 Shizuku 执行系统级操作 | — |
| [`AccessibilityNodeInfo`](api_cn/AccessibilityNodeInfo.md) | 安卓无障碍节点信息 | — |
| [`$screen` 屏幕操作](api_cn/screen.md) | 截图、分辨率、旋转和屏幕信息 | [ScreenInfo 屏幕信息](api_cn/screen/ScreenInfo.md) |
| [`$adapt` 坐标适配](api_cn/adapt.md) | 按屏幕配置换算坐标和图片尺寸 | — |
| [`$event` 事件监听](api_cn/event.md) | 系统、无障碍和应用内部事件监听 | — |
| [`$app` 应用操作](api_cn/app.md) | 启动、停止、查询应用与任务 | [AppInfo 应用信息](api_cn/app/AppInfo.md)、[AppTaskInfo 任务信息](api_cn/app/AppTaskInfo.md) |
| [`$device` 设备信息](api_cn/device.md) | 读取设备标识、硬件和系统信息 | — |
| [`$sys` 系统工具](api_cn/sys.md) | 系统级辅助功能 | — |
| [`$permit` 权限工具](api_cn/permit.md) | 查询和申请运行时权限 | — |
| [`$global` 全局函数](api_cn/global.md) | 等待、提示、剪贴板、前台应用等常用函数 | — |

### 图色识别、视觉与绘制

| 入口 | 能力简介 | 关联文档 |
| --- | --- | --- |
| [`$ag` 图色框架](api_cn/ag.md) | 找图、找色、多点找色、多目标匹配和血条识别 | [AgMoreResult 多个结果](api_cn/AgMoreResult.md) |
| [`$img` 图片操作](api_cn/img.md) | 读取、保存、裁剪、缩放、旋转、拼接和模糊 | [ImageInfo 图片信息](api_cn/ImageInfo.md)、[Image 图片对象](api_cn/img/Image.md) |
| [`$ocr` 文字识别](api_cn/ocr.md) | 屏幕或图片文字识别 | [OcrOptions 识别配置](api_cn/ocr/OcrOptions.md)、[DetectResult 结果](api_cn/ocr/DetectResult.md)、[DetectResultItem 结果项](api_cn/ocr/DetectResultItem.md) |
| [`$yolo` 目标检测](api_cn/yolo.md) | 创建检测器并在屏幕或图片上识别目标 | [YoloObject](api_cn/yolo/YoloObject.md)、[YoloResult](api_cn/yolo/YoloResult.md)、[YoloResultCell](api_cn/yolo/YoloResultCell.md) |
| [`$canvas` 画布](api_cn/canvas.md) | 创建画布、画笔、矩形和矩阵进行图片绘制 | [XCanvas 画布对象](api_cn/canvas/XCanvas.md) |
| [`$draw` 全屏绘制](api_cn/draw.md) | 在屏幕最上层绘制框、点、文字、圆和路径 | — |
| [`$color` 颜色操作](api_cn/color.md) | 颜色解析、转换与比较 | — |
| [`Point` 点对象](api_cn/opencv/Point.md) | 识别和绘图常用的二维坐标类型 | [Rect 范围对象](api_cn/opencv/Rect.md) |

YOLO 进阶资料：

- [训练模型：环境搭建](api_cn/yolo/a_train1.md)
- [输入输出层名称对照表](api_cn/yolo/io_names.md)
- [结果排序规则表](api_cn/yolo/result_sort.md)

### 悬浮窗与屏幕叠加

| 入口 | 能力简介 | 关联文档 |
| --- | --- | --- |
| [`$floaty` 悬浮窗](api_cn/floaty.md) | 应用级、系统级、可调节悬浮窗和区域选择 | [AppFloaty](api_cn/floaty/AppFloaty.md)、[SysFloaty](api_cn/floaty/SysFloaty.md)、[AdjFloaty](api_cn/floaty/AdjFloaty.md)、[SelectFloaty](api_cn/floaty/SelectFloaty.md) |
| [`$arc` 悬浮球](api_cn/arc.md) | 扇形悬浮菜单、按钮容器和菜单项 | [MenuBody 按钮容器](api_cn/arc/MenuBody.md)、[MenuItem 悬浮按钮](api_cn/arc/MenuItem.md) |
| [`$tip` 阻塞式对话框](api_cn/tip.md) | 信息、输入、确认、列表、日期和时间弹窗 | [alert 原生对话框](api_cn/tip/alert.md)、[dialog M3 对话框](api_cn/tip/dialog.md) |

### 文件、数据与媒体

| 入口 | 能力简介 | 关联文档 |
| --- | --- | --- |
| [`$file` 文件系统](api_cn/file.md) | 文件和目录的读写、复制、移动与遍历 | — |
| [`$res` 资源管理器](api_cn/res.md) | 访问应用内置资源 | — |
| [`$storage` 应用内存储](api_cn/storage.md) | 保存脚本配置和轻量数据 | — |
| [`$sqlite` 轻量数据库](api_cn/sqlite.md) | 创建、查询和更新 SQLite 数据库 | — |
| [`$excel` 表格操作](api_cn/excel.md) | 读取和写入 Excel 表格 | — |
| [`$fc` 文件选择器](api_cn/fc.md) | 选择文件或目录 | [FcConfig 文件选择配置](api_cn/fc/FcConfig.md) |
| [`$media` 媒体播放](api_cn/media.md) | 播放本地音频和资源音频 | — |
| [`$tts` 语音阅读](api_cn/tts.md) | 文本转语音 | [TtsOptions 语音配置](api_cn/tts/TtsOptions.md) |
| [`AudioInfo` 音频信息](api_cn/AudioInfo.md) | 音频元数据与属性 | — |
| [`VideoInfo` 视频信息](api_cn/VideoInfo.md) | 视频元数据与属性 | — |

### 网络、文本与安全

| 入口 | 能力简介 | 关联文档 |
| --- | --- | --- |
| [`$http` 网络请求](api_cn/http.md) | HTTP 请求、上传和下载 | [HttpOptions 请求配置](api_cn/http/HttpOptions.md)、[HttpResponse 响应体](api_cn/http/HttpResponse.md) |
| [`$ws` WebSocket](api_cn/ws.md) | 双向实时通信 | [Ws 封装对象](api_cn/ws/Ws.md) |
| [`$html` 网页操作](api_cn/html.md) | 解析和操作 HTML | — |
| [`$bus` 消息总线](api_cn/bus.md) | 脚本内部发布、订阅和解耦 | — |
| [`$str` 字符串操作](api_cn/str.md) | 字符串查找、替换、分割和编码 | — |
| [`$date` 日期工具](api_cn/date.md) | 日期时间格式化与计算 | [DateInfo 日期信息](api_cn/date/DateInfo.md) |
| [`$crypt` 加密算法](api_cn/crypt.md) | 摘要、加解密和编码 | [CryptKey](api_cn/CryptKey.md)、[CryptKeyPair](api_cn/CryptKeyPair.md)、[CryptOptions](api_cn/CryptOptions.md) |
| [`$qr` 二维码工具](api_cn/qr.md) | 二维码生成与识别 | [QrOptions 制作配置](api_cn/qr/QrOptions.md) |

### 脚本、并发与扩展

| 入口 | 能力简介 | 关联文档 |
| --- | --- | --- |
| [`$engine` 脚本引擎](api_cn/engine.md) | 运行脚本、执行代码和管理任务 | [JsTaskInfo 任务信息](api_cn/engine/JsTaskInfo.md)、[`$task` 脚本任务](api_cn/engine/task.md) |
| [`$thread` 并发编程](api_cn/thread.md) | 后台任务、循环器、线程管理和界面线程 | [Threadx 增强线程](api_cn/thread/Threadx.md)、[CdLock 倒计时锁](api_cn/thread/CdLock.md) |
| [`$timer` 定时任务](api_cn/timer.md) | 定时和重复执行脚本 | — |
| [`$log` 日志框架](api_cn/log.md) | 输出、保存和管理运行日志 | — |
| [`$plugin` 插件系统](api_cn/plugin.md) | 加载独立插件 App 并调用其能力 | — |
| [`$ext` 扩展加载](api_cn/ext.md) | 加载 Dex、APK、JAR 和 SO | [LoadExtConfig](api_cn/ext/LoadExtConfig.md)、[LoadSoConfig](api_cn/ext/LoadSoConfig.md) |
| [`$mem` 内存读写](api_cn/mem.md) | 内存扫描与读写 | — |
| [`$engine` Web 插件引擎](api_cn/web-plugin/engine.md) | Web 插件环境中的脚本执行能力 | [文件管理](api_cn/web-plugin/file.md)、[日志](api_cn/web-plugin/log.md) |

## UI 开发

UI 框架基于 Google [Material 3](https://m3.material.io/) 扩展，封装了常用布局、控件和组件式界面。所有视图都继承自 [`XView`](ui_cn/XView.md)，所有布局都继承自 [`XLayout`](ui_cn/layout.md)。

### 入门与基础

| 文档 | 说明 |
| --- | --- |
| [UI 框架总览](ui_cn/index.md) | 框架设计、演示视频与整体结构 |
| [`$ui` 界面交互](ui_cn/ui.md) | 界面线程、解析布局、显示弹窗和界面工具 |
| [UI 界面对象](ui_cn/ui/UI.md) | 获取视图、查找控件及页面级操作 |
| [Sheet 底部弹窗](ui_cn/ui/Sheet.md) | 解析和显示底部弹窗 |
| [XView 控件父类](ui_cn/XView.md) | 所有控件的公共属性、事件和方法 |
| [布局父类](ui_cn/layout.md) | 所有布局的公共能力和子视图管理 |
| [颜色属性对照表](ui_cn/other/color.md) | 常用颜色值参考 |
| [重力属性对照表](ui_cn/other/gravity.md) | `gravity` 对齐属性参考 |
| [补充文档](ui_cn/other.md) | 其他 UI 使用说明与补充资料 |

### 布局

| 布局 | 说明 |
| --- | --- |
| [绝对布局](ui_cn/layout/absolute.md) | 按绝对坐标放置子视图 |
| [卡片布局](ui_cn/layout/card.md) | Material 卡片容器 |
| [约束布局](ui_cn/layout/const.md) | 通过约束关系确定位置和尺寸 |
| [锚点布局](ui_cn/layout/coord.md) | 围绕锚点组织控件 |
| [抽屉布局](ui_cn/layout/drawer.md) | 侧边抽屉导航 |
| [折叠布局](ui_cn/layout/expand.md) | 可展开和收起的内容区域 |
| [流式布局](ui_cn/layout/flow.md) | 子视图自动换行排列 |
| [刷新布局](ui_cn/layout/flush.md) | 支持下拉刷新 |
| [帧布局](ui_cn/layout/frame.md) | 子视图层叠放置 |
| [网格布局](ui_cn/layout/grid.md) | 行列网格排列 |
| [包含布局](ui_cn/layout/include.md) | 复用其他布局文件 |
| [线性布局](ui_cn/layout/linear.md) | 水平或垂直排列 |
| [滑动布局](ui_cn/layout/nested.md) | 嵌套滚动内容 |
| [相对布局](ui_cn/layout/relative.md) | 按兄弟控件或父容器定位 |
| [滚动布局](ui_cn/layout/scroll.md) | 单方向滚动容器 |

布局示例：[折叠文本案例](ui_cn/layout/expand/demo_expand_more_desc.md)。

### 控件速查

| 控件 | 说明 | 相关文档与示例 |
| --- | --- | --- |
| [应用条](ui_cn/appbar.md) | 顶部标题、菜单与操作区 | [应用条布局](ui_cn/appbar/appbar-layout.md)、[综合案例](ui_cn/appbar/demo.md) |
| [按钮](ui_cn/button.md) | 普通按钮、图标按钮和点击交互 | [按钮组](ui_cn/button/button-group.md)、[综合案例](ui_cn/button/demo.md) |
| [多选框](ui_cn/check.md) | 多项选择 | [综合案例](ui_cn/check/demo.md) |
| [小片](ui_cn/chip.md) | 标签式选择与筛选 | [小片组](ui_cn/chip/chip-group.md)、[综合案例](ui_cn/chip/demo.md) |
| [下拉框](ui_cn/drop.md) | 下拉选项选择 | [综合案例](ui_cn/drop/demo.md) |
| [编辑框](ui_cn/edit.md) | 文本编辑与输入 | [综合案例](ui_cn/edit/demo.md) |
| [悬浮按钮](ui_cn/fab.md) | Material 悬浮操作按钮 | [综合案例](ui_cn/fab/demo.md) |
| [分割线](ui_cn/hr.md) | 内容分隔 | [综合案例](ui_cn/hr/demo.md) |
| [图片与图标](ui_cn/img.md) | 图片、图标、圆角和着色 | [综合案例](ui_cn/img/demo.md) |
| [输入框](ui_cn/input.md) | 带辅助文本的输入组件 | [综合案例](ui_cn/input/demo.md) |
| [列表](ui_cn/ls.md) | 纵向列表与列表项 | — |
| [加载](ui_cn/load.md) | 加载状态与进度指示 | [综合案例](ui_cn/load/demo.md)、[登录界面案例](ui_cn/load/demo-login.md) |
| [日志](ui_cn/log.md) | 页面内日志显示 | [综合案例](ui_cn/log/demo.md)、[日志框架案例](ui_cn/log/demo-log.md) |
| [导航栏](ui_cn/nav.md) | 底部导航与页面切换 | [综合案例](ui_cn/nav/demo.md) |
| [多页布局](ui_cn/pager.md) | 多页面切换与分页 | [标签联动案例](ui_cn/pager/demo-pager-tab.md) |
| [进度条](ui_cn/progress.md) | 线性或圆形进度显示 | [综合案例](ui_cn/progress/demo.md)、[下载图片案例](ui_cn/progress/demo-downloadImg.md) |
| [单选按钮](ui_cn/radio.md) | 单项选择 | [单选按钮组](ui_cn/radio/radio-group.md)、[综合案例](ui_cn/radio/demo.md) |
| [轨道](ui_cn/rail.md) | 导航轨道与内容切换 | [综合案例](ui_cn/rail/demo.md)、[动态组件案例](ui_cn/rail/demo-dyn-widget.md) |
| [范围](ui_cn/range.md) | 范围值展示与选择 | [综合案例](ui_cn/range/demo.md) |
| [拖动条](ui_cn/seek.md) | 拖动选择数值 | — |
| [滑动条](ui_cn/slider.md) | Material 滑动条 | — |
| [状态栏](ui_cn/statusbar.md) | 页面状态栏样式 | — |
| [开关](ui_cn/switch.md) | 二态开关 | [综合案例](ui_cn/switch/demo.md) |
| [标签布局](ui_cn/tab.md) | 标签页与内容联动 | — |
| [文本](ui_cn/text.md) | 文本样式、字号和颜色 | — |
| [工具栏](ui_cn/toolbar.md) | 页面工具栏 | — |
| [视频](ui_cn/video.md) | 视频播放组件 | [简易播放器案例](ui_cn/video/demo_simple_video_player.md) |
| [网页](ui_cn/webview.md) | WebView 容器与页面交互 | [功能交互案例](ui_cn/webview/demo_simple_webview_call.md)、[桥梁对象](ui_cn/webview/webview-bridge.md) |

### 示例速查

| 示例 | 涉及能力 |
| --- | --- |
| [按钮综合案例](ui_cn/button/demo.md) | 按钮样式、图标与点击事件 |
| [登录界面](ui_cn/load/demo-login.md) | 输入框、按钮、加载状态和布局组合 |
| [日志框架案例](ui_cn/log/demo-log.md) | 日志显示与页面集成 |
| [标签联动](ui_cn/pager/demo-pager-tab.md) | 多页布局与标签切换 |
| [下载图片案例](ui_cn/progress/demo-downloadImg.md) | 网络下载与进度反馈 |
| [动态组件](ui_cn/rail/demo-dyn-widget.md) | 动态添加和更新控件 |
| [简易视频播放器](ui_cn/video/demo_simple_video_player.md) | 视频组件与媒体控制 |
| [WebView 功能交互](ui_cn/webview/demo_simple_webview_call.md) | 页面与脚本双向调用 |

## 语言版本

| 内容 | 中文 | English directory |
| --- | --- | --- |
| API 参考 | [中文 API](api_cn/ag.md) | [English API](api_en/ag.md) |
| UI 框架 | [中文 UI](ui_cn/index.md) | [English UI](ui_en/index.md) |
| 手势动作 | [`$act` 中文](api_cn/act.md) | [`$act` English](api_en/act.md) |
| 图色框架 | [`$ag` 中文](api_cn/ag.md) | [`$ag` English](api_en/ag.md) |
| 界面交互 | [`$ui` 中文](ui_cn/ui.md) | [`$ui` English](ui_en/ui.md) |

## 文档约定

- **`$` 前缀**：表示脚本运行环境中可直接使用的全局对象，例如 `$app`、`$img`、`$ui`。
- **对象主文档**：通常以对象名命名，例如 [`api_cn/http.md`](api_cn/http.md)。
- **类型与配置文档**：位于对象同名目录，例如 [`HttpOptions`](api_cn/http/HttpOptions.md)、[`OcrOptions`](api_cn/ocr/OcrOptions.md)。
- **综合案例**：文件名通常为 `demo.md`；专题案例使用 `demo-*.md` 或 `demo_*.md`。
- **更新时间**：每篇文档开头都标注了更新时间，版本行为以对应页面为准。

## 仓库结构

```text
AutoGod-Docs/
├─ README.md
├─ api_cn/        # 中文 API 参考
│  ├─ act/        # 手势相关类型
│  ├─ img/        # 图片类型
│  ├─ ocr/        # OCR 配置与结果
│  ├─ yolo/       # 目标检测与训练资料
│  └─ ...
├─ api_en/        # 英文目录的 API 参考
├─ ui_cn/         # 中文 UI 框架
│  ├─ layout/     # 布局文档
│  ├─ ui/         # $ui、UI、Sheet
│  └─ .../        # 控件与示例
└─ ui_en/         # 英文目录的 UI 文档
```



如果不知道从哪里开始，建议先阅读 [UI 框架总览](ui_cn/index.md)；如果主要开发自动化能力，则从 [`$act` 手势动作](api_cn/act.md) 和 [`$ag` 图色框架](api_cn/ag.md) 开始。
