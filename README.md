# SuperPins Fix

Zen 浏览器的独立 CSS 补丁，通过 Sine 与原版 SuperPins 一起加载。修复顶层图标网格固定标签的声音按钮溢出，以及嵌套 Glance 图标被百分比居中规则推偏的问题。

**当前为 0.1.0 本地候选版本，尚未发布仓库或在日常用户配置中安装。** 已完成独立 CSS 测试，以及完整 Sine 的隔离本地注册、加载、开关和重启验证；Sine 仓库下载安装、真实侧栏切换及人工视觉验收仍待完成。

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

每个顶层固定标签使用三列：左侧 24px Glance 标记、中间居中的网站图标、右侧原生 24px 声音按钮。状态不存在时保留相应位置，避免网站图标移动。子标签图标独立居中，不继承 SuperPins 的 `margin-left: 50%` 和位移。

最小标签宽度为 **80px**，或 SuperPins 原有最小宽度（取较大者）。这为三个位置、间距和内边距留足空间，窄侧栏每行可能比原来少一个标签。保持上游自动伸展和换行，不强行指定每行数量。其他网格列数、图标尺寸和高度选项尚未全面验证。

不隐藏或裁切声音按钮，不修改其状态图标、提示、静音／取消静音／媒体阻止逻辑，也不修改 Glance 的原生事件处理。Glance 子标签自身的声音按钮仍遵循 Zen 原生隐藏规则；本补丁修复的是父固定标签按钮。

补丁不含 JavaScript。原版 SuperPins 仍须保留；不要修改其安装文件，也不要手工编辑 Sine 自动生成的 CSS 入口。

## 通过 Sine 安装

仓库尚未发布，因此目前没有可直接填写的安装地址。发布并完成隔离验收后：

1. 将 `chrome.css`、`theme.json`、`README.md` 放在同一个 GitHub 仓库根目录；`.gitignore` 排除本地研究与测试配置。
2. 在目标设备安装 Sine 和原版 SuperPins，核对上表的必需偏好。
3. 在 Sine 的自定义仓库安装入口输入实际的 `所有者/仓库名`（或仓库地址），安装 **SuperPins Fix**。不要把示例文字当成地址。
4. 确认两个 Mod 均已启用，再按下方清单验收。若热加载结果不明确，重启隔离浏览器后复测。

`theme.json` 使用稳定 UUID、名称、说明、版本、`style.chrome` 和时间字段。没有编造作者或尚不存在的 homepage；本机 Sine 的 `createThemeJSON()` 会用实际安装来源补齐 homepage。UUID 应长期保持不变。

