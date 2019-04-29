---
title: 使用常时等量管道的数据流
description: 使用常时等量管道的数据流
ms.assetid: a66f4191-53ce-4ca2-aae7-8fb24a1a9a16
keywords:
- 等时管道 WDK USBCAMD2
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- WDK Windows 2000 内核流 USBCAMD2 微型驱动程序库
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
- 数据流 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d88d01b372ea8c9a73794786fe88e322bca03748
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374125"
---
# <a name="data-flow-using-isochronous-pipes"></a>使用常时等量管道的数据流





USBCAMD2 开始同步管道上传输请求两个 32 数据包的传输。 每个数据包都有对应于所选的替代设置的最大大小的最大大小。

**请注意**  等时管道上的流式处理是独立于 Microsoft DirectShow 流式处理。

 

双缓冲区同步传输请求持续提交到 USBCAMD2 和停止仅当以下两种情况之一发生：

1.  发出停止 DirectShow 流状态 (KSSTATE\_停止)。

2.  照相机微型驱动程序请求 USBCAMD2 停止传输同步数据流表示通过 USBCAMD\_停止\_中的流式处理标志*PipeStateFlags*对的调用中的参数[ *USBCAMD\_SetIsoPipeState*](https://msdn.microsoft.com/library/windows/hardware/ff568629)。

正在流式处理时，USBCAMD2 和照相机微型驱动程序请流式处理停止前重复以下过程：

1.  USBCAMD2 调用照相机微型驱动程序的[ *CamProcessUSBPacketEx* ](https://msdn.microsoft.com/library/windows/hardware/ff557631)回调函数 (在 IRQL = 调度\_级别) 为每个数据包 USBCAMD2 接收从 USB 总线驱动程序。 照相机微型驱动程序必须设置在错误条件的情况下的相应的错误标志。 如果将使用检测新的视频帧的开头，微型驱动程序还必须设置新的视频帧标志*FrameComplete*的参数**CamProcessUSBPacketEx**。

2.  USBCAMD2 照相机微型驱动程序已确定视频帧的已完成后，调用照相机微型驱动程序的[ *CamProcessRawVideoFrameEx* ](https://msdn.microsoft.com/library/windows/hardware/ff557625) （从工作线程的上下文） 的回调函数若要处理的视频帧，如果需要执行颜色空间转换或解压缩。 USBCAMD2 返回到的已完成原始帧*stream.sys*类驱动程序来处理的照相机微型驱动程序在 IRQL = 被动\_级别。 如果没有足够的帧数据或者时出错解压缩由于错误数据，例如，则*BytesReturned*参数**CamProcessRawVideoFrameEx**必须设置为 0。

 

 




