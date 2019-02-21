---
title: AV/C 概述
description: AV/C 概述
ms.assetid: ff9e6dfc-7ab4-4b56-8b47-d3ea46b579e0
keywords:
- AV/C WDK，有关 AV/C
- Avc.sys 功能驱动程序 WDK
- 对等方 Avc.sys 模式 WDK AV/C
- 虚拟 Avc.sys 模式 WDK AV/C
- Avc.sys 功能驱动程序 WDK，有关 Avc.sys 函数驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e01a56600aca0974afda1d4099d42cc4baad68a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542278"
---
# <a name="avc-overview"></a>AV/C 概述





本部分介绍了 Microsoft 提供*Avc.sys* IEEE 1394 音频/视频控件 (AV/C) 协议提供支持的功能驱动程序。 本部分还提供了指导原则开发 AV/C 子单元 AV/C 符合设备的驱动程序。 AV/C 协议的详细信息位于[1394年贸易协会](https://go.microsoft.com/fwlink/p/?linkid=518448)网站。 请注意，供应商可能会使用 Microsoft 提供的驱动程序， *Msdv.sys*或*Mstape.sys*，以支持其磁带子单元连接，如果适用。 这些两个类驱动程序进行不必要的磁带子单元连接编写驱动程序。

*Avc.sys*提供两种操作模式： 对等和虚拟。 *Avc.sys*对等模式支持外部 C AV/设备上的子单元连接。 *Avc.sys*虚拟模式下启用计算机的功能公开为 AV/C 子单元，并因此以使计算机成为 AV/C 的有效目标的命令，从请求其他 AV/C 设备跨 IEEE 1394 串行总线。

*Avc.sys*使用单独的驱动程序堆栈，以支持对等子单元和虚拟子单元连接。 请注意，不同的模式不支持相同的功能。 有关对等子单元和虚拟子单元驱动程序堆栈的详细信息，请参阅[AV/C 驱动程序堆栈](av-c-driver-stacks.md)。

*Avc.sys*为对等方和虚拟子单元连接生成设备标识符 (Id)。 设备标识符将正确的 INF 文件和子单元驱动程序与将子单元连接相关联。 AV/C 设备连接到计算机时*Avc.sys*枚举作为对等子单元连接活动子单元连接。 然后，Windows 将加载相应的子单元驱动程序。 对等方和虚拟子单元设备标识符字符串的格式的详细信息，请参阅[AV/C 设备 Id](av-c-device-identifiers.md)。

*Avc.sys*提供了以下功能：

-   在 100 毫秒要求所代表的对等子单元驱动程序 AV/C 规范所定义的临时响应。 *Avc.sys*返回仅 AV/C 命令或查询的最终响应。 虚拟子单元驱动程序仍必须生成临时和最终响应。

-   路由从 AV/C 子单元连接到其各自的子单元驱动程序的响应。 子单元驱动程序仅其硬件从接收响应。

-   IEC 61883 即插即用枚举和内核流式处理 (KS) 框架中的控制。 有关即插即用连接和数据格式的详细信息，请参阅[AV/C 子单元插入连接和格式管理](av-c-subunit-plug-connection-and-format-management.md)。

子单元驱动程序可以使用 Stream 类接口或更高版本的 AVStream 接口。 此外，子单元驱动程序可以提供其自己 KS 代理插件公开给用户模式应用程序的自定义属性页。 有关详细信息，请参阅[AV/C 内核流式处理接口和 KS 代理插件](av-c-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins.md)。

通常情况下，供应商编写 AV/C 子单元驱动程序提供支持：

-   控制基于设备类型定义的子单元[1394年贸易协会规范](https://go.microsoft.com/fwlink/p/?LinkId=518448)网站

-   管理即插即用连接到基于 IEC 61883 标准通过 IEEE 1394 总线的流数据。 有关 61883 标准的详细信息，请参阅[IEC](https://go.microsoft.com/fwlink/p/?linkid=8732)网站。

 

 




