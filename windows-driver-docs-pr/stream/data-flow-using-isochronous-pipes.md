---
title: 使用常时等量管道的数据流
description: 使用常时等量管道的数据流
ms.assetid: a66f4191-53ce-4ca2-aae7-8fb24a1a9a16
keywords:
- 同步管道 WDK USBCAMD2
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- USBCAMD2 微型驱动程序库 WDK Windows 2000 内核流式处理
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
- 数据流 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7ddf3eaf87bd2d1890855fbd8b233d95c8547fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845066"
---
# <a name="data-flow-using-isochronous-pipes"></a>使用常时等量管道的数据流





USBCAMD2 通过请求两次传输32数据包，开始对同步管道进行流式处理。 每个数据包的最大大小都对应于所选替代设置中的最大大小。

**请注意**，同步管道上的   流式处理与 Microsoft DirectShow 流式处理无关。

 

仅当出现以下两种情况之一时，双缓冲区常传输请求才会持续提交到 USBCAMD2 并停止：

1.  发出 stop DirectShow 流状态（KSSTATE\_停止）。

2.  照相机微型驱动程序通过在调用[*USBCAMD\_SetIsoPipeState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_setisopipestate)的*PipeStateFlags*参数中传递 USBCAMD\_stop\_流式处理标志来请求 USBCAMD2 停止同步流式处理。

正在进行流式处理时，USBCAMD2 和相机微型驱动程序重复以下过程，直到流停止：

1.  对于 USBCAMD2 从 USB 总线驱动程序接收的每个数据包，USBCAMD2 会调用摄像微型驱动程序的[*CamProcessUSBPacketEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_packet_routine_ex)回调函数（为 IRQL = 调度\_级别）。 在出现错误情况时，照相机微型驱动程序必须设置相应的错误标志。 如果使用**CamProcessUSBPacketEx**的*FrameComplete*参数检测到新视频帧的开头，则微型驱动程序还必须设置新的视频帧标志。

2.  在照相机微型驱动程序确定了视频帧完成后，如果需要执行，则 USBCAMD2 将从工作线程的上下文中调用相机微型驱动程序的[*CamProcessRawVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex)回调函数来处理视频帧。颜色空间转换或解压缩。 USBCAMD2 将完成的原始帧返回到要由相机微型驱动程序处理的*sys.databases*类驱动程序，以 IRQL = 被动\_级别。 如果没有足够的帧数据或由于数据错误而在解压缩期间出现错误，例如， **CamProcessRawVideoFrameEx**的*BytesReturned*参数必须设置为0。

 

 




