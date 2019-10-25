---
title: 通过 USB 相机捕获静态帧
description: 通过 USB 相机捕获静态帧
ms.assetid: 762021ea-753c-4cd2-9eec-1403ee918d4e
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- USBCAMD2 微型驱动程序库 WDK Windows 2000 内核流式处理
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
- 捕获静止帧 WDK USBCAMD2
- 静止帧捕获 WDK USBCAMD2
- 批量管道 WDK USBCAMD2
- 推送模型 WDK USBCAMD2
- 拉取模型 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1499661294b68fe5ea22d1dad939b825cbfb85e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844740"
---
# <a name="capturing-still-frames-from-a-usb-camera"></a>通过 USB 相机捕获静态帧





USBCAMD2 为单独的[静止映像驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)提供了功能，使其能够通过相机的批量管道从相机检索静止帧。

***<em>若要支持仍帧捕获，USBCAMD2 微型驱动程序必须执行以下</em>***

-   从 PROPSETID\_VIDCAP\_VIDEOCONTROL 属性处理程序中调用[*USBCAMD\_BulkReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_bulkreadwrite) ，并将指针传递到可在其中捕获静态图像的微型驱动程序分配缓冲区。 指针不能为**NULL**。

-   然后，USBCAMD2 在开始大容量传输之前调用微型驱动程序的[*CamNewVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_new_frame_routine_ex)回调函数。 如果相机微型驱动程序确定实际的静止帧小于 DirectShow 分配的最大大小，则它可以减少请求的大容量传输大小。

-   大容量传输完成后，USBCAMD2 将调用微型驱动程序的[*CamProcessRawVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex)回调函数以允许微型驱动程序执行其他处理。

静止帧数据流适用于*请求*模型。 当应用程序请求静止帧时发生请求。 此外，仍然可以在*推送*模型中使用帧数据流。 当用户按下相机上的按钮时，会发生推送，触发设备事件。

*使用 * * *</strong> pull * * * * 模型从 STI 微型驱动程序检索静止帧 * * * * * * * * <strong>**

-   打开与照相机关联的 WDM 视频捕获源筛选器。

-   打开在上一步中获取的筛选器句柄上的静止 pin。

-   在该 pin 上，用最大大小的缓冲区调用**ReadFile** 。

-   将 "流状态" 从 "暂停" 设置为 "运行"。

-   获取指向 USBCAMD2 照相机微型驱动程序的[PROPSETID\_VIDCAP\_VIDEOCONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)属性集的接口指针。

-   设置与[**KSPROPERTY\_VIDEOCONTROL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode)关联的*KS\_VideoControlFlag\_触发器*标志。

*支持使用 * * *</strong>推送 * * * * 模型从相机检索静止帧 * * * * <strong>**

-   从 InitializeNewInterface 的微型驱动程序\_初始化\_设备处理程序中调用[**USBCAMD\_SRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)时，传递*USBCAMD\_CamControlFlag\_EnableDeviceEvents*标志。 微型驱动程序处理 SRB\_从其[*AdapterReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)回调函数内初始化\_设备。

-   当用户将[**KSEVENT\_VIDCAPTOSTI\_EXT\_触发器**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcaptosti-ext-trigger)事件推送到已注册的图像处理应用程序时，USBCAMD2 会将触发器按钮推送到该应用程序。

若要取消请求的批量读取或写入，应用程序应调用**CancelIO** ，并将句柄连接到静态静态。 如果需要将表传输到相机（通过 USB 批量输出管道），应用程序应调用**WriteFile** ，并将句柄连接到静止 pin。

 

 




