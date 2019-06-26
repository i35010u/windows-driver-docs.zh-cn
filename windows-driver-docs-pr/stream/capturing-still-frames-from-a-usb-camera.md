---
title: 通过 USB 相机捕获静态帧
description: 通过 USB 相机捕获静态帧
ms.assetid: 762021ea-753c-4cd2-9eec-1403ee918d4e
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- WDK Windows 2000 内核流 USBCAMD2 微型驱动程序库
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
- 仍捕获帧 WDK USBCAMD2
- 仍帧捕获 WDK USBCAMD2
- 大容量管道 WDK USBCAMD2
- 推送模型 WDK USBCAMD2
- 拉取模型 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcc85bc6fa240e59496d1d72dda61d584ddacfbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386662"
---
# <a name="capturing-still-frames-from-a-usb-camera"></a>通过 USB 相机捕获静态帧





USBCAMD2 提供了一个单独的功能[静止图像驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)从照相机的大容量管道通过照相机检索仍帧。

***<em>若要支持仍帧捕获 USBCAMD2 微型驱动程序必须执行以下</em>***

-   调用[ *USBCAMD\_BulkReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pfnusbcamd_bulkreadwrite)从 PROPSETID\_VIDCAP\_VIDEOCONTROL 属性处理程序并将指针传递给微型驱动程序分配的缓冲区到这可以捕获静止图像。 指针不能**NULL**。

-   USBCAMD2 然后调用微型驱动程序的[ *CamNewVideoFrameEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_new_frame_routine_ex)开始大容量传输之前的回调函数。 如果确定实际的静态帧是小于分配的 DirectShow 的最大大小，照相机微型驱动程序可以减少大容量传输的请求的大小。

-   USBCAMD2 大容量传输完成后，调用微型驱动程序的[ *CamProcessRawVideoFrameEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex)回调函数，以允许微型驱动程序执行其他处理。

仍能用帧数据流*拉取*模型。 当应用程序请求一个静态帧，拉取时发生。 或者，仍帧数据流还可在*推送*模型。 推送用户推送按钮在照像机上，触发设备事件时发生。

*<strong>* 若要使用 * * *</strong>拉取** * * * 若要检索的模型仍帧从 STI 微型驱动程序 * * *

-   打开与相机关联的 WDM 视频捕获源筛选器。

-   打开在上一步中获得对筛选器句柄仍 pin。

-   调用**ReadFile**上该 pin 的最大尺寸的缓冲区。

-   从暂停将流状态设置为运行。

-   获取到 USBCAMD2 照相机微型驱动程序的接口指针[PROPSETID\_VIDCAP\_VIDEOCONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)属性集。

-   设置*KS\_VideoControlFlag\_触发器*与关联的标志[ **KSPROPERTY\_VIDEOCONTROL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode).

*<strong>* 若要支持 * * *</strong>推送** * * * 若要检索的模型仍帧从照相机 * * *

-   传递*USBCAMD\_CamControlFlag\_EnableDeviceEvents*标志在调用时[ **USBCAMD\_InitializeNewInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)从内微型驱动程序的 SRB\_初始化\_设备处理程序。 微型驱动程序处理 SRB\_初始化\_中的设备及其[ *AdapterReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)回调函数。

-   将发送 USBCAMD2 [ **KSEVENT\_VIDCAPTOSTI\_EXT\_触发器**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcaptosti-ext-trigger)到注册的图像处理应用程序时用户将推送到触发器按钮的事件照相机。

若要取消请求的批量读取或写入，应用程序应调用**CancelIO**的句柄仍 pin。 如果表需要传输到 （通过 USB 大容量扩展管道） 摄像机，应用程序应调用**WriteFile**的句柄仍 pin。

 

 




