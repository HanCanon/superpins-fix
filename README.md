# SuperPins Fix

**[简体中文](#简体中文) · [English](#english) · [日本語](#日本語)**

A small CSS companion for SuperPins: centered favicons, contained audio controls, and floating Glance cards.

**Final version: 0.1.2** · [Install with Sine](https://github.com/CosmoCreeper/Sine) · [Report an issue](https://github.com/HanCanon/superpins-fix/issues)

---

## 简体中文

为 [Zen Browser](https://zen-browser.app/) 的 [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) 提供独立的 CSS 修复，通过 Sine 与原版模组一起使用。解决图标网格固定标签中的声音按钮溢出、Glance 预览标记偏移，以及网站图标与标签背景不对齐的问题。

### 功能与效果

- **图标居中**：网站图标相对标签背景水平、垂直居中，播放声音或打开 Glance 时保持原位。
- **叠放预览**：Glance 显示为右上角带背景和边框的小卡片，视觉风格参考 Zen Essentials。
- **声音角标**：声音按钮位于右下角，保留原生静音、取消静音及状态显示。
- **保留布局**：不增加标签最小宽度，保留 SuperPins 的间距和换行。
- **独立安装**：纯 CSS，无额外 JavaScript；无需修改 SuperPins 文件或 Sine 自动生成的样式入口。

### 安装

1. 安装并启用 [Sine](https://github.com/CosmoCreeper/Sine) 和原版 **SuperPins**。
2. 启用 Zen 竖向标签栏，以及 SuperPins 的图标网格模式（legacy layout）和自动伸展（auto-grow）。
3. 在 Sine 的自定义 GitHub 仓库安装入口输入：

   ```text
   HanCanon/superpins-fix
   ```

4. 安装并启用 **SuperPins Fix**，同时保留 SuperPins 启用。若样式未刷新，重启 Zen。

如果已安装旧版补丁，在 Sine 中检查更新，确认版本为 **0.1.2**。无需导入项目文件夹或 `theme.json`；Sine 的“导入”按钮用于恢复模组清单。

### 兼容性与必要设置

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

### 验证与使用边界

0.1.2 已通过隔离环境的布局和原生交互测试，维护者也已在实际使用中确认效果良好，暂未发现其他问题。

- 覆盖普通、播放、静音、媒体阻止状态，以及 Glance 有无的 24 个布局组合；另行验证了真实音频的静音／取消静音、Glance 打开／关闭及同时出现时的操作。
- 在固定标签区域宽度为 180、240、260、320 CSS px 时，确认标签本身的尺寸、位置和换行不因补丁改变；主图标修正为背景中心。
- 已测试 16px 网站图标、40px 标签高度。声音按钮及点击区域为 16px；Glance 卡片为 24×20px，内部图标为 14px。
- 窄标签中，预览卡片可以叠在网站图标边缘，这是设计效果；不会因此移动主图标。声音与 Glance 角标分居上下，不互相遮挡。
- 其他图标／标签尺寸、真实自动播放阻止后的恢复点击、Alt+点击手势、紧凑侧栏隐藏／弹出，以及远程更新的完整流程尚未全面验证。

### 移除与故障排查

在 Sine 中停用或卸载 **SuperPins Fix** 即可恢复原版效果，不需要恢复其他配置文件。

若补丁未生效，先核对版本、三个必要偏好，以及 Sine 中两个模组是否均已启用，再重启 Zen。若外观异常，停用补丁对比，并检查其他修改标签外观的模组。上游修复相关问题后，可停用本补丁确认是否仍有需要。

### 项目状态与反馈

**0.1.2 为最终版本，不再计划发布后续版本。** 未来 Zen、SuperPins 或 Sine 更新可能影响兼容性，本项目不承诺跟进适配。

仍可通过 [Issues](https://github.com/HanCanon/superpins-fix/issues) 记录问题，但不保证响应或修复。请附上组件版本、SuperPins 设置、侧栏模式、其他相关模组、复现步骤，以及补丁启用／停用时的对比截图。

---

## English

An independent CSS patch for [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) in [Zen Browser](https://zen-browser.app/), installed alongside the original mod through Sine. It fixes overflowing audio controls, misplaced Glance indicators, and favicons that are off-center within pinned-tab backgrounds.

### Features

- **Centered favicons:** website icons stay horizontally and vertically centered within the tab background, including during audio playback and Glance previews.
- **Floating previews:** Glance appears as a small card in the upper-right corner, with a background and border inspired by Zen Essentials.
- **Audio badges:** the lower-right audio button retains native mute, unmute, and state handling.
- **Preserved layout:** no increased minimum tab width; SuperPins spacing and wrapping are retained.
- **Independent installation:** CSS only, with no additional JavaScript. No edits to SuperPins files or Sine-generated stylesheet entries are required.

### Installation

1. Install and enable [Sine](https://github.com/CosmoCreeper/Sine) and the original **SuperPins** mod.
2. Enable Zen's vertical tabs and SuperPins' **legacy layout** (icon grid) and **auto-grow** options.
3. Enter the following in Sine's custom GitHub repository installation field:

   ```text
   HanCanon/superpins-fix
   ```

4. Install and enable **SuperPins Fix**, keeping SuperPins enabled as well. Restart Zen if the styles do not refresh.

If you have an older patch installed, check for updates in Sine and confirm version **0.1.2**. Do not import the project folder or `theme.json`; Sine's Import button restores an exported mod list.

### Compatibility and required settings

| Component | Verified version |
| --- | --- |
| Zen Browser | 1.22.2b |
| SuperPins | 1.7.2 |
| Sine | 2.3.4.1c |

Check these preferences in `about:config`:

| Preference | Required value |
| --- | --- |
| `zen.tabs.vertical` | `true` |
| `uc.pins.legacy-layout` | `true` |
| `uc.pins.auto-grow` | `true` |

The patch applies only to **top-level pinned-tab grids in the expanded sidebar**. Regular tabs, Essentials, and tabs inside folders are outside its scope. The patch layout does not apply when the required settings are disabled or the pinned area contains a drag-target marker.

Compatibility with other versions is unconfirmed. On multiple devices, install the patch separately and use the same required settings; this project does not synchronize browser preferences.

### Validation and limitations

Version 0.1.2 passed isolated layout and native interaction tests. The maintainer has also confirmed satisfactory results in daily use, with no further issues observed so far.

- Tested 24 layout combinations covering normal, playing, muted, and blocked-media states, with and without Glance. Actual audio mute/unmute, Glance opening/closing, and their combined interaction were tested separately.
- At pinned-area widths of 180, 240, 260, and 320 CSS px, tab dimensions, positions, and wrapping were unchanged by the patch. Favicons were corrected to the background center.
- Tested with 16px favicons and 40px tab height. The audio control and its clickable area are 16px; the Glance card is 24×20px with a 14px icon.
- On narrow tabs, the preview card may overlap the favicon's edge. This layering is intentional and does not move the favicon. Audio and Glance badges occupy separate lower and upper corners without covering each other.
- Other icon/tab sizes, resuming genuinely blocked autoplay, the Alt-click gesture, compact-sidebar hide/reveal behavior, and the complete remote update flow have not been fully verified.

### Removal and troubleshooting

Disable or uninstall **SuperPins Fix** in Sine to restore the original appearance. No other configuration files need restoring.

If the patch is not applied, check component versions, the three required preferences, and that both mods are enabled in Sine, then restart Zen. For visual issues, compare with the patch disabled and check other mods that change tab appearance. If upstream fixes these issues, disable this patch to determine whether it is still needed.

### Project status and feedback

**0.1.2 is the final version. No further releases are planned.** Future Zen, SuperPins, or Sine updates may affect compatibility; ongoing adaptation is not promised.

You may still document problems in [Issues](https://github.com/HanCanon/superpins-fix/issues), but responses and fixes are not guaranteed. Include component versions, SuperPins settings, sidebar mode, other relevant mods, reproduction steps, and screenshots with the patch enabled and disabled.

---

## 日本語

[Zen Browser](https://zen-browser.app/) の [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) 向けの独立した CSS パッチです。Sine を使い、元の SuperPins と併用します。固定タブのアイコングリッドで発生する音声ボタンのはみ出し、Glance のプレビュー表示のずれ、サイトアイコンとタブ背景の中心位置のずれを修正します。

### 主な機能

- **アイコンの中央配置**：サイトアイコンをタブ背景の上下左右の中央に配置します。音声再生中や Glance 表示中も位置は変わりません。
- **重ねて表示するプレビュー**：Glance を右上の小さなカードとして表示します。背景と枠線は Zen Essentials の外観を参考にしています。
- **音声バッジ**：右下の音声ボタンで、標準のミュート、ミュート解除、状態表示を利用できます。
- **元のレイアウトを維持**：タブの最小幅を増やさず、SuperPins の間隔と折り返しを維持します。
- **独立した導入**：CSS のみで動作し、追加の JavaScript は不要です。SuperPins のファイルや Sine が生成するスタイルシートの読み込み設定を編集する必要はありません。

### インストール

1. [Sine](https://github.com/CosmoCreeper/Sine) と元の **SuperPins** をインストールし、有効にします。
2. Zen の縦型タブと、SuperPins の **legacy layout**（アイコングリッド）、**auto-grow**（自動拡張）を有効にします。
3. Sine のカスタム GitHub リポジトリのインストール欄に、次の値を入力します。

   ```text
   HanCanon/superpins-fix
   ```

4. **SuperPins Fix** をインストールして有効にします。SuperPins も有効のままにしてください。表示が更新されない場合は Zen を再起動します。

旧版を導入済みの場合は Sine で更新を確認し、バージョンが **0.1.2** になっていることを確認してください。プロジェクトフォルダーや `theme.json` のインポートは不要です。Sine の「インポート」は、エクスポートした Mod 一覧を復元する機能です。

### 対応環境と必要な設定

| コンポーネント | 動作確認済みバージョン |
| --- | --- |
| Zen Browser | 1.22.2b |
| SuperPins | 1.7.2 |
| Sine | 2.3.4.1c |

`about:config` で次の設定を確認してください。

| 設定名 | 必須の値 |
| --- | --- |
| `zen.tabs.vertical` | `true` |
| `uc.pins.legacy-layout` | `true` |
| `uc.pins.auto-grow` | `true` |

対象は、**展開されたサイドバー内の、最上位の固定タブグリッド**のみです。通常のタブ、Essentials、フォルダー内のタブは対象外です。必要な設定が無効の場合や、固定タブ領域にドラッグ対象のマーカーがある場合は、パッチのレイアウトを適用しません。

他のバージョンとの互換性は未確認です。複数の端末では、それぞれにパッチを導入し、必要な設定をそろえてください。このプロジェクトはブラウザー設定を同期しません。

### 検証内容と制限

0.1.2 は、独立したテスト環境でレイアウトと標準機能の操作テストを完了しています。メンテナーの実利用でも良好な表示が確認されており、現時点では追加の問題は報告されていません。

- 通常、音声再生、ミュート、メディア再生ブロックの各状態と Glance の有無を含む、24 通りのレイアウトを確認しました。実際の音声のミュート／解除、Glance の開閉、両機能の同時使用も別途確認しています。
- 固定タブ領域の幅が 180、240、260、320 CSS px の場合に、タブ自体の寸法、位置、折り返しが変わらないことを確認しました。サイトアイコンは背景の中央に補正されます。
- 16px のサイトアイコンと高さ 40px のタブで検証しています。音声ボタンとクリック領域は 16px、Glance カードは 24×20px、内部アイコンは 14px です。
- 幅の狭いタブでは、プレビューカードがサイトアイコンの端に重なることがあります。これは意図した表示であり、サイトアイコン自体は移動しません。音声と Glance のバッジは上下に分かれ、互いを覆いません。
- その他のアイコン／タブサイズ、実際にブロックされた自動再生の再開、Alt+クリック操作、コンパクトサイドバーの表示／非表示切り替え、リモート更新の全工程は、まだ十分に検証されていません。

### 削除とトラブルシューティング

Sine で **SuperPins Fix** を無効化またはアンインストールすると、元の表示に戻ります。他の設定ファイルを復元する必要はありません。

適用されない場合は、各バージョン、3 つの必須設定、Sine で両方の Mod が有効になっていることを確認し、Zen を再起動してください。表示に問題がある場合は、パッチを無効にした状態と比較し、タブの外観を変更する他の Mod も確認してください。上流で問題が修正された場合は、本パッチを無効にして引き続き必要かどうかを確認できます。

### プロジェクトの状態とフィードバック

**0.1.2 が最終版です。今後のリリースは予定していません。** 将来の Zen、SuperPins、Sine の更新により互換性が失われる可能性があり、継続的な対応は保証しません。

問題は引き続き [Issues](https://github.com/HanCanon/superpins-fix/issues) に記録できますが、返答や修正を保証するものではありません。各バージョン、SuperPins の設定、サイドバーのモード、関連する他の Mod、再現手順、パッチの有効時／無効時の比較スクリーンショットを添えてください。

---

## Project files · 项目文件 · ファイル構成

| File | Purpose / 用途 / 内容 |
| --- | --- |
| [chrome.css](chrome.css) | CSS patch / 修复样式 / 修正スタイル |
| [theme.json](theme.json) | Sine metadata / Sine 元信息 / Sine 用メタデータ |
| [README.md](README.md) | Trilingual guide / 三语说明 / 3 言語のガイド |

## Credits · 致谢 · 謝辞

[Zen Browser](https://github.com/zen-browser/desktop) · [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) · [Sine](https://github.com/CosmoCreeper/Sine)

本项目是独立的兼容补丁，并非上述项目的官方组件。

This is an independent compatibility patch, not an official component of the projects above.

本プロジェクトは独立した互換性パッチであり、上記プロジェクトの公式コンポーネントではありません。
