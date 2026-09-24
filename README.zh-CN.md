# SuperPins Fix

[English](README.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md)

**最终版本: 0.1.2** · [通过 Sine 安装](https://github.com/CosmoCreeper/Sine) · [反馈问题](https://github.com/HanCanon/superpins-fix/issues)

为 [Zen Browser](https://zen-browser.app/) 的 [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) 提供独立的 CSS 修复，通过 Sine 与原版模组一起使用。解决图标网格固定标签中的声音按钮溢出、Glance 预览标记偏移，以及网站图标与标签背景不对齐的问题。

## 功能与效果

- **图标居中**：网站图标相对标签背景水平、垂直居中，播放声音或打开 Glance 时保持原位。
- **叠放预览**：Glance 显示为右上角带背景和边框的小卡片，视觉风格参考 Zen Essentials。
- **声音角标**：声音按钮位于右下角，保留原生静音、取消静音及状态显示。
- **保留布局**：不增加标签最小宽度，保留 SuperPins 的间距和换行。
- **独立安装**：纯 CSS，无额外 JavaScript；无需修改 SuperPins 文件或 Sine 自动生成的样式入口。

## 安装

1. 安装并启用 [Sine](https://github.com/CosmoCreeper/Sine) 和原版 **SuperPins**。
2. 启用 Zen 竖向标签栏，以及 SuperPins 的图标网格模式（legacy layout）和自动伸展（auto-grow）。
3. 在 Sine 的自定义 GitHub 仓库安装入口输入：

   ```text
   HanCanon/superpins-fix
   ```

4. 安装并启用 **SuperPins Fix**，同时保留 SuperPins 启用。若样式未刷新，重启 Zen。

如果已安装旧版补丁，在 Sine 中检查更新，确认版本为 **0.1.2**。无需导入项目文件夹或 `theme.json`；Sine 的“导入”按钮用于恢复模组清单。

## 兼容性与必要设置

| 组件 | 已验证版本 |
| --- | --- |
| Zen Browser | 1.22.2b |
| SuperPins | 1.7.2 |
| Sine | 2.3.4.1c |

在 `about:config` 中核对：

| 偏好 | 必需值 |
| --- | --- |
| `zen.tabs.vertical` | `true` |
| `uc.pins.legacy-layout` | `true` |
| `uc.pins.auto-grow` | `true` |

仅作用于**展开侧栏中的顶层固定标签网格**。普通标签、Essentials 和文件夹内的标签不在修复范围；不满足上述设置或区域存在拖动目标标记时，不应用补丁布局。

其他版本尚未确认兼容。多设备使用时，分别安装补丁并保持相同的必要设置；本项目不负责同步浏览器偏好。

## 验证与使用边界

0.1.2 已通过隔离环境的布局和原生交互测试，维护者也已在实际使用中确认效果良好，暂未发现其他问题。

- 覆盖普通、播放、静音、媒体阻止状态，以及 Glance 有无的 24 个布局组合；另行验证了真实音频的静音／取消静音、Glance 打开／关闭及同时出现时的操作。
- 在固定标签区域宽度为 180、240、260、320 CSS px 时，确认标签本身的尺寸、位置和换行不因补丁改变；主图标修正为背景中心。
- 已测试 16px 网站图标、40px 标签高度。声音按钮及点击区域为 16px；Glance 卡片为 24×20px，内部图标为 14px。
- 窄标签中，预览卡片可以叠在网站图标边缘，这是设计效果；不会因此移动主图标。声音与 Glance 角标分居上下，不互相遮挡。
- 其他图标／标签尺寸、真实自动播放阻止后的恢复点击、Alt+点击手势、紧凑侧栏隐藏／弹出，以及远程更新的完整流程尚未全面验证。

## 移除与故障排查

在 Sine 中停用或卸载 **SuperPins Fix** 即可恢复原版效果，不需要恢复其他配置文件。

若补丁未生效，先核对版本、三个必要偏好，以及 Sine 中两个模组是否均已启用，再重启 Zen。若外观异常，停用补丁对比，并检查其他修改标签外观的模组。上游修复相关问题后，可停用本补丁确认是否仍有需要。

## 项目状态与反馈

**0.1.2 为最终版本，不再计划发布后续版本。** 未来 Zen、SuperPins 或 Sine 更新可能影响兼容性，本项目不承诺跟进适配。

仍可通过 [Issues](https://github.com/HanCanon/superpins-fix/issues) 记录问题，但不保证响应或修复。请附上组件版本、SuperPins 设置、侧栏模式、其他相关模组、复现步骤，以及补丁启用／停用时的对比截图。

## 项目文件

| 文件 | 用途 |
| --- | --- |
| [chrome.css](chrome.css) | 修复样式 |
| [theme.json](theme.json) | Sine 元信息 |
| [README.md](README.md) | 英语说明 |
| [README.zh-CN.md](README.zh-CN.md) | 简体中文说明 |
| [README.ja.md](README.ja.md) | 日语说明 |

## 致谢

[Zen Browser](https://github.com/zen-browser/desktop) · [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) · [Sine](https://github.com/CosmoCreeper/Sine)

本项目是独立的兼容补丁，并非上述项目的官方组件。
