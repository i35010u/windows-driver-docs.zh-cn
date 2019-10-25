---
title: 基于 PCI 的电视捕获
description: 基于 PCI 的电视捕获
ms.assetid: ae97d5f7-82de-4d6e-9835-ff4c7427f333
keywords:
- 筛选器关系图配置 WDK 视频捕获、基于 PCI 的电视捕获
- 基于 PCI 的电视捕获 WDK 视频捕获
- TV 捕获 WDK 视频捕获
- 电视捕获 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55c3d06fe972f64c2c9fa41083b0929df8b8ecab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845308"
---
# <a name="pci-based-tv-capture"></a>基于 PCI 的电视捕获


使用电视/收音机调谐器、电视音频和 crossbars 的基于 PCI 的捕获设备需要复杂的筛选器图形，并且具有通常能够使用总线的硬件控制单独的预览和捕获流，每个都有可能不同的颜色空间和帧方面. 此类设备还可以为 VBI 或时间码提供单独的流。

下图显示了连接到预览和捕获流的单独呈现器。

![阐释连接到预览和捕获流的单独呈现器的关系图](images/pci-tvtuner.gif)

[PROPSETID\_分配器\_控件](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)属性集特定于此类筛选器关系图。

此类筛选器图形的可选变化形式是使用[**KS\_VIDEOINFOHEADER2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader2)结构格式将预览 pin 连接到视频混音器/呈现器（VMR）的 DirectShow 滤镜，而不是标准视频呈现器。 在此模式下配置时，如果显示设备支持视频端口管理器（VPM）和[视频端口扩展](video-port-based-capture.md)（VPEs）内核模式视频传输，则会将缓冲区与 Microsoft DirectDraw surface handles 一起传递到捕获设备[**KS\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)结构。

然后，视频捕获微型驱动程序可以在捕获到曲面时，无限期地保留缓冲区的所有权。 在运行全屏 MS-DOS 应用程序或独占模式游戏时，微型驱动程序必须注册指示缺少表面的通知。 在这些情况下，微型驱动程序应将缓冲区填写回捕获筛选器。

如果视频捕获硬件包含 FM 收音机调谐器，请参阅[使用收音机调谐器的视频捕获设备](video-capture-devices-with-radio-tuners.md)。

 

 




