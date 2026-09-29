# 剪映自动化编辑技能 (jianying-editor-skill)

一个面向 AI 助手的剪映（JianYing Pro）自动化剪辑技能。通过自然语言描述需求，即可自动完成**文案、配音、字幕、配乐、特效、录屏、网页动效转视频、导出**的整套剪辑流程。

> 本仓库由 [Levenli](https://github.com/Levenli) 维护，基于 [luoluoluo22/jianying-editor-skill](https://github.com/luoluoluo22/jianying-editor-skill)（MIT License）整理与二次开发，感谢原作者的杰出贡献。

## 平台支持

| 平台 | 状态 | 说明 |
| --- | --- | --- |
| Windows | 推荐使用 | 支持草稿生成、素材导入、字幕、配音、云端素材下载、录屏和自动导出（依赖 Windows UI Automation，剪映 5.9 或更低版本最稳） |
| macOS | 支持草稿生成 | 支持新版草稿目录探测、`draft_info.json` 草稿生成、FFmpeg 媒体解析兜底和录屏适配；自动导出不支持，需在剪映内手动导出 |
| CapCut 国际版 | 不支持 | 仅适配国内版剪映专业版（JianyingPro） |
| 手机端剪映 | 不支持 | 仅面向桌面版草稿工程 |

## 能做什么

| 功能 | 说明 |
| --- | --- |
| 素材导入 | 视频、音频、图片一句话丢进时间轴，自动排列 |
| AI 配音 | 输入文案自动生成语音，支持剪映原生音色和微软语音 |
| 字幕生成 | 根据配音自动拆句、逐句对齐字幕，支持打字机等动画效果 |
| 自动配乐 | 本地音乐或剪映素材库的云端音乐曲 |
| 特效 / 转场 / 滤镜 | 按名字搜索剪映自带特效库，一句话应用 |
| 网页动效转视频 | 用 HTML/JS/Canvas 写动画，自动录屏变成视频素材导入剪映 |
| 录屏 + 智能变焦 | 录制屏幕操作，自动给鼠标点击位置加缩放和红圈标记 |
| 影视解说 | AI 分析视频内容，自动生成分镜脚本并合成解说视频 |
| 自动导出 | Windows UI 自动化导出 MP4，macOS 生成草稿后手动导出 |
| 关键帧动画 | 缩放、位移、透明度等关键帧，做出运镜效果 |
| 复合片段 | 像嵌套工程一样，把多个子项目组合成一个完整视频 |

## 快速开始

### 安装技能

在支持 Agent Skills 的编辑器（Antigravity / Trae / Claude Code / Cursor 等）项目目录中：

```bash
git clone https://github.com/<your-username>/jianying-editor-skill.git skills/jianying-editor
```

或按各编辑器的约定目录安装（`.claude/skills/`、`.trae/skills/`、`.agent/skills/` 等）。

### 安装 Python 依赖

```bash
pip install -r requirements.txt

# 网页捕获环境（Web-to-Video 功能必填）
playwright install chromium
```

技能默认自动探测剪映安装位置，若探测失败，请告知 AI 你的草稿目录：
- **Windows**: `C:\Users\<用户名>\AppData\Local\JianyingPro\User Data\Projects\com.lveditor.draft`
- **macOS**: `/Users/<用户名>/Movies/JianyingPro/User Data/Projects/com.lveditor.draft`

## 使用示例

跟 AI 说这些自然语言指令即可：

- "帮我随便剪一个视频看看效果"
- "把 `D:\旅行素材` 文件夹里的视频和照片剪成一个 Vlog，配轻快音乐，加标题'周末露营记'"
- "写一段关于'秋天的第一杯奶茶'的短视频文案，配温柔女声旁白和字幕，找温馨 BGM"
- "这个视频 `D:\电影片段.mp4`，帮我做一个 60 秒影视解说"
- "我要录一段操作教程，帮我启动录屏，录完自动导入剪映"
- "帮我用网页写一个星空粒子片头动画，5 秒，然后导入剪映"

更详细的使用指南见 [usage.md](usage.md)。

## 目录说明

- `SKILL.md` — 给 AI 看的技能说明书
- `scripts/` — 核心自动化脚本（草稿生成、导出、素材检索等）
- `rules/` — 各功能场景的操作规则
- `docs/` — Agent 执行手册与命令 SOP
- `examples/` — 完整工作流示例代码
- `references/` — 参考文档与示例资料（非运行时依赖）
- `tools/recording/` — 录屏工具
- `assets/` — 演示用测试视频和音乐
- `data/` — 云端音乐 / 文字样式等素材库索引

## 常见问题

1. **看不到新生成的草稿？** 剪映不会实时刷新文件列表，生成草稿后重启剪映，或随便点进一个旧草稿再退出。
2. **自动导出失败？** 导出脚本模拟鼠标键盘操作，运行时请勿动鼠标键盘；仅支持 Windows，剪映 5.9 或更早版本最稳；macOS 请在剪映中手动导出。

## 开源协议

- 本项目基于 [MIT License](LICENSE) 开源。
- 底层草稿数据映射与基础控制层内嵌并二次开发了开源项目 [pyJianYingDraft](https://github.com/GuanYixuan/pyJianYingDraft)（作者：GuanYixuan），该模块遵循 [Apache License 2.0](scripts/vendor/pyJianYingDraft/LICENSE)。
- 原项目作者：[luoluoluo22](https://github.com/luoluoluo22)，版权声明见 [LICENSE](LICENSE)。
