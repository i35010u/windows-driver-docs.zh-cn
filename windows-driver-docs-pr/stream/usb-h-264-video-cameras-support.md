---
title: USB H.264 视频摄像机支持
description: 从 Windows 8 开始，支持 h.264 视频编解码器（编码器/解码器）。
ms.assetid: EB73E2B2-B34E-4DC1-807A-4990A54E6E8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1ca0f9bb2c36928f7935e51dc5d683a9331a7ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842621"
---
# <a name="usb-h264-video-cameras-support"></a>USB H.264 视频摄像机支持


从 Windows 8 开始，支持 h.264 视频编解码器（编码器/解码器）。 编解码器基于用于对视频数据进行编码和解码的算法，这些算法允许高质量和高分辨率视频流式处理。 下面是 Windows 8 UVC 类驱动程序（Usbvideo）支持的部分功能：

-   对 H-p 视频摄像机支持的功能的发现。
-   视频摄像机上的 h.264 流的会话协商。
-   从相机流式传输 h.264 有效负载。
-   对 H-p 视频摄像机支持的功能的发现。

H-p 编解码器使用有效的视频压缩来减少和删除冗余视频数据。 这样，数字视频文件可以通过网络有效地存储和交换。

如果选择使用 UVC 类驱动程序 Usbvideo 而不是专有驱动程序，则必须根据接下来介绍的指南在设备上实施视频流固件。

### <a name="firmware-guidelines"></a>固件指导原则

UVC 类驱动程序 Usbvideo 会直接查询视频摄像机，以获取其功能，并驱动设备，而无需专有驱动程序。 有关本指南的当前实现的信息，您必须参考适用于 H-p/MPEG-2 的 Microsoft 视频类驱动程序规范。 另请参阅[适用于 h-p 的 USB 视频类的 Microsoft 建议的扩展](https://go.microsoft.com/fwlink/p/?LinkId=233063)。

**请注意**  将在将来的标准文档中发布官方准则，此位置为[视频设备规范的通用串行总线设备类定义](https://go.microsoft.com/fwlink/p/?linkid=516989)。

 

## <a name="related-topics"></a>相关主题
[**KS\_DATAFORMAT\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)  
[**KS\_DATARANGE\_H264\_视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_h264_video)  
[**KS\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_h264videoinfo)  



