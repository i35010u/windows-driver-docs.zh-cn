---
title: AV/C 客户端驱动程序
description: AV/C 客户端驱动程序
ms.assetid: 70d98c31-2da6-455b-91d8-59bed306b574
keywords:
- AVStream WDK、 AV/C
- AV/C WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5dfa74d7f2b1a9229e23579d29c8f950ac43ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384826"
---
# <a name="avc-client-drivers"></a>AV/C 客户端驱动程序





Microsoft 为 Windows XP 和更高版本操作系统中的 IEEE 音频/视频控制 (AV/C) 协议提供支持。 AV/C 协议定义 AV/C 合规的设备上用于颁发命令到和从子单元连接发送响应的方法。 您可以控制通过 IEEE 1394 串行总线符合 AV/C 协议，如果编写驱动程序以支持的子单元硬件的设备上的子单元连接。 请注意，不需要编写子单元驱动程序以支持磁带子单元连接，因为 Microsoft 提供此功能的两个其他驱动程序*Msdv.sys*并*Mstape.sys*。

为了支持 AV/C 协议，Microsoft 提供以下两个驱动程序：

-   *Avc.sys*

-   *Avcstrm.sys*

*Avc.sys*是提供支持，以建立和管理子单元/单位功能驱动程序插入连接。 *Avcstrm.sys*是添加了支持来帮助进行流式处理以下特定的数据格式的较低的筛选器驱动程序：

-   标准清晰数字视频 (SDDV，61883 2 规范)

-   MPEG2-TS （61883 4 规范）

根据你的设备的功能，可以使用中提供的可选支持*Avcstrm.sys*来帮助进行流式处理 SDDV 和/或 MPEG2-TS 数据。 如果*Avcstrm.sys*不支持你的设备，所使用的格式，则可以使用的连接管理和流式处理功能公开的数据*是 61883.sys*，位于较低的驱动程序堆栈。

子单元驱动程序应遵循[Windows 驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff565698)(WDM) 体系结构。 子单元驱动程序可以使用 Stream 类接口或 AVStream 接口。 AVStream 是用于开发的子单元驱动程序的首选的接口。 Stream 类接口已过时，但 Microsoft 已停止使用其进一步开发。 有关这两个接口的详细信息，请参阅[AV/C 内核流式处理接口和 KS 代理插件](av-c-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins.md)。

有关如何编写 AV/C 子单元驱动程序的详细信息，请参阅[AV/C 概述](av-c-overview.md)。 有关如何使用详细信息*Avcstrm.sys*若要帮助流式处理数据，请参阅[AV/C 流式处理概述](av-c-streaming-overview.md)。

AV/C 协议支持基于 IEEE 1394 驱动程序堆栈和 IEC 61883 标准。 IEC 61883 驱动程序堆栈的详细信息，请参阅[IEC 61883 客户端驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537188)。

 

 




