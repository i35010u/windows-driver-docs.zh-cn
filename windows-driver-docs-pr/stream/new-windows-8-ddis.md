---
title: Windows 8 的新 AVStream 接口
ms.assetid: B3C223BD-2A00-4B87-9D0E-557C0CA3F2DE
description: 提供有关 AVStream 流式处理媒体的信息是新的或更新 Windows 8 的驱动程序接口。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feb2052137a12b339916fab962d53ce3696b6dea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377777"
---
# <a name="new-avstream-interfaces-for-windows-8"></a>Windows 8 的新 AVStream 接口


这些 AVStream 流式处理媒体驱动程序接口是新的或更新 Windows 8:

## <a name="extended-camera-control-interface"></a>扩展的照相机控件接口


此扩展现有的接口用于映像捕获过程控制照相机功能。 请参阅[扩展相机控件属性](extended-camera-control-properties.md)。

## <a name="usb-video-class-15-driver-update-h264-video-codec"></a>USB 视频类 1.5 驱动程序更新 （H.264 视频编解码器）


从 Windows 8 开始支持 USB 视频类驱动程序的新版本 1.5。 此驱动程序更新合并的 H.264 视频编解码器标准，并在这些主题中所述：

-   [USB 视频类驱动程序概述](usb-video-class-driver-overview.md)
-   [USB H.264 视频摄像机支持](usb-h-264-video-cameras-support.md)
-   [**KS\_DATAFORMAT\_H264VIDEOINFO**](https://msdn.microsoft.com/library/windows/hardware/hh463996)
-   [**KS\_DATARANGE\_H264\_VIDEO**](https://msdn.microsoft.com/library/windows/hardware/hh464002)
-   [**KS\_H264VIDEOINFO**](https://msdn.microsoft.com/library/windows/hardware/hh464008)

此外，将新的常量值添加到[ **KS\_VideoControlFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff567696)枚举。

## <a name="image-data-format-structures"></a>图像数据格式结构


这些结构是使用 JPEG 图像捕获和编码指定 pin （或流式处理） 上的图像数据。

-   [**KS\_DATAFORMAT\_IMAGEINFO**](https://msdn.microsoft.com/library/windows/hardware/jj151598)
-   [**KS\_DATARANGE\_IMAGE**](https://msdn.microsoft.com/library/windows/hardware/jj151599)

## <a name="device-removal-and-preemption"></a>设备删除和抢占


照相机设备已从 （丢失） 的系统中删除或已被占用由新的 UWP 应用时使用此新接口。

-   [**KSEVENTSETID\_设备**](https://msdn.microsoft.com/library/windows/hardware/jj156036)
-   [**KSEVENT\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/jj151588)
-   [**KSEVENT\_DEVICE\_LOST**](https://msdn.microsoft.com/library/windows/hardware/jj156039)
-   [**KSEVENT\_设备\_已占用**](https://msdn.microsoft.com/library/windows/hardware/jj156040)

 

 




