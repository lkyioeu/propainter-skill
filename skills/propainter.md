---
name: propainter-generic
description: ProPainter 视频修复工具通用指南。当用户提到"ProPainter"、"视频修复"、"视频去水印"、"视频擦除"、"视频 inpainting"、"处理视频"、"制作 mask"、"去掉路人"、"去掉水印"、"去掉杂物"、"视频补帧"、"视频填充"时使用此 skill。提供完整的操作流程、命令模板和常见问题解答。适用于任何环境和硬件配置。
---

# ProPainter 视频修复工具通用指南

## 工具简介

ProPainter 是一个基于深度学习的视频修复工具，可以去除视频中的水印、路人、杂物等不需要的内容。

**核心功能**：
- 视频去水印
- 视频去路人
- 视频去杂物
- 视频内容修复

---

## 环境要求

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

---

## 安装步骤

### 1. 克隆仓库

```bash
git clone https://github.com/sczhou/ProPainter.git
cd ProPainter
```

### 2. 创建 Conda 环境

```bash
conda create -n propainter python=3.10 -y
conda activate propainter
```

### 3. 安装依赖

```bash
# 安装 PyTorch（根据 CUDA 版本选择）
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118

# 安装其他依赖
pip install -r requirements.txt
```

### 4. 下载预训练模型

模型会在首次运行时自动下载，或手动下载到 `weights/` 目录：

- `ProPainter.pth`
- `recurrent_flow_completion.pth`
- `raft-things.pth`

---

## 使用流程

### 1. 激活环境

```bash
conda activate propainter
```

### 2. 制作 Mask

```bash
python tools/mask_maker.py --video "你的视频.mp4"
```

**操作说明**：

| 操作 | 说明 |
|---|---|
| 鼠标左键按住 | 画 mask（绿色区域） |
| 鼠标右键按住 | 擦除 mask |
| 滚轮 | 调整画笔大小 |
| Ctrl+S | 保存 mask |
| Ctrl+Z | 撤销 |
| Ctrl+C | 清空 |
| Ctrl+Q | 退出 |

**保存位置**: `masks/mask.png`

### 3. 运行 ProPainter

**低分辨率模式（推荐，速度快）**：
```bash
python inference_propainter.py -i "你的视频.mp4" -m "masks/mask.png" --fp16 --height 360 --width 640
```

**原分辨率模式（质量高，速度慢）**：
```bash
python inference_propainter.py -i "你的视频.mp4" -m "masks/mask.png" --fp16
```

**输出位置**: `results/`

---

## 参数说明

| 参数 | 说明 | 默认值 |
|---|---|---|
| `-i` / `--video` | 输入视频路径 | 必填 |
| `-m` / `--mask` | mask 图片路径 | 必填 |
| `-o` / `--output` | 输出目录 | `results/` |
| `--fp16` | 半精度推理（省显存） | 关闭 |
| `--height` | 处理高度 | 原始高度 |
| `--width` | 处理宽度 | 原始宽度 |
| `--resize_ratio` | 缩放比例 | 1.0 |
| `--neighbor_length` | 局部邻帧数 | 10 |
| `--ref_stride` | 全局参考帧步长 | 10 |
| `--subvideo_length` | 子视频长度 | 80 |
| `--mask_dilation` | mask 膨胀系数 | 8 |

---

## 显存参考

| 分辨率 | 显存占用 | 处理速度 |
|---|---|---|
| 1280x720 | ~7.5GB | 慢 |
| 640x360 | ~2GB | 快 3-4 倍 |
| 320x240 | ~1GB | 最快 |

**建议**：
- 4GB 显存：使用 `--height 240 --width 320`
- 8GB 显存：使用 `--height 360 --width 640`
- 12GB+ 显存：可使用原分辨率

---

## 场景命令模板

### 场景 1：处理单个视频（推荐）

