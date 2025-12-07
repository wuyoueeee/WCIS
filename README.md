# 🏗️ 基于YOLO和大语言模型的墙体裂缝检测系统


**WCIS (Wall Crack Inspection System)** 是一款基于YOLO和大语言模型的墙体裂缝检测系统。它结合了 **YOLOv8** 的高精度目标检测能力和 **LLaVA** 多模态大语言模型的深度分析能力，不仅能精准识别墙体裂缝，还能智能分析裂缝成因并提供专业的修复建议。


---
代码获取地址：[https://mbd.pub/o/bread/YZWZmZlqZw==](https://mbd.pub/o/bread/YZWZmZlqZw==)

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/0aedc7f8e00344969d58f14664524da2.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/fa40b2a05bc74990b513643fcfeba277.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/4ac9c7c8c4094afbb7d6f3263d65dcd6.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/051acb61efc4498abbae0a719b1a73a0.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/70bc4d766fcf4b09b38d03ff46ed1b67.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/580a019199f74c449d64079d3ef285c3.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/79f1769a8a5049109d4d01a84f4c82f0.jpeg#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c465088bfc71469490ec85846482813b.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a9352d1dd96442d2aee7b9927204d87c.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/618ca94cca124b63b5b0d53d69edcfad.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/b1dd0aa70f2d4a0b92f3993463f00c6c.png#pic_center)

## 🏗️ 系统架构设计

本系统采用模块化分层架构设计，主要包含以下核心组件：

### 1. 表现层 (Presentation Layer)
- **Web UI**: 基于 **Gradio 4.0** 构建的交互式前端。
- **功能模块**:
    - `AdvancedWebInterface`: 主界面控制器，管理所有 Tab 页面的布局与交互。
    - **实时反馈**: 利用 Gradio 的 Event Listener 实现训练进度的实时轮询与展示。

### 2. 业务逻辑层 (Business Logic Layer)
- **核心控制器**: `crack_detection_system.py` 负责协调各子模块。
- **视频处理**: `video_detector.py` 使用 OpenCV 逐帧读取视频，调用检测器进行推理，并合成标注视频。
- **批量处理**: `web_interface_advanced.py` 内置多线程批处理逻辑，支持文件队列管理与结果打包。
- **历史管理**: `history_manager.py` 基于 SQLite/JSON 记录所有操作日志，支持持久化存储。

### 3. 算法核心层 (Algorithm Core Layer)
- **目标检测**:
    - **YOLOv8**: 负责定位裂缝坐标 (`bbox`)、计算置信度 (`confidence`)。
    - **多尺度推理**: 支持自适应图片缩放，确保小裂缝不漏检。
- **智能分析**:
    - **LLaVA**: 使用 `llava_analyzer.py` 连接 Ollama 服务。
    - **Prompt Engineering**: 内置专为裂缝分析设计的提示词模板，自动提取检测结果并生成专业报告。

---

## 🌟 核心功能特性

### 1. 🎯 高精度裂缝检测 (YOLOv8)
*   **实时检测**: 毫秒级响应，快速识别墙体表面的横向、纵向及网状裂缝。
*   **可视化标注**: 在原图上精准绘制检测框，采用工业级红/黄警示色标注，并显示置信度百分比。
*   **多模型支持**: 支持 YOLOv8n/s/m/l/x 全系列模型，用户可根据硬件算力在速度与精度间灵活权衡。

### 2. 🧠 LLaVA 智能成因分析
*   **深度诊断**: 集成 LLaVA 多模态大模型，系统不仅"看到"裂缝，更能结合上下文"理解"裂缝。
*   **专业报告**: 自动生成结构化报告，包含：
    *   **裂缝分布**: 描述裂缝的位置、走向。
    *   **严重程度**: 评估裂缝宽度、长度带来的风险等级。
    *   **可能成因**: 分析是否由地基沉降、温度收缩或外力撞击引起。
    *   **修复建议**: 提供灌浆、封闭或结构加固等专业建议。
*   **交互式问答**: 内置智能助手，用户可针对检测结果进行追问，获取更多工程建议。

### 3. 📂 全能检测模式
*   **单图检测**: 适合精细化分析单张图片，支持缩放查看细节。
*   **视频流检测**: 
    *   支持 MP4/AVI/MOV 等多格式视频流。
    *   **跳帧优化**: 可调节跳帧参数以平衡处理速度与检测密度。
    *   **自动合成**: 处理结束后自动生成带有标注框的视频文件，方便回看。
*   **批量处理 (High Efficiency)**: 
    *   支持一次性拖拽上传数百张现场照片。
    *   后台多线程队列处理，不阻塞主界面。
    *   自动生成 CSV 统计报表（包含文件名、裂缝数、最大置信度）。
    *   一键下载打包好的结果图集 (ZIP)。

### 4. 🚀 可视化模型训练
*   **零代码训练**: **无需编写任何 Python 代码**，在 Web 界面即可配置 Epochs、Batch Size、Image Size 等超参数。
*   **实时监控**: 
    *   动态展示 mAP50 / mAP50-95 指标变化曲线。
    *   实时滚动显示训练日志。
    *   可视化进度条预估剩余时间。
*   **硬件自适应**: 自动检测并优先使用 GPU (CUDA)，若无 GPU 则自动降级至 CPU 模式并调整推荐参数。

### 5. 📊 历史记录与数据管理
*   **全生命周期记录**: 所有的检测任务（图片、视频）和训练任务都会自动记录到本地数据库。
*   **数据回溯**: 
    *   支持按时间范围、任务类型（检测/训练）筛选。
    *   随时查看过往的检测结果详情和 LLaVA 分析报告。
*   **一键刷新**: 界面自动同步最新的后台数据状态，确保多人协作时信息一致。

---

## � 系统环境要求

为了获得最佳体验，建议满足以下配置：

| 组件 | 最低配置 | 推荐配置 |
| :--- | :--- | :--- |
| **操作系统** | Windows 10/11, Linux (Ubuntu 20.04+) | Windows 11 或 Ubuntu 22.04 |
| **Python** | 3.8 | 3.10 |
| **GPU** | NVIDIA GTX 1060 (6GB) | NVIDIA RTX 3060 (12GB) 或更高 |
| **内存** | 16 GB | 32 GB |
| **硬盘** | 20 GB 可用空间 | 50 GB SSD |

**必需软件:**
*   **Ollama**: 用于运行 LLaVA 模型 (智能分析功能必需)。
*   **FFmpeg**: 用于视频处理 (视频检测功能必需)。

---

## �️ 安装与部署指南

### 第一步: 环境准备
1.  **安装 Python 依赖**
    ```bash
    pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
    ```

### 第二步: 安装外部依赖

1.  **安装 Ollama (智能分析)**
    *   访问 [Ollama 官网](https://ollama.ai) 下载并安装。
    *   安装完成后，在终端运行以下命令下载 LLaVA 模型：
        ```bash
        ollama pull llava
        ```


### 第三步: 启动系统

运行以下命令启动高级 Web 界面：

```bash
python run_web_advanced.py
```

启动成功后，浏览器自动访问: `http://localhost:7860`

---

## 📖 详细使用手册

### Tab 1: 🎯 模型训练
在此页面，你可以对自己收集的数据集进行模型微调。
1.  **配置环境**: 系统会自动检测 GPU。选择 GPU 以获得更快的速度。
2.  **设置参数**: 
    *   **模型大小**: `n` (nano) 最快，`x` (extra large) 最准。推荐使用 `s` 或 `m`。
    *   **Epochs**: 训练轮数，通常 100-300 轮效果较好。
3.  **开始训练**: 点击"🚀 开始训练"，右侧日志区会显示实时进度。

### Tab 2: 📸 图片检测
1.  **加载模型**: 默认加载 `best.pt`，只需点击"📂 加载模型"。
2.  **上传图片**: 点击图片区域上传或拖拽图片。
3.  **配置项**:
    *   **置信度阈值**: 过滤低可信度的检测框。
    *   **启用 LLaVA**: 勾选后会调用大模型进行深度分析（速度较慢，约 5-10秒/张）。
4.  **查看结果**: 左侧显示检测图，右侧显示智能分析报告。

### Tab 3: 🎥 视频检测
1.  **上传视频**: 支持 MP4/AVI 等常见格式。
2.  **跳帧设置**: 默认为 5。数值越大处理越快，但可能漏检快闪过的裂缝。
3.  **下载结果**: 处理完成后，可以直接播放或通过顶部图标下载标注好的视频。

### Tab 4: 📂 批量检测 (新功能)
1.  **批量上传**: 一次性选择多张图片上传。
2.  **自动化处理**: 点击"🚀 开始批量处理"，系统将自动遍历所有图片。
3.  **结果导出**:
    *   **预览**: 缩略图形式预览检测结果。
    *   **下载**: 自动生成包含所有标注图片和 `summary_report.csv` 的 ZIP 压缩包。

### Tab 5: 💬 智能问答
*   这是一个通用的工程助手。你可以询问关于建筑规范、裂缝修复工艺、材料选择等任何问题。
*   底层调用 Ollama/LLaVA 模型进行对话。

### Tab 6: 📜 历史记录
*   **自动保存**: 所有的检测和训练任务都会被记录。
*   **筛选查看**: 点击"检测历史"或"训练历史"子标签查看详细表格。
*   **自动刷新**: 切换到此标签页时表格会自动刷新。

---

## ⚙️ 配置文件 (config.yaml) 说明

系统核心配置位于 `config.yaml`，可根据需要修改：

```yaml
web:
  host: "127.0.0.1"  # 监听地址
  port: 7860       # 端口号
  share: false     # 是否创建公网链接

yolov8:
  model_size: "n"  # 默认模型大小
  train:
    device: 0      # GPU索引
    batch_size: 16

llava:
  ollama_url: "http://localhost:11434" # Ollama服务地址
  model: "llava"
```

---

## 🔧 故障排查 (Troubleshooting)

| 问题现象 | 可能原因 | 解决方案 |
| :--- | :--- | :--- |
| **启动报错 `NameError: yaml`** | 依赖未正确导入 | 确保已运行 `pip install pyyaml` |
| **LLaVA 无法启用** | Ollama 服务未运行 | 检查是否安装 Ollama，尝试并在终端运行 `ollama serve` |
| **视频检测报错 `FileNotFound`** | 缺少 FFmpeg | 请安装 FFmpeg 并将其添加到系统环境变量 PATH 中 |
| **训练时显存溢出 (OOM)** | 批次大小过大 | 在训练设置中调小 `Batch Size` (如改为 8 或 4) |
| **端口被占用** | 程序已在运行 | 关闭其他终端窗口，或使用任务管理器结束 `python.exe` 进程 |

---


