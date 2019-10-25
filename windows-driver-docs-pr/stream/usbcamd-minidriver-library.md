---
title: USBCAMD 微型驱动程序库
description: USBCAMD 微型驱动程序库
ms.assetid: 4447bf3d-5eaa-4de7-96bb-22dae68b44eb
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- USBCAMD2 微型驱动程序库 WDK Windows 2000 内核流式处理
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b926488600223a4bcc974937304b43ed51c3926
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827368"
---
# <a name="usbcamd-minidriver-library"></a>USBCAMD 微型驱动程序库


USBCAMD2 是一个内核模式微型驱动程序库，可简化基于 USB 的流式处理相机的驱动程序开发。 USBCAMD2 微型驱动程序库*与 stream 类（db-library*）和 USB 总线驱动程序交互，以便您可以专注于实现对照相机属性和图像处理的支持。

Microsoft 通过 Microsoft Windows 98 驱动程序开发工具包（DDK）发布了原始 USBCAMD 微型驱动程序库。 已在 windows Server 2003、Windows XP 和 Windows 2000 Ddk 以及 Windows 驱动程序工具包（WDK）中将原始库更新为 USBCAMD2。 USBCAMD2 添加了[新功能](usbcamd2-features.md)，可为静止 pin、电源管理（如休眠）和扩展版本的原始 api 提供支持。

除了 USBCAMD2 微型驱动程序库以外，Microsoft 还提供了[Usb 视频类（UVC）驱动程序](usb-video-class-driver.md)来支持基于 USB 的相机。 UVC 支持 USBCAMD2 中的功能的超集。 Microsoft 建议对所有新硬件开发使用 UVC 驱动程序。 但是，如果无法将硬件设计更改为符合 UVC，则必须编写 USBCAMD2 微型驱动程序。

微型驱动程序库管理设备上 USB 总线上的数据流，其中包括处理与在 USB 总线上维护流相关联的启动、停止、同步和错误恢复问题。 USBCAMD2 调用由供应商实现的回调函数来处理特定于硬件的操作，例如内核流式处理属性支持、选择备用 USB 接口设置、图像解压缩和处理。

相机微型驱动程序负责：

-   实现对内核流式处理属性（如[PROPSETID\_VIDCAP\_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)和[PROPSETID\_VIDCAP\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)的支持。

-   确定数据流是否有效，以及照相机微型驱动程序的[*CamProcessUSBPacketEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_packet_routine_ex)回调函数中的当前或下一个视频帧的一部分。

-   从流中提取视频帧，并在视频帧返回到相机微型驱动程序的[*CamProcessRawVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex)回调函数中的调用应用程序之前对其执行处理。

原始 USBCAMD 微型驱动程序库在 Windows 98 上支持为*USBCAMD*，但在 windows 2000 上不受支持。 USBCAMD2 在 Windows 2000 和更高版本以及 Windows Millennium Edition 和更高版本上都支持*usbcamd sysand USBCAMD2*。 64位平台上不支持原始 USBCAMD 微型驱动程序库和 USBCAMD2。

对于 Windows 2000 和更高版本以及 Windows Millennium Edition 及更高版本的操作系统，照相机供应商应该使用 USBCAMD2 微型驱动程序库而不是原始库来开发相机微型驱动程序。

您可以使用*usbintel*示例照相机微型驱动程序作为起点。 此示例在适用于 Windows XP 的驱动程序开发工具包（DDK）和 Windows 驱动程序工具包（WDK）中提供，windows XP 通过 Windows 7 （版本7600）。 WDK 会将此示例安装到*src\\wdm\\videocap\\usbintel* （如果选择作为安装选项）。

**其他资源**

开发人员应熟悉[核心流式处理](kernel-streaming.md)、[流式传输微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)和[视频捕获设备](video-capture-devices.md)中的资料。

有关其他开发人员信息，包括 USB 规范，请参阅[usb-IF 开发人员区域](https://go.microsoft.com/fwlink/p/?linkid=8781)。

有关一般或使用者信息，请参阅[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)。

 

 




