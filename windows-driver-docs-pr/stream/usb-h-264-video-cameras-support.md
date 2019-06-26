---
title: USB H.264 视频摄像机支持
description: 从 Windows 8 开始，支持 H.264 视频编解码器 （编码器/解码器）。
ms.assetid: EB73E2B2-B34E-4DC1-807A-4990A54E6E8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8842072f52c9fe831f5b7bd8417b26530e626ff7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368820"
---
# <a name="usb-h264-video-cameras-support"></a>USB H.264 视频摄像机支持


从 Windows 8 开始，支持 H.264 视频编解码器 （编码器/解码器）。 编解码器进行编码和解码，便于高质量和高分辨率视频流式处理视频数据的算法为基础。 以下是一些在 Windows 8 UVC 类驱动程序，Usbvideo.sys，现成的支持的功能：

-   发现的 H.264 视频摄像机所支持的功能。
-   要在视频摄像机上的 H.264 流的会话协商。
-   流式处理从摄像机的 H.264 有效负载。
-   发现的 H.264 视频摄像机所支持的功能。

H.264 编解码器使用高效的视频压缩以减少并删除冗余的视频数据。 这样数字视频文件，以便有效地存储和通过网络交换。

如果您选择使用 UVC 类驱动程序 Usbvideo.sys 而不是专有的驱动程序，则必须根据下一步所述的准则在设备上实现视频流式处理的固件。

### <a name="firmware-guidelines"></a>固件的指导原则

UVC 类驱动程序 Usbvideo.sys 查询视频摄像机直接以获取其功能，然后驱动器在设备与所需的任何专有驱动程序。 有关这些准则的当前实现的信息，必须引用视频类驱动程序的 Microsoft 规范 H.264/MPEG-4。 另请参阅[Microsoft 建议的 H.264 USB 视频类扩展](https://go.microsoft.com/fwlink/p/?LinkId=233063)。

**请注意**  将在未来的标准文档中，若要在此位置中找到发布的官方指南：[视频设备规范的通用串行总线设备类定义](https://go.microsoft.com/fwlink/p/?linkid=516989)。

 

## <a name="related-topics"></a>相关主题
[**KS\_DATAFORMAT\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)  
[**KS\_DATARANGE\_H264\_VIDEO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_h264_video)  
[**KS\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_h264videoinfo)  



