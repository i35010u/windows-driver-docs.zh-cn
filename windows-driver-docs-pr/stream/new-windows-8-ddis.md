---
title: Windows 8 的新 AVStream 接口
ms.assetid: B3C223BD-2A00-4B87-9D0E-557C0CA3F2DE
description: 提供有关适用于 Windows 8 的新的或已更新的 AVStream 流媒体驱动程序接口的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464821ab9aa5362610cd527c93f99f08ee959cad
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192145"
---
# <a name="new-avstream-interfaces-for-windows-8"></a>Windows 8 的新 AVStream 接口


这些 AVStream 流媒体驱动程序接口是 Windows 8 的新增或更新的：

## <a name="extended-camera-control-interface"></a>扩展相机控制接口


此现有接口的扩展用于在映像捕获期间控制相机功能。 请参阅 [扩展相机控制属性](extended-camera-control-properties.md)。

## <a name="usb-video-class-15-driver-update-h264-video-codec"></a>USB Video 类1.5 驱动程序更新 (视频编解码器) 


从 Windows 8 开始，支持新1.5 版本的 USB 视频类驱动程序。 此驱动程序更新合并了 h.264 视频编解码器标准，并在以下主题中进行了介绍：

-   [USB 视频类驱动程序概述](usb-video-class-driver-overview.md)
-   [USB H.264 视频摄像机支持](usb-h-264-video-cameras-support.md)
-   [**KS \_ DATAFORMAT \_ H264VIDEOINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)
-   [**KS \_ DATARANGE \_ H264 \_ 视频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_h264_video)
-   [**KS \_ H264VIDEOINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_h264videoinfo)

此外，已将一个新的常数值添加到 [**KS \_ VideoControlFlags**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_videocontrolflags) 枚举中。

## <a name="image-data-format-structures"></a>图像数据格式结构


这些结构与 JPEG 图像捕获和编码一起使用，以指定 pin (或 stream) 上的图像数据。

-   [**KS \_ DATAFORMAT \_ IMAGEINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_imageinfo)
-   [**KS \_ DATARANGE \_ 图像**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_image)

## <a name="device-removal-and-preemption"></a>设备删除和抢占


当照相机设备已从系统中删除 (丢失) 或被新的 UWP 应用抢占时，将使用此新接口。

-   [**KSEVENTSETID \_ 设备**](./kseventsetid-device.md)
-   [**KSEVENT \_ 设备**](/windows-hardware/drivers/ddi/ks/ne-ks-ksevent_device)
-   [**KSEVENT \_ 设备 \_ 丢失**](./ksevent-device-lost.md)
-   [**KSEVENT \_ 设备已被 \_ 抢占**](./ksevent-device-preempted.md)

 