Sine 可从未上架的 GitHub 仓库安装 Mod，并从来源获取更新，见 [Sine README](https://github.com/CosmoCreeper/Sine#-test-mods-in-a-snap)。本项目尚未验证远程下载和更新的完整流程；本地注册后的热切换已验证。

## 本地导入与本地测试

本机 Sine 2.3.4.1c 的“导入”按钮接受 `.json` 文件，但其用途是恢复 Sine 导出的**模组清单数组**。已核对本机 `core/settings.mjs`：读取数组后，对每项调用 `manager.installMod(mod.homepage, null, false)`，仍从仓库下载代码。它不接受项目文件夹、ZIP，也不能直接把本项目的单个 `theme.json` 当作导入清单。

无需先发布仓库也能做开发测试：将文件放入隔离配置的 Sine 模组目录，并登记本地安装记录。这属于手动本地注册，不是“导入”按钮的安装流程。本次测试步骤为：

1. 创建独立 Zen 配置，复制本机的 Sine 启动组件、完整 SuperPins 和 unloaded-tabs Mod；关闭该测试配置的自动更新。
2. 在测试浏览器关闭时，将本项目三个文件复制到该配置的 `chrome/sine-mods/267b7866-35ad-437f-9ab8-c6baf2810d42/`。
3. 在该配置的 `chrome/sine-mods/mods.json` 对象中，以补丁 UUID 为键，加入 `theme.json` 的元信息，并增加 `"enabled": true`、`"no-updates": true`。保留其他 Mod 记录，不覆盖整个清单。
4. 启动测试浏览器。Sine 自己生成 CSS 入口并加载补丁，无需手写或修改 `chrome/sine-mods/chrome.css`。
5. 本地文件修改不会从 GitHub 自动同步；测试新的 CSS 时重新复制文件并重启测试浏览器。本地记录没有 homepage，保持禁止自动更新。

本次隔离配置位于项目内 `.local-research/profile-sine/`。本地注册方式已验证，不代表 Sine 承诺长期支持此内部记录格式。日常分发仍推荐 GitHub 仓库安装，便于获取更新。不要在浏览器运行时直接修改其安装清单。

## 加载优先级与更新

已读取本机 Sine 的 `services/stylesheets.sys.mjs` 和 `core/manager.sys.mjs`，并与 [上游源码快照](https://github.com/CosmoCreeper/Sine/tree/fb0bd4ca6af888f10648e126947f7d1f82228433/src) 对照：

- CSS 按 Mod ID 的字典序生成 `@import`，作为 `USER_SHEET` 加载；不是按安装先后顺序。本补丁的 ID 实际排在 SuperPins 前面。
- 本补丁规则含两个真实祖先 ID，并使用 `!important`，覆盖目标范围内 SuperPins 的重要规则。已在同一 USER_SHEET 来源层级下验证前后两种加载顺序。无需重命名 ID 来抢顺序；未使用会改变重要规则优先级的 cascade layer。
- 本机 Sine 对自定义仓库比较 `new Date(updatedAt)`，远端时间更晚才更新。**每次发布同时递增 version 和 updatedAt**；同一天发布多次时使用不同的 ISO 8601 UTC 时间。仅递增 version 不足以触发此版本 Sine 的更新。
- Manifest 明确提供 updatedAt，因此不依赖 Sine 在字段缺失时采用 GitHub 仓库时间的回退逻辑。无需添加商店专用 commit 或 origin 字段。

以上是针对当前实现的核对结果，升级 Sine 后需要重新确认。

## 已完成的隔离验证

使用本机同一 Zen 二进制、全新项目内配置和 Marionette 无界面测试。未复制真实配置的登录信息；未修改现用浏览器配置。首轮直接按 USER_SHEET 方式加载 CSS；后续在另一隔离配置中使用完整本机 Sine、SuperPins（含 JavaScript）和 unloaded-tabs Mod，由 Sine 自己加载本地注册的补丁。

最终 CSS 的测试结果：

| 检查 | 结果与边界 |
| --- | --- |
| 48 个布局组合 | 2 种加载顺序 × 3 种区域宽度（180/240/320 CSS px）× 4 种状态（普通／声音／静音／媒体阻止）× Glance 有无；全部通过 |
| 布局断言 | 网站图标中心误差不超过 0.6 CSS px；按钮内部 24px 区域、Glance 和图标均在父标签内；互不重叠；相邻标签不重叠；同排宽度一致；父标签未溢出区域 |
| 5 个退出条件 | legacy 关闭、竖向标签关闭、展开属性关闭、拖动标记、auto-grow 关闭；均退出补丁布局 |
| 3 个范围检查 | Essentials、非固定标签、嵌套容器中的标签；补丁启停不改变被检布局属性（属性／结构模拟，不是完整文件夹交互） |
| 真实媒体 | 本地生成 WAV 播放产生原生 soundplaying；原生按钮点击后 tab 的 muted 与 browser.audioMuted 均变为 true，再次点击均变回 false |
| 真实 Glance | 调用 Zen 原生管理器打开预览并形成嵌套子标签；父标签音频仍在播放时截屏检查；按关闭标签流程关闭后子标签消失 |
| 完整 Sine 布局回归 | 自动生成入口加载下，24 个状态／宽度组合和 5 个退出条件全部通过 |
| 完整 Sine 交互回归 | 原生新建、加载音频并固定标签；播放、静音、取消静音、Glance 打开／关闭通过；Glance 开着时静音及取消静音通过，均确认父标签仍位于固定区域并使用 grid |
| Sine 开关 | 调用与界面开关相同的 `toggleTheme()`；停用后入口移除补丁、布局恢复 flex 和百分比 margin；启用后入口恢复、布局变为 grid 和零 margin |
| 重启保留 | 正常关闭再启动同一隔离配置，补丁仍启用，新固定标签自动应用 grid，入口由 Sine 生成 |

布局矩阵中的状态与 Glance 节点是注入真实浏览器 DOM 的测试夹具；另有独立的真实播放及 Glance 管理器测试。媒体阻止只验证了状态布局，尚未实际触发自动播放阻止后点击恢复。Glance 测试没有覆盖 Alt+点击手势和所有焦点路径。

测试工具、第三方源码、临时配置和原始结果保留在被 `.gitignore` 排除的 `.local-research/`，不属于发布内容。曾遇到测试配置无普通标签时 Glance 关闭调用报错；最终交互测试保留普通标签后通过。后续还发现改写标签 ID 会干扰 Zen 分区同步，最终完整 Sine 交互测试保留原生 ID，并逐步检查父容器。不将这些隔离夹具问题解释为 CSS 修复了 Zen 的关闭或同步逻辑。

## 安装后的人工验收

优先在独立 Zen 配置中安装完整 Sine、SuperPins 和本补丁，不要直接用主配置试验。对照补丁启用／停用两种状态检查：

- 普通固定标签：图标居中，选中／悬停背景和相邻标签正常，换行可接受。
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
