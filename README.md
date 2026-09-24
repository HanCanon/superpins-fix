# SuperPins Fix

为 [Zen Browser](https://zen-browser.app/) 的 [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) 提供声音按钮与 Glance 预览标记的 CSS 修复，通过 [Sine](https://github.com/CosmoCreeper/Sine) 独立安装。

保留 SuperPins 的图标网格布局，避免播放声音或打开 Glance 时，新增控件撑宽标签、溢出背景或出现图标偏移。

> 当前版本：**0.1.1**，仍在完善视觉效果。请先阅读下方的当前效果与已知限制。

## 功能

- 修复固定标签的声音按钮溢出，保留原生静音与取消静音功能。
- 为 Glance 子标签单独定位，避免继承父标签的图标偏移规则。
- 保留普通状态的标签宽度、图标位置、间距与换行。
- 纯 CSS 实现，与原版 SuperPins 分别更新、启用和卸载。

## 安装

1. 安装并启用 **Sine** 和 **SuperPins**。
2. 在 SuperPins 中启用图标网格模式（legacy layout）和自动伸展（auto-grow），使用 Zen 竖向标签栏。
3. 在 Sine 的自定义 GitHub 仓库安装入口输入：

   ```text
   HanCanon/superpins-fix
   ```

4. 安装并启用 **SuperPins Fix**，同时保持原版 SuperPins 启用。若样式未刷新，重启 Zen。

无需下载或导入项目文件夹，也无需编辑 SuperPins 文件或 Sine 的样式入口。Sine 2.3.4.1c 的“导入”功能用于恢复模组清单，不接受本项目文件夹或单独的 `theme.json`。

## 兼容性

以下组合已完成隔离环境中的布局和基本交互测试：

| 组件 | 版本 |
| --- | --- |
| Zen Browser | 1.22.2b |
| SuperPins | 1.7.2 |
| Sine | 2.3.4.1c |

补丁依赖以下设置，可在 `about:config` 中核对：

| 偏好 | 值 |
| --- | --- |
| `zen.tabs.vertical` | `true` |
| `uc.pins.legacy-layout` | `true` |
| `uc.pins.auto-grow` | `true` |

仅作用于展开侧栏中的顶层固定标签网格；不处理普通标签、Essentials 和文件夹内的标签。关闭上述选项或进入拖放状态时，交由原版布局处理。

其他版本尚未确认兼容。Zen 或 SuperPins 更新后，可能需要调整补丁。

## 当前效果与已知限制

**0.1.1 使用底部角标布局：**声音按钮位于右下角，Glance 标记位于左下角。出现声音、静音、媒体阻止状态或 Glance 时，网站图标上移 8px；状态消失后恢复原位。这一版本尚未实现 Essentials 风格的右上角叠放预览卡片。

- 声音按钮缩放为 16px，点击区域也随之缩小。
- 已测试 16px 网站图标和 40px 标签高度；其他尺寸组合需要验证。
- 已验证多种侧栏宽度下的布局、真实音频的静音／取消静音，以及通过 Zen 原生管理器打开／关闭 Glance。
- 自动播放阻止后的恢复点击、Alt+点击手势、紧凑侧栏隐藏／弹出，以及 GitHub 远程更新的完整流程尚未全部验证。

## 更新与卸载

通过 Sine 检查本模组更新。多设备使用时，分别安装本模组，并保持相同的 SuperPins 设置；补丁不会同步浏览器偏好。

要恢复原版效果，在 Sine 中停用或卸载 **SuperPins Fix** 即可。上游修复相关问题后，也可以先停用补丁确认是否仍有需要。

## 问题反馈与贡献

欢迎提交 [Issue](https://github.com/HanCanon/superpins-fix/issues) 或 Pull Request。反馈布局问题时，请附上：

- Zen、SuperPins、Sine 和本补丁的版本。
- 相关 SuperPins 设置、侧栏模式及其他影响标签外观的模组。
- 复现步骤，以及补丁启用／停用时的对比截图。

修改 CSS 后，请检查普通状态、播放、静音、Glance 打开／关闭，以及音频与 Glance 同时出现的情况；确认不同侧栏宽度下的换行和按钮点击正常。

项目文件：

| 文件 | 用途 |
| --- | --- |
| [chrome.css](chrome.css) | 修复样式 |
| [theme.json](theme.json) | Sine 安装与更新元信息 |

发布样式更新时保持模组 UUID 不变，并同时更新 `version` 和 `updatedAt`。Sine 2.3.4.1c 通过 `updatedAt` 判断自定义仓库是否有更新；仅修改版本号不足以触发更新。

## 相关项目

- [Zen Browser](https://github.com/zen-browser/desktop)
- [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins)
- [Sine](https://github.com/CosmoCreeper/Sine)

本项目是独立的兼容补丁，并非上述项目的官方组件。
