---
title: USB H.264 视频摄像机支持
description: 从 Windows 8 开始，支持 h.264 视频编解码器（编码器/解码器）。
ms.assetid: EB73E2B2-B34E-4DC1-807A-4990A54E6E8D
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 59db5535dd594476b1bf88af11c995082df580c9
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111254"
---
# <a name="usb-h264-video-cameras-support"></a>USB H-p 视频相机支持

从 Windows 8 开始，支持 h.264 视频编解码器（编码器/解码器）。 编解码器基于用于对视频数据进行编码和解码的算法，这些算法允许高质量和高分辨率视频流式处理。 下面是 Windows 8 UVC 类驱动程序支持的一些功能，Usbvideo.sys，这是现成的：

- 对 H-p 视频摄像机支持的功能的发现。

- 视频摄像机上的 h.264 流的会话协商。

- 从相机流式传输 h.264 有效负载。

- 对 H-p 视频摄像机支持的功能的发现。

H-p 编解码器使用有效的视频压缩来减少和删除冗余视频数据。 这样，数字视频文件可以通过网络有效地存储和交换。

如果选择使用 UVC 类驱动程序 Usbvideo.sys 而不是专有的驱动程序，则必须按照下面所述的指导原则在设备上实施视频流式处理固件。

## <a name="firmware-guidelines"></a>固件指导原则

UVC 类驱动程序 Usbvideo.sys 直接查询视频摄像机以获取其功能，然后驱动设备，而无需专用驱动程序。 有关本指南的当前实现的信息，您必须参考适用于 H-p/MPEG-2 的 Microsoft 视频类驱动程序规范。 另请参阅[适用于 h-p 的 USB 视频类的 Microsoft 建议的扩展](https://docs.microsoft.com/previous-versions/windows/hardware/download/dn550976(v=vs.85))。

> [!NOTE]
> 官方准则将在将来的标准文档中发布，该文档位于此位置：[视频设备规范的通用串行总线设备类定义](https://www.usb.org/documents)。

## <a name="related-topics"></a>相关主题

[**KS \_ DATAFORMAT \_ H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)  

[**KS \_ DATARANGE \_ H264 \_ 视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_h264_video)  

[**KS \_ H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_h264videoinfo)  
