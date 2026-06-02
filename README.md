# 🎬 ProPainter Skill for Claude Code

[![GitHub Stars](https://img.shields.io/github/stars/lkyioeu/propainter-skill?style=social)](https://github.com/lkyioeu/propainter-skill)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **ProPainter 视频修复工具的 Claude Code Skill** — 让 AI 帮你轻松去除视频中的水印、路人、杂物！

## ✨ 功能特点

- 🎯 **智能触发** — 30+ 中文关键词自动激活（视频修复、去水印、去路人、去字幕、去logo等）
- 📋 **完整指南** — 从安装到使用的全流程操作指南
- ⚡ **命令模板** — 4 种场景的即用命令模板
- 🔧 **故障排除** — 6 个常见问题的详细解决方案
- 💾 **显存优化** — 针对不同显存配置的优化建议

## 🚀 快速开始

### 方式 1：直接下载

```bash
# 下载 Skill 文件
curl -o ~/.claude/skills/propainter.md https://raw.githubusercontent.com/lkyioeu/propainter-skill/main/skills/propainter.md

# 在 Claude Code 中使用
# 输入 /propainter 或提到"视频修复"
```

### 方式 2：克隆仓库

```bash
# 克隆仓库
git clone https://github.com/lkyioeu/propainter-skill.git

# 复制 Skill 到 Claude Code 目录
cp propainter-skill/skills/propainter.md ~/.claude/skills/

# 在 Claude Code 中使用
# 输入 /propainter 或提到"视频修复"
```

## 📖 使用方法

### 在 Claude Code 中使用

1. **自动触发** — 提到以下关键词会自动激活：
   - **基础功能**：ProPainter、视频修复、去水印、去路人、去杂物
   - **高级功能**：视频去字幕、视频去logo、视频去日期、视频去时间戳
   - **处理模式**：视频批量修复、批量处理视频、视频自动化处理
   - **技术术语**：视频 inpainting、视频内容感知填充、视频对象移除
   - **操作相关**：制作 mask、视频擦除、视频抠图、视频清理

2. **手动调用** — 输入 `/propainter`

### Skill 提供的内容

- ✅ 完整的安装步骤
- ✅ 详细的操作流程
- ✅ 4 种场景的命令模板
- ✅ 参数说明和显存参考
- ✅ 6 个常见问题的解决方案
- ✅ 故障排除指南

## 🎯 适用场景

| 场景 | 说明 |
|---|---|
| **去水印** | 去除视频中的文字水印、LOGO |
| **去路人** | 去除视频中不需要的行人 |
| **去杂物** | 去除视频中的杂物、干扰物 |
| **去字幕** | 去除视频中的字幕文字 |
| **去日期/时间戳** | 去除视频中的日期、时间显示 |
| **视频修复** | 修复视频中的损坏区域 |

## 💻 系统要求

### 硬件要求

| 项目 | 最低要求 | 推荐配置 |
|---|---|---|
| **GPU** | NVIDIA GPU 4GB+ | NVIDIA GPU 8GB+ |
| **内存** | 8GB | 16GB+ |
| **硬盘** | 10GB | 20GB+ |

### 软件要求

- **操作系统**: Windows/Linux/macOS
- **Python**: 3.8-3.10
- **CUDA**: 11.7+
- **Conda**: 推荐使用

## 📚 相关资源

- **ProPainter 官方仓库**: [github.com/sczhou/ProPainter](https://github.com/sczhou/ProPainter)
- **论文**: [arxiv.org/abs/2309.03897](https://arxiv.org/abs/2309.03897)
- **项目主页**: [shangchenzhou.com/projects/ProPainter](https://shangchenzhou.com/projects/ProPainter/)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建你的分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开一个 Pull Request

## 📄 许可证

本项目基于 MIT 许可证开源 — 详见 [LICENSE](LICENSE) 文件

## ⭐ 支持

如果这个项目对你有帮助，请给一个 ⭐ Star！

---

**作者**: [lkyioeu](https://github.com/lkyioeu)

**仓库**: [github.com/lkyioeu/propainter-skill](https://github.com/lkyioeu/propainter-skill)
