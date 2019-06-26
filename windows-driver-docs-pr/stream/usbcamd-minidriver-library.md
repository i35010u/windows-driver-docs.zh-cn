---
title: USBCAMD 微型驱动程序库
description: USBCAMD 微型驱动程序库
ms.assetid: 4447bf3d-5eaa-4de7-96bb-22dae68b44eb
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- WDK Windows 2000 内核流 USBCAMD2 微型驱动程序库
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b49a397adcd4ba4a22567b7979b408443cedda3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383126"
---
# <a name="usbcamd-minidriver-library"></a>USBCAMD 微型驱动程序库


USBCAMD2 是一个内核模式微型驱动程序库，简化了基于 USB 的流式处理相机的驱动程序开发。 使用 Stream 类的 USBCAMD2 微型驱动程序库接口 (*stream.sys*) 和 USB 总线驱动程序，以便您可以集中精力实现对照相机的属性和图像处理支持。

Microsoft 发布了原始 USBCAMD 微型驱动程序库与 Microsoft Windows 98 驱动程序开发工具包 (DDK)。 原始库已更新到 USBCAMD2 Windows Server 2003、 Windows XP 和 Windows 2000 Ddk 中和 Windows Driver Kit (WDK) 中。 添加了 USBCAMD2[的新功能](usbcamd2-features.md)仍 pin 提供支持，power （如休眠状态） 的管理和扩展的版本的原始 Api。

除了 USBCAMD2 微型驱动程序库中，Microsoft 还提供[USB 视频类 (UVC) 驱动程序](usb-video-class-driver.md)以支持基于 USB 的照相机。 UVC USBCAMD2 中支持的功能超集。 Microsoft 建议所有新的硬件开发使用 UVC 驱动程序。 如果，但是，不能更改硬件设计为 UVC 合规，则必须编写 USBCAMD2 微型驱动程序。

微型驱动程序库管理设备，其中包括处理与维护 USB 总线上的流相关联的启动、 停止、 同步和错误恢复问题从 USB 总线上的数据流。 USBCAMD2 调用供应商实现回调函数来处理硬件特定的操作，如内核的流属性支持、 选择备用 USB 接口设置和映像解压缩和处理。

照相机微型驱动程序负责：

-   实现支持流属性，例如内核[PROPSETID\_VIDCAP\_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)并[PROPSETID\_VIDCAP\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol).

-   确定数据流是否有效且当前或下一个视频帧的照相机微型驱动程序的一部分[ *CamProcessUSBPacketEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_process_packet_routine_ex)回调函数。

-   从流中提取视频帧和视频的帧执行处理，它们返回到调用应用程序在照相机微型驱动程序的前[ *CamProcessRawVideoFrameEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex)回调函数。

在 Windows 98 上为支持原始 USBCAMD 微型驱动程序库*usbcamd.sys*，但在 Windows 2000 上不受支持。 在 Windows 2000 和更高版本和 Windows Millennium Edition 及更高版本为这两者支持 USBCAMD2 *usbcamd.sysand usbcamd2.sys*。 原始 USBCAMD 微型驱动程序库和 USBCAMD2 都不支持在 64 位平台上。

对于 Windows 2000 及更高版本和 Windows Millennium Edition 和更高版本操作系统，照相机供应商应使用 USBCAMD2 微型驱动程序库而不是原始的库开发照相机微型驱动程序。

可以使用*usbintel*示例照相机微型驱动程序作为起始点。 此示例是在驱动程序开发工具包 (DDK) 和适用于 Windows XP 到 Windows 7 (生成 7600) 的 Windows Driver Kit (WDK) 中可用。 WDK 中安装到此示例*src\\wdm\\videocap\\usbintel* （如果它被选为安装的选项）。

**其他资源**

开发人员应熟悉中的材料[流式处理内核](kernel-streaming.md)，[流式处理微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)，并[视频捕获设备](video-capture-devices.md)。

有关其他开发人员信息，包括 USB 规范，请参阅[USB-如果开发人员区域](https://go.microsoft.com/fwlink/p/?linkid=8781)。

常规或使用者的信息，请参阅[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)。

 

 




