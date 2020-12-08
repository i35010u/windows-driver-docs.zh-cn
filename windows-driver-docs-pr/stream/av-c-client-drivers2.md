---
title: AV/C 客户端驱动程序
description: AV/C 客户端驱动程序
keywords:
- AVStream WDK，AV/C
- AV/C WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d5d57b9cfbc06311b5461582799fa232bd4ec86
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834013"
---
# <a name="avc-client-drivers"></a>AV/C 客户端驱动程序





Microsoft 在 Windows XP 及更高版本的操作系统中 (AV/C) 协议提供对 IEEE 音频/视频控制的支持。 AV/C 协议定义用于在 AV/C 兼容设备上发出命令和从子单元连接发送响应的方法。 如果你编写了支持子单位硬件的驱动程序，则可以在每个 IEEE 1394 串行总线上的设备上控制子单元连接。 请注意，你无需编写子单位驱动程序来支持磁带子单元连接，因为 Microsoft 为此功能提供了另外两个驱动程序， *Msdv.sys* 和 *Mstape.sys*。

为了支持 AV/C 协议，Microsoft 提供了以下两个驱动程序：

-   *Avc.sys*

-   *Avcstrm.sys*

*Avc.sys* 是一种函数驱动程序，它提供对建立和管理子单位/单元连接的支持。 *Avcstrm.sys* 是一个较低筛选器的驱动程序，它增加了对以下特定数据格式进行流式处理的支持：

-   标准定义数字视频 (SDDV，61883-2 规格) 

-   MPEG2-TS (61883-4 规范) 

根据设备的功能，可以使用 *Avcstrm.sys* 中提供的可选支持来帮助进行流式处理 SDDV 和/或 MPEG2 TS 数据。 如果 *Avcstrm.sys* 不支持你的设备使用的格式，则可以使用 *61883.sys* 提供的连接管理和数据流式处理功能，该功能位于驱动程序堆栈中。

子单位驱动程序应遵循 [Windows 驱动模型](../kernel/introduction-to-wdm.md) (WDM) 体系结构。 子单位驱动程序可以使用 Stream 类接口或 AVStream 接口。 AVStream 是用于开发子单位驱动程序的首选界面。 流类接口已过时，Microsoft 已不再进行进一步的开发。 有关这两个接口的详细信息，请参阅 [AV/C Kernel-Streaming Interface AND KS Proxy 插件](av-c-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins.md)。

有关如何编写 AV/C 子单位驱动程序的详细信息，请参阅 [av/c 概述](av-c-overview.md)。 有关如何使用 *Avcstrm.sys* 来协助流式传输数据的详细信息，请参阅 [AV/C 流式处理概述](av-c-streaming-overview.md)。

AV/C 协议支持基于 IEEE 1394 驱动程序堆栈和 IEC-61883 标准构建。 有关 IEC-61883 驱动程序堆栈的详细信息，请参阅 [iec-61883 客户端驱动程序](../ieee/iec-61883-client-drivers.md)。

 