```bash
conda activate propainter && python tools/mask_maker.py --video "VIDEO_PATH" && python inference_propainter.py -i "VIDEO_PATH" -m "masks/mask.png" --fp16 --height 360 --width 640
```

### 场景 2：处理多个视频

```bash
conda activate propainter && for video in *.mp4; do python tools/mask_maker.py --video "$video" && python inference_propainter.py -i "$video" -m "masks/mask.png" --fp16 --height 360 --width 640; done
```

### 场景 3：高质量处理（原分辨率）

```bash
conda activate propainter && python tools/mask_maker.py --video "VIDEO_PATH" && python inference_propainter.py -i "VIDEO_PATH" -m "masks/mask.png" --fp16
```

### 场景 4：显存优化处理

```bash
conda activate propainter && python tools/mask_maker.py --video "VIDEO_PATH" && python inference_propainter.py -i "VIDEO_PATH" -m "masks/mask.png" --fp16 --height 240 --width 320 --neighbor_length 5 --ref_stride 20
```

---

## 目录结构

```
ProPainter/
├── inference_propainter.py  # 主程序
├── model/                   # 模型代码
├── core/                    # 核心代码
├── RAFT/                    # 光流估计
├── utils/                   # 工具函数
├── weights/                 # 预训练模型
├── tools/                   # mask 制作工具
├── masks/                   # 你的 mask
├── inputs/                  # 示例视频
├── results/                 # 输出结果
├── configs/                 # 配置文件
├── requirements.txt         # 依赖列表
└── README.md                # 说明文档
```

---

## 常见问题与故障排除

### Q1: 显存不够 (CUDA out of memory)

**解决方案**（按优先级）：
1. 加 `--fp16`（必加）
2. 降低分辨率：`--height 360 --width 640`
3. 进一步降到：`--height 240 --width 320`
4. 减小 `--neighbor_length 5`
5. 增大 `--ref_stride 20`
6. 减小 `--subvideo_length 50`

### Q2: 处理速度太慢

**解决方案**：
- 降低分辨率（最有效）
- 减小 `--neighbor_length`
- 增大 `--ref_stride`
- 使用 `--resize_ratio 0.5` 缩放视频

### Q3: 处理效果不好

**解决方案**：
- 制作更精确的 mask（完整覆盖）
- 增大 `--mask_dilation 15-20`
- 使用原分辨率模式
- 调整 `--neighbor_length` 和 `--ref_stride`

### Q4: 中文路径报错

**解决方案**：
- 复制视频到英文路径
- 使用英文文件名

### Q5: Mask 保存失败

**解决方案**：
- 确保用 Ctrl+S 保存
- 检查路径：`masks/mask.png`
- 检查磁盘空间
- 尝试用英文路径

### Q6: 命令执行失败

**解决方案**：
1. 检查 conda 环境是否激活
2. 检查路径是否正确
3. 检查文件是否存在
4. 检查读写权限

---

## 注意事项

1. **视频格式**: 支持 mp4、avi 等常见格式
2. **Mask 规则**: 白色=要修复的区域，黑色=保留
3. **显存管理**: 根据显存大小选择合适的分辨率
4. **路径规范**: 建议使用英文路径，避免中文路径问题
5. **备份原视频**: 处理前建议备份原视频

---

## 快速开始

```bash
# 1. 克隆仓库
git clone https://github.com/sczhou/ProPainter.git
cd ProPainter

# 2. 创建环境
conda create -n propainter python=3.10 -y
conda activate propainter

# 3. 安装依赖
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
pip install -r requirements.txt

# 4. 处理视频
python tools/mask_maker.py --video "你的视频.mp4"
python inference_propainter.py -i "你的视频.mp4" -m "masks/mask.png" --fp16 --height 360 --width 640
```

---

## 参考链接

- **GitHub**: https://github.com/sczhou/ProPainter
- **论文**: https://arxiv.org/abs/2309.03897
- **项目主页**: https://shangchenzhou.com/projects/ProPainter/
