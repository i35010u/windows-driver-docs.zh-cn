---
title: Windows 8 的新 AVStream 接口
ms.assetid: B3C223BD-2A00-4B87-9D0E-557C0CA3F2DE
description: 提供有关 AVStream 流式处理媒体的信息是新的或更新 Windows 8 的驱动程序接口。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338b12fd0d7badc84ce0dde98274f90592ff39d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363269"
---
# <a name="new-avstream-interfaces-for-windows-8"></a>Windows 8 的新 AVStream 接口


这些 AVStream 流式处理媒体驱动程序接口是新的或更新 Windows 8:

## <a name="extended-camera-control-interface"></a>扩展的照相机控件接口


此扩展现有的接口用于映像捕获过程控制照相机功能。 请参阅[扩展相机控件属性](extended-camera-control-properties.md)。

## <a name="usb-video-class-15-driver-update-h264-video-codec"></a>USB 视频类 1.5 驱动程序更新 （H.264 视频编解码器）


从 Windows 8 开始支持 USB 视频类驱动程序的新版本 1.5。 此驱动程序更新合并的 H.264 视频编解码器标准，并在这些主题中所述：

-   [USB 视频类驱动程序概述](usb-video-class-driver-overview.md)
-   [USB H.264 视频摄像机支持](usb-h-264-video-cameras-support.md)
-   [**KS\_DATAFORMAT\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)
-   [**KS\_DATARANGE\_H264\_VIDEO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_h264_video)
-   [**KS\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_h264videoinfo)

此外，将新的常量值添加到[ **KS\_VideoControlFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ks_videocontrolflags)枚举。

## <a name="image-data-format-structures"></a>图像数据格式结构


这些结构是使用 JPEG 图像捕获和编码指定 pin （或流式处理） 上的图像数据。

-   [**KS\_DATAFORMAT\_IMAGEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_dataformat_imageinfo)
-   [**KS\_DATARANGE\_IMAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_image)

## <a name="device-removal-and-preemption"></a>设备删除和抢占


照相机设备已从 （丢失） 的系统中删除或已被占用由新的 UWP 应用时使用此新接口。

-   [**KSEVENTSETID\_设备**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-device)
-   [**KSEVENT\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksevent_device)
-   [**KSEVENT\_DEVICE\_LOST**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-device-lost)
-   [**KSEVENT\_设备\_已占用**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-device-preempted)

 

 




