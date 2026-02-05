# Linux Kernel v6.1 for Allwinner T113-S3

本项目基于主线 Linux 内核 v6.1，针对 Allwinner T113-S3 SoC 进行适配。

适配了我自己的T113板卡

## 参考资料

- 《[MangoPi Dual T113 主线内核编译记录](https://bbs.aw-ol.com/topic/2338/mangopi-dual-t113-%E4%B8%BB%E7%BA%BF%E5%86%85%E6%A0%B8%E7%BC%96%E8%AF%91%E8%AE%B0%E5%BD%95)》

## 硬件平台

- **SoC**: Allwinner T113-S3（双核 ARM Cortex-A7）
- **目标板**: `sun8i-t113-iot-station`

## 已实现功能

### 基础系统支持
- 主线内核v6.1
- 双核正常启用
- 主频调度器支持

### 音频驱动增强
- 修改 codec 驱动，支持外置功放的 GPIO 使能控制，DAPM自动管理  

### 显示支持
- 新增 ST7735R 1.8 英寸 SPI LCD 驱动支持  
  - 设备树兼容名：`yyh,tft18019`
  - 分辨率：160*128

## 问题

### Cedrus 硬件视频解码器异常
- **现象**：  
  `cedrus` 驱动加载正常，`/dev/video0` 和 `/dev/media0` 设备节点已创建，但实际调用硬解时失败。
  
- **初步分析**：  
  怀疑与 CMA内存异常有关。系统启动后 CMA 区域被异常占满，导致解码缓冲区申请失败。
