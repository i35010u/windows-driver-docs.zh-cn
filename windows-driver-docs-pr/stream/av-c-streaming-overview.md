---
title: AV/C 流式处理概述
description: AV/C 流式处理概述
ms.assetid: c500fad7-26b7-4507-953e-258dd9c91253
keywords:
- AV/C WDK，Stream 筛选器驱动程序
- Stream 筛选器驱动程序 WDK AV/C
- Avcstrm.sys 流式处理筛选器驱动程序 WDK
- 流式处理有关 Avcstrm.sys 流式处理筛选器驱动程序筛选器驱动程序 WDK，Avcstrm.sys
- 筛选器驱动程序 WDK AV/C 的流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbf100cd30e67d04b732019bf2abf4b2d66058bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386746"
---
# <a name="avc-streaming-overview"></a>AV/C 流式处理概述

本部分介绍 AV/C 流式处理筛选器驱动程序*Avcstrm.sys*，Microsoft 提供了用于处理流媒体数据从 AV/C 子单元，如果该数据位于任一 SDDV 或 MPEG2TS 格式。 这些格式是用于存储媒体信号中的数字数据的两个最常见方法。

*Avcstrm.sys*是较低级别子单元的筛选器驱动程序，直接位于上面*Avc.sys*并*是 61883.sys*中驱动程序堆栈和下方的任何子单元驱动程序。 AV/C Stream 筛选器驱动程序为 AV/C 协议驱动程序提供额外支持。 它是可选的供应商联系以使用这一支持。

磁带子单元规范 (位于[1394年贸易协会](https://go.microsoft.com/fwlink/p/?LinkId=518448)网站) 的支持不同的传输状态控件，如播放、 暂停、 记录和停止，而不考虑其媒体信号。 但是，相同的子单元类型的数据格式可以是相同或不同。 例如，DV 和 DVHS 设备包含磁带子单元连接。 但是，DV 通常使用基于 IEC 61883 2 规范，SDDV 数据格式而 DVHS 使用 61883 4 规范为基础的 MPEG2TS 数据格式。 因此，磁带子单元连接的筛选器驱动程序必须支持 SDDV 和 MPEG2TS 数据格式，但使用相同的设备控制进行磁带子单元。 这意味着每个子单元驱动程序必须重复相同的功能提供识别格式的流式传输功能。

控制 61883 和 AV/C 子单元驱动程序堆栈上的 AV/C 子单元驱动要求驱动程序函数来接收或传输使用设备驱动程序接口 (DDIs) 61883 协议驱动程序提供的数据流。 这些驱动程序函数执行以下操作：

- 将同步资源分配和建立同步连接

- 队列数据缓冲区

- 附加并完成接收或传输数据缓冲区

- 在线程间同步流状态

AV/C Stream 筛选器驱动程序依赖于*是 61883.sys*协议驱动程序。 *Avcstrm.sys*使用提供的 DDIs*是 61883.sys*为了执行同步连接和流式处理同步数据，并且它使用*Avc.sys*发布外部设备控制的 AV/C 命令.

有关 AV/C 协议在其构建 AV/C 流式处理筛选器驱动程序的详细信息，请参阅[AV/C 概述](av-c-overview.md)。 有关 61883 协议的详细信息，请参阅[IEC 61883 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-client-drivers)。

有关详细信息和资源，请参阅以下链接：

[Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)

[1394 贸易协会规范](https://go.microsoft.com/fwlink/p/?linkid=518448)

[国际电工委员会](https://go.microsoft.com/fwlink/p/?linkid=8732)
