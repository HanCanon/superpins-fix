# SuperPins Fix

Zen 浏览器的独立 CSS 补丁，通过 Sine 与原版 SuperPins 一起加载。修复顶层图标网格固定标签的声音按钮溢出，以及嵌套 Glance 图标被百分比居中规则推偏的问题。

**当前为 0.1.1 候选版本。** 仓库：[HanCanon/superpins-fix](https://github.com/HanCanon/superpins-fix)。修正 0.1.0 强制 80px 最小宽度造成的额外换行，保留普通状态的原版布局。新版已完成隔离布局和原生交互测试，日常配置下的视觉验收仍需进行。

## 适用范围

2026-09-23 重新核对的目标环境：

| 项目 | 版本／设置 |
| --- | --- |
| Zen | 1.22.2b，BuildID `20260915091052` |
| Zen SourceStamp | `e74571eead515d37edd0914739f744bcb5258c51` |
| SuperPins | 1.7.2，提交 `88639a2587d076925baa33d4af3c867499da526e` |
| Sine | 本机 engine.json 标记 `2.3.4.1c` |
| 必需偏好 | `zen.tabs.vertical = true` |
| 必需偏好 | `uc.pins.legacy-layout = true` |
| 必需偏好 | `uc.pins.auto-grow = true` |
| 生效状态 | `#navigator-toolbox[zen-sidebar-expanded="true"]` |

仅匹配固定标签区域的直接子标签；排除 Essentials、Glance 子标签本身和文件夹内的标签。拖放期间区域含 `zen-dragtarget` 时退出，让上游处理拖动布局。普通标签、折叠侧栏、关闭 legacy-layout 或 auto-grow 时均不应用补丁。

这里的“展开”指 DOM 状态；Zen 隐藏式紧凑模式与窄侧栏不是同一概念。紧凑侧栏在弹出时若带有展开属性，仍会匹配补丁。实际隐藏／弹出切换需要人工验收。

## 布局与取舍

不覆盖标签的宽度、最小宽度、网格列数和普通状态图标位置，由 SuperPins 决定间距与换行。声音按钮绝对定位在右下角，Glance 标记位于左下角，两者不占用横向布局空间。

有声音／静音／媒体阻止状态或 Glance 时，主图标上移 8px，为底部角标留出空间；状态消失后恢复原位置。原生 24px 声音控件整体缩放为 **16px**，包括其点击区域；Glance 标记为 16px，内部图标为 12px。这是保留紧凑宽度的取舍。默认 16px 网站图标、40px 标签高度已测试，其他高度和放大图标选项需要另行验证。

不隐藏或裁切声音按钮，不修改其状态图标、提示、静音／取消静音／媒体阻止逻辑，也不修改 Glance 的原生事件处理。Glance 子标签自身的声音按钮仍遵循 Zen 原生隐藏规则；本补丁修复的是父固定标签按钮。

补丁不含 JavaScript。原版 SuperPins 仍须保留；不要修改其安装文件，也不要手工编辑 Sine 自动生成的 CSS 入口。

## 通过 Sine 安装

仓库地址为 `https://github.com/HanCanon/superpins-fix`。建议先在隔离配置中验证仓库安装：

1. 将 `chrome.css`、`theme.json`、`README.md` 放在同一个 GitHub 仓库根目录；`.gitignore` 排除本地研究与测试配置。
2. 在目标设备安装 Sine 和原版 SuperPins，核对上表的必需偏好。
3. 在 Sine 的自定义仓库安装入口输入 `HanCanon/superpins-fix`（或上述仓库地址），安装 **SuperPins Fix**。若该配置已手动注册同 UUID 的补丁，先在 Sine 中移除旧的本地安装记录。
4. 确认两个 Mod 均已启用，再按下方清单验收。若热加载结果不明确，重启隔离浏览器后复测。

`theme.json` 使用稳定 UUID、名称、说明、版本、`style.chrome` 和时间字段。homepage 指向本仓库。UUID 应长期保持不变。

Sine 可从未上架的 GitHub 仓库安装 Mod，并从来源获取更新，见 [Sine README](https://github.com/CosmoCreeper/Sine#-test-mods-in-a-snap)。本项目尚未验证远程下载和更新的完整流程；本地注册后的热切换已验证。

## 本地导入与本地测试

本机 Sine 2.3.4.1c 的“导入”按钮接受 `.json` 文件，但其用途是恢复 Sine 导出的**模组清单数组**。已核对本机 `core/settings.mjs`：读取数组后，对每项调用 `manager.installMod(mod.homepage, null, false)`，仍从仓库下载代码。它不接受项目文件夹、ZIP，也不能直接把本项目的单个 `theme.json` 当作导入清单。

无需先发布仓库也能做开发测试：将文件放入隔离配置的 Sine 模组目录，并登记本地安装记录。这属于手动本地注册，不是“导入”按钮的安装流程。本次测试步骤为：

1. 创建独立 Zen 配置，复制本机的 Sine 启动组件、完整 SuperPins 和 unloaded-tabs Mod；关闭该测试配置的自动更新。
2. 在测试浏览器关闭时，将本项目三个文件复制到该配置的 `chrome/sine-mods/267b7866-35ad-437f-9ab8-c6baf2810d42/`。
3. 在该配置的 `chrome/sine-mods/mods.json` 对象中，以补丁 UUID 为键，加入 `theme.json` 的元信息，并增加 `"enabled": true`、`"no-updates": true`。保留其他 Mod 记录，不覆盖整个清单。
4. 启动测试浏览器。Sine 自己生成 CSS 入口并加载补丁，无需手写或修改 `chrome/sine-mods/chrome.css`。
5. 本地文件修改不会从 GitHub 自动同步；测试新的 CSS 时重新复制文件并重启测试浏览器。本次本地测试记录创建时没有 homepage；即使新 manifest 已提供仓库地址，本地测试记录也应保持禁止自动更新，避免测试代码被远端替换。

本次隔离配置位于项目内 `.local-research/profile-sine/`。本地注册方式已验证，不代表 Sine 承诺长期支持此内部记录格式。日常分发仍推荐 GitHub 仓库安装，便于获取更新。不要在浏览器运行时直接修改其安装清单。

## 加载优先级与更新

已读取本机 Sine 的 `services/stylesheets.sys.mjs` 和 `core/manager.sys.mjs`，并与 [上游源码快照](https://github.com/CosmoCreeper/Sine/tree/fb0bd4ca6af888f10648e126947f7d1f82228433/src) 对照：

- CSS 按 Mod ID 的字典序生成 `@import`，作为 `USER_SHEET` 加载；不是按安装先后顺序。本补丁的 ID 实际排在 SuperPins 前面。
- 本补丁规则含两个真实祖先 ID，并使用 `!important`，覆盖目标范围内 SuperPins 的重要规则。已在同一 USER_SHEET 来源层级下验证前后两种加载顺序。无需重命名 ID 来抢顺序；未使用会改变重要规则优先级的 cascade layer。
- 本机 Sine 对自定义仓库比较 `new Date(updatedAt)`，远端时间更晚才更新。**每次发布同时递增 version 和 updatedAt**；同一天发布多次时使用不同的 ISO 8601 UTC 时间。仅递增 version 不足以触发此版本 Sine 的更新。
- Manifest 明确提供 updatedAt，因此不依赖 Sine 在字段缺失时采用 GitHub 仓库时间的回退逻辑。无需添加商店专用 commit 或 origin 字段。

以上是针对当前实现的核对结果，升级 Sine 后需要重新确认。

## 已完成的隔离验证

0.1.1 使用本机 Zen 1.22.2b，在项目内独立配置中加载完整 Sine、SuperPins 1.7.2 和 unloaded-tabs Mod。未修改日常配置。

- 在固定区域宽度 180、240、260、320 CSS px 下，对比 Sine 开关补丁前后：普通标签及网站图标的 x/y/宽/高完全一致，保留换行与间距。
- 24 个组合（180/240/320px × 普通/播放/静音/媒体阻止 × Glance 有无）通过：图标不横移，角标在标签内，网站图标、声音按钮与 Glance 互不重叠，相邻标签无重叠或新增宽度差异。
- 5 个退出条件通过：关闭 legacy、关闭竖向标签、关闭展开属性、拖动标记、关闭 auto-grow。偏好切换会触发上游样式重建；原版外观比较在恢复稳定后单独执行。
- 真实音频播放、原生按钮静音/取消静音通过；通过 Zen 管理器打开 Glance 后再次静音/取消静音通过；关闭 Glance 后子标签移除。

布局矩阵中的状态与 Glance 节点为 DOM 夹具，另有真实媒体及原生 Glance 管理器交互测试。尚未覆盖真实自动播放阻止后的恢复点击、Alt+点击手势、紧凑侧栏隐藏/弹出、所有图标尺寸与高度选项。

0.1.0 曾验证两种 CSS 加载顺序、范围排除和重启保留；这些是旧版测试记录，不视为新版已重跑。新版沿用相同祖先选择器优先级。测试脚本、配置和结果位于忽略的 `.local-research/`，不属于发布文件。

## 安装后的人工验收

优先在独立 Zen 配置中安装完整 Sine、SuperPins 和本补丁，不要直接用主配置试验。对照补丁启用／停用两种状态检查：

- 普通固定标签：图标居中，选中／悬停背景和相邻标签正常，与停用补丁时的间距和换行一致。
- 播放、静音、取消静音、媒体自动播放被阻止：按钮完整、可点击，提示与音频状态一致；阻止状态点击后能够恢复。
- 用实际手势打开和关闭 Glance：预览标记可识别，关闭后消失，主图标不偏移。
- 父标签播放声音时打开 Glance：两个位置不重叠；Glance 开着时再次点击静音与取消静音。
- 拖动侧栏宽度，切换展开、折叠、紧凑隐藏／弹出状态；退出补丁范围时应回到原生／SuperPins 布局。
- 检查普通标签、Essentials、文件夹、标签拖放，以及另一个 unloaded-tabs Mod；不应出现补丁导致的新增变化。
- Sine 中单独停用／启用补丁，重启后再次确认；从测试仓库提高 updatedAt 后验证更新识别。

## 多设备、移除和维护

每台设备分别安装同一个原版 SuperPins 和同一个补丁仓库。代码更新与浏览器偏好同步是两件事；请单独核对必要选项，不要依赖安装补丁自动改偏好。

先在 Sine 停用 **SuperPins Fix** 复测；确认无需补丁后卸载这个 Mod 即可。补丁没有新建偏好、修改入口或写入原版 SuperPins 文件。上游修复后，同样先停用复测，再决定移除。

独立补丁不会被 SuperPins 更新直接覆盖，但 Zen DOM、按钮尺寸、上游选择器或 Sine 加载方式变化仍可能使其失效。升级后按上述清单回归，保留明确的版本验证记录。

参考：[SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins)、[Sine](https://github.com/CosmoCreeper/Sine)。
