---
title: AV/C 流式处理概述
description: AV/C 流式处理概述
keywords:
- AV/C WDK，流筛选器驱动程序
- 流筛选器驱动程序 WDK AV/C
- Avcstrm.sys 流筛选器驱动程序 WDK
- Avcstrm.sys 流筛选器驱动程序 WDK，关于 Avcstrm.sys 流式处理筛选器驱动程序
- 筛选器驱动程序 WDK AV/C 流式处理
ms.date: 03/05/2021
ms.localizationpriority: medium
ms.openlocfilehash: f37433ff9fbafeea3997cc67397b6626ceb8b975
ms.sourcegitcommit: 57ffd9cfed01220923bdd0b20539e32a0e211caf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102236411"
---
# <a name="avc-streaming-overview"></a>AV/C 流式处理概述

本部分介绍了 Microsoft 提供的 AV/C 流式处理筛选器驱动程序（ *Avcstrm.sys*），以帮助从 AV/c 子单位传输媒体数据（如果该数据采用 SDDV 或 MPEG2TS 格式）。 这些格式是用于在媒体信号中存储数字数据的两种最常见的方法。

*Avcstrm.sys* 是较低级别的子单位筛选器驱动程序，它位于驱动程序堆栈中和任何子单位驱动程序的正上方 *Avc.sys* 和 *61883.sys* 。 AV/C 流筛选器驱动程序为 AV/C 协议驱动程序提供附加支持。 供应商可以使用此支持。

1394贸易关联磁带子单位规范支持不同的传输状态控制（如播放、暂停、记录和停止），而不考虑其媒体信号。 但是，同一子类型的数据格式可以相同，也可以不同。 例如，DV 和 DVHS 设备都包含磁带子单元连接。 但是，DV 通常使用基于 IEC 61883-2 规范的 SDDV 数据格式，而 DVHS 使用基于61883-4 规范的 MPEG2TS 数据格式。 因此，适用于磁带子单元连接的筛选器驱动程序必须支持 SDDV 和 MPEG2TS 数据格式，但对磁带子单位使用相同的设备控件。 这意味着每个子单位驱动程序必须重复相同的功能，以提供可识别格式的流式处理功能。

在61883和 AV/C 子单位驱动程序堆栈上控制 AV/C 子单位驱动程序需要使用驱动程序函数通过61883协议驱动程序提供 (DDIs) 来接收或传输数据流。 这些驱动程序函数执行以下操作：

- 分配同步资源并建立同步连接

- 队列数据缓冲区

- 附加并完成数据缓冲区的接收或传输

- 跨线程同步流状态

AV/C 流筛选器驱动程序依赖于 *61883.sys* 协议驱动程序。 *Avcstrm.sys* 使用 *61883.sys* 提供的 DDIs 来执行同步连接和同步数据流，并使用 *Avc.sys* 为外部设备控制发出 AV/C 命令。

有关在其上生成 AV/C 流式处理筛选器驱动程序的 AV/C 协议的详细信息，请参阅 [AV/c 概述](av-c-overview.md)。 有关61883协议的详细信息，请参阅 [IEC-61883 客户端驱动程序](../ieee/iec-61883-client-drivers.md)。

有关详细信息和资源，请参阅以下链接：

[Windows 驱动模型](../kernel/introduction-to-wdm.md)

[国际电工委员会 (International Electrotechnical Commission)](https://www.iec.ch/)
