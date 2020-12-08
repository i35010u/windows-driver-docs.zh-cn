---
title: 通过 USB 相机捕获静态帧
description: 通过 USB 相机捕获静态帧
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
ms.openlocfilehash: 8b313a1ca1d8c82cd0dcaff084650a383857c0e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839365"
---
# <a name="capturing-still-frames-from-a-usb-camera"></a>通过 USB 相机捕获静态帧





USBCAMD2 为单独的 [静止映像驱动程序](../image/still-image-drivers.md) 提供了功能，使其能够通过相机的批量管道从相机检索静止帧。

***<em>若要支持仍帧捕获，USBCAMD2 微型驱动程序必须执行以下</em>** _

-   从 PROPSETID VIDCAP VIDEOCONTROL 属性处理程序调用 [_USBCAMD \_ BulkReadWrite *](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_bulkreadwrite) \_ \_ ，并将一个指针传递到可在其中捕获静态图像的微型驱动程序分配缓冲区。 指针不能为 **NULL**。

-   然后，USBCAMD2 在开始大容量传输之前调用微型驱动程序的 [*CamNewVideoFrameEx*](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_new_frame_routine_ex) 回调函数。 如果相机微型驱动程序确定实际的静止帧小于 DirectShow 分配的最大大小，则它可以减少请求的大容量传输大小。

-   大容量传输完成后，USBCAMD2 将调用微型驱动程序的 [*CamProcessRawVideoFrameEx*](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex) 回调函数以允许微型驱动程序执行其他处理。

静止帧数据流适用于 *请求* 模型。 当应用程序请求静止帧时发生请求。 此外，仍然可以在 *推送* 模型中使用帧数据流。 当用户按下相机上的按钮时，会发生推送，触发设备事件。

*<strong>* 使用 * * *</strong> pull** * * * 模型从 STI 微型驱动程序检索静止帧 * * * * * * * *

-   打开与照相机关联的 WDM 视频捕获源筛选器。

-   打开在上一步中获取的筛选器句柄上的静止 pin。

-   在该 pin 上，用最大大小的缓冲区调用 **ReadFile** 。

-   将 "流状态" 从 "暂停" 设置为 "运行"。

-   获取指向 USBCAMD2 照相机微型驱动程序的 [PROPSETID \_ VIDCAP \_ VIDEOCONTROL](./propsetid-vidcap-videocontrol.md) 属性集的接口指针。

-   设置与 [**KSPROPERTY \_ VIDEOCONTROL \_ 模式**](./ksproperty-videocontrol-mode.md)关联的 *KS \_ VideoControlFlag \_ 触发器* 标志。

*<strong>* 支持使用 * * *</strong> 推送** * * * 模型从相机检索静止帧 * * * *

-   从 InitializeNewInterface 的微型驱动程序 INITIALIZE 设备处理程序中调用 [**USBCAMD \_ SRB**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)时，传递 *USBCAMD \_ CamControlFlag \_ EnableDeviceEvents* 标志 \_ \_ 。 微型驱动程序 \_ \_ 从其 [*AdapterReceivePacket*](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine) 回调函数中处理 SRB 初始化设备。

-   当用户将 [**KSEVENT \_ VIDCAPTOSTI \_ EXT \_ 触发器**](./ksevent-vidcaptosti-ext-trigger.md) 事件推送到已注册的图像处理应用程序时，USBCAMD2 会将触发器按钮推送到该应用程序。

若要取消请求的批量读取或写入，应用程序应调用 **CancelIO** ，并将句柄连接到静态静态。 如果需要通过 USB 大容量管道) 将表传输到相机 (，应用程序应调用 **WriteFile** ，并将句柄连接到静止 pin。

 

