---
title: 流媒体示例
description: 流媒体示例
ms.assetid: 797763a6-cd13-4d76-8ddb-75d812a8dde3
keywords:
- 流式处理媒体示例 WDK
- 采样 WDK 流式处理媒体
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 899454ffa42e413fa12b1f593b127c651bfc055d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190355"
---
# <a name="streaming-media-samples"></a>流媒体示例

可以在[“Microsoft 示例”门户](/samples/browse/?products=windows-wdk)上浏览和下载各个 Windows 10 驱动程序示例。 还可以在 GitHub 上克隆、分叉或下载 [Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) 存储库。

Windows 驱动程序示例的早期版本存档在这里：

- [Windows 8.1 驱动程序示例](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)

- [Windows 8 驱动程序示例](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.0%20Samples)

对于 Windows 7，示例包含在 [Windows 驱动程序工具包 (WDK) 7 下载](https://www.microsoft.com/download/details.aspx?id=11800)中。

| 示例名称 | 生成环境 | 目标操作系统 | PnP 驱动程序 | 内置驱动程序 | 示例说明 |
|--|--|--|--|--|--|
| AVStream) 的以筛选器为中心的模拟捕获驱动程序 (Avssamp | Windows 8.1<br><br>Windows 8<br><br>Windows 7 | Windows 8.1<br><br>Windows 8<br><br>Windows 7 | 否 | 否 | 提供具有功能音频的以筛选为中心的 AVStream 捕获驱动程序。 该驱动程序以 RGB24 或 YUV422 格式以 320 x 240 分辨率进行捕获，同时在循环中播放用户提供的脉冲代码调制 (PCM) 波形音频文件。 此示例演示如何编写以筛选为中心的 AVStream 微型驱动程序。 |
| AVStream 模拟硬件示例驱动程序 (Avshws)  |Windows 8.1<br><br>Windows 8<br><br>Windows 7 | Windows 8.1<br><br>Windows 8<br><br>Windows 7| 否 | 否 | 为模拟的硬件部分提供以 pin 为中心的 AVStream 捕获驱动程序。 驱动程序在 320 x 240 上通过直接 DMA 到捕获缓冲区中的 RGB24 或 YUV422 格式执行捕获。<br><br>示例的目的是演示如何编写以 pin 为中心的 AVStream 微型驱动程序。 该示例还演示了如何使用 AVStream 提供的相关功能实现 DMA。<br><br>此示例的功能增强了参数验证和溢出检测。 |
| SonyDCam 1394 网络摄像机驱动程序 | Windows 7 | Windows 7 | 否 | 是 | Microsoft Windows 驱动模型 (WDM) Stream 类视频捕获驱动程序，该驱动程序支持基于1394的数字照相机，该驱动程序符合1394贸易关联中的数字照相机规范。 |
| USBIntel 网络摄像机驱动程序 | Windows 7 | Windows 7 | 否 | 是 | Microsoft Windows 驱动模型 (WDM) stream 类视频捕获驱动程序。 |
| 软件调谐器 | Windows 7 | Windows 7 | 否 | 否 | 演示了几种数字网络类型。 |