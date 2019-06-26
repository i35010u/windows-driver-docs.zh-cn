---
title: 基于 PCI 的电视捕获
description: 基于 PCI 的电视捕获
ms.assetid: ae97d5f7-82de-4d6e-9835-ff4c7427f333
keywords:
- 筛选图形配置 WDK 视频捕获，基于 PCI 的电视捕获
- 基于 PCI 的电视捕获 WDK 视频捕获
- 电视捕获 WDK 视频捕获
- 电视捕获 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dff215e202b03cbfd8d684c2c725d201ec16ac3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370383"
---
# <a name="pci-based-tv-capture"></a>基于 PCI 的电视捕获


与电视/广播调谐器、 电视音频和纵横制基于 PCI 的捕获设备需要复杂的筛选器关系图，并通常是总线控制单独的预览和捕获流，每个都有可能不同的颜色空间和框架的支持的硬件维度。 此类设备还可以为 VBI 或时间码提供独立的流。

下图显示了单独的呈现器连接到的预览和捕获的流。

![连接到预览和捕获流的说明单独呈现器的关系图](images/pci-tvtuner.gif)

[PROPSETID\_ALLOCATOR\_控制](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)属性集是特定于此类型的筛选器关系图。

对于此类型的筛选器图形可选变体是通过使用连接到视频 Mixer/呈现器 (VMR) DirectShow 筛选器而不是标准的视频呈现器的预览针[ **KS\_VIDEOINFOHEADER2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_videoinfoheader2)结构格式。 此模式中配置时，显示设备的支持的视频端口管理器 (VPM) 和[的视频端口扩展](video-port-based-capture.md)(VPEs) 内核模式视频传输，将缓冲区传递到捕获设备和 MicrosoftDirectDraw 图面中处理[ **KS\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)结构。

视频捕获微型驱动程序然后可以保留缓冲区无限期-锁定、 填充、 解除锁定，和翻转图面，因为它们捕获到的所有权。 微型驱动程序必须注册运行全屏幕 MS-DOS 应用程序或排他模式游戏时指示应用层协议的丢失的通知。 在这些情况下，微型驱动程序应完成的缓冲区返回到捕获筛选器。

如果你的视频捕获硬件包括 FM 广播调谐器，请参阅[视频捕获设备使用广播调谐器](video-capture-devices-with-radio-tuners.md)。

 

 




