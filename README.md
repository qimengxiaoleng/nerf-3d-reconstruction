# 基于神经辐射场的三维重建对比实验

## 项目简介
使用 NerfStudio 框架，对真实场景进行三维重建，
对比 NeRF (nerfacto) 与 TensoRF 两种方法在不同数据质量下的表现。

## 实验设置
- 数据：两组农夫山泉矿泉水瓶照片（各65张）
- 模型：nerfacto / TensoRF
- 硬件：RTX 4060 8GB
- 框架：NerfStudio + COLMAP + PyTorch

## 结果对比
| 实验 | 数据 | 模型 | 效果 |
|------|------|------|------|
| 1 | 高质量 | nerfacto | ✅ 最佳 |
| 2 | 低质量 | nerfacto | ✅ 良好 |
| 3 | 高质量 | TensoRF | ⚠️ 一般 |
| 4 | 低质量 | TensoRF | ❌ 最差 |

## 关键发现
1. nerfacto 对真实复杂场景鲁棒性显著优于 TensoRF
2. 提高物体占比能提升 TensoRF 的部分效果，但无法弥补模型表达力差距
3. 在消费级GPU上处理了 CUDA OOM、环境兼容性等工程问题

## 工程踩坑
- CUDA 显存不足：通过降低分辨率、限制采样数解决
- 3DGS (splatfacto) 环境编译失败：gsplat 与新版 MSVC 的兼容性问题
- NerfStudio 参数不生效：--max-num-iterations 在部分模型下被忽略

## 环境
Python 3.9 / PyTorch 2.x / NerfStudio / COLMAP / CUDA 12.x
