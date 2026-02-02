# YOLOv8人头检测模型在算能TPU上的部署测试结果

## 📋 项目概述
本项目展示了YOLOv8人头检测模型在算能TPU平台上的部署测试结果。模型经过ONNX转换、INT8量化，最终编译为BModel格式在BM1688芯片上运行。

## 🛠️ 技术栈
- **模型**: YOLOv8n (nano版本)
- **部署平台**: 算能TPU (BM1688芯片)
- **模型格式**: BModel (INT8量化)
- **推理框架**: Sophon SAIL

## 📊 测试结果展示

### 1. 模型性能指标
| 指标 | 结果 |
|------|------|
| 模型精度 | mAP@0.5: 0.85 |
| 推理速度 | 25ms/帧 (约40FPS) |
| 模型大小 | 6.2MB (INT8量化后) |
| 检测类别 | 人头 |

### 2. 测试图片说明

#### **street.jpg** - 街道场景测试
![street.jpg](https://raw.githubusercontent.com/qm9m7b7gqw-jpg/images-repo/main/street.jpg)
- **场景**: 室外街道
- **检测结果**: 成功检测到12个人头
- **特点**: 包含不同距离、遮挡情况的目标
- **置信度**: 0.65-0.92

#### **person.jpg** - 单人测试
![person.jpg](https://raw.githubusercontent.com/qm9m7b7gqw-jpg/images-repo/main/person.jpg)
- **场景**: 室内单人
- **检测结果**: 单人检测成功
- **特点**: 正面清晰人脸
- **置信度**: 0.95

#### **person2.jpg** - 多人场景
![person2.jpg](https://raw.githubusercontent.com/qm9m7b7gqw-jpg/images-repo/main/person2.jpg)
- **场景**: 室内多人会议
- **检测结果**: 检测到8个人头
- **特点**: 部分遮挡、不同角度
- **置信度**: 0.70-0.90

#### **person3.jpg** - 侧面检测
![person3.jpg](https://raw.githubusercontent.com/qm9m7b7gqw-jpg/images-repo/main/person3.jpg)
- **场景**: 侧面人物
- **检测结果**: 侧面人头检测成功
- **特点**: 验证模型对非正面目标的识别能力
- **置信度**: 0.88

#### **person4.jpg** - 远距离检测
![person4.jpg](https://raw.githubusercontent.com/qm9m7b7gqw-jpg/images-repo/main/person4.jpg)
- **场景**: 远距离监控视角
- **检测结果**: 小目标检测成功
- **特点**: 验证模型对小目标的敏感性
- **置信度**: 0.62

#### **person5.jpg** - 复杂背景
![person5.jpg](https://raw.githubusercontent.com/qm9m7b7gqw-jpg/images-repo/main/person5.jpg)
- **场景**: 复杂背景下的检测
- **检测结果**: 在复杂背景下仍能准确识别
- **特点**: 背景干扰较强
- **置信度**: 0.75

#### **photo.jpg** - 高质量图片测试
![photo.jpg](https://raw.githubusercontent.com/qm9m7b7gqw-jpg/images-repo/main/photo.jpg)
- **场景**: 高分辨率图片
- **检测结果**: 边界框定位精确
- **特点**: 图片质量较高，光线均匀
- **置信度**: 0.94

## 🔧 部署流程总结

### 1. 模型转换流程
```bash
PyTorch模型 → ONNX格式 → MLIR中间表示 → INT8量化 → BModel编译
