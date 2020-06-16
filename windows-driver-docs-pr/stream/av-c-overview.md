---
title: AV/C 概述
description: AV/C 概述
ms.assetid: ff9e6dfc-7ab4-4b56-8b47-d3ea46b579e0
keywords:
- AV/C WDK，关于 AV/C
- Avc.sys 函数驱动程序 WDK
- 对等 Avc.sys 模式 WDK AV/C
- 虚拟 Avc.sys 模式 WDK AV/C
- Avc.sys 函数驱动程序 WDK，关于 Avc.sys 函数驱动程序
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: c430d5cbd982d9182e60f037bd1e5b19ad07ac52
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793747"
---
# <a name="avc-overview"></a>AV/C 概述

本部分介绍了 Microsoft 提供的*Avc.sys*函数驱动程序，该驱动程序提供对 IEEE 1394 音频/视频控制（AV/C）协议的支持。 本部分还提供了为 AV/C 兼容设备开发 AV/C 子单位驱动程序的指南。 [1394 贸易协会的](https://1394ta.org/library-2)网站上提供了 AV/C 协议的详细信息。 请注意，供应商可能使用 Microsoft 提供的驱动程序（ *Msdv.sys*或*Mstape.sys*）支持其磁带子单元连接（如果适用）。 这两个类驱动程序使写入磁带的驱动程序子单元连接不必要。

*Avc.sys*提供了两种运行模式：对等和虚拟。 *Avc.sys*对等机模式支持外部 AV/C 设备上的子单元连接。 利用*Avc.sys*虚拟模式，计算机功能可以作为 Av/c 子源公开，从而使计算机成为 Av/c 命令的有效目标，并使其在 IEEE 1394 串行总线上通过其他 Av/c 设备发出。

*Avc.sys*使用单独的驱动程序堆栈来支持对等子和虚拟子单元连接。 请注意，不同模式不支持相同的功能。 有关对等子和虚拟子单位驱动程序堆栈的详细信息，请参阅[AV/C 驱动程序堆栈](av-c-driver-stacks.md)。

*Avc.sys*会为对等互连和 virtual 子单元连接生成设备标识符（id）。 设备标识符将正确的 INF 文件和子单位驱动程序与子单元连接相关联。 当 AV/C 设备连接到计算机时， *Avc.sys*将活动的子单元连接作为对等子单元连接枚举。 然后，Windows 将加载相应的子单位驱动程序。 有关对等互连和虚拟子单位的设备标识符字符串的格式的详细信息，请参阅[AV/C 设备 id](av-c-device-identifiers.md)。

*Avc.sys*提供了以下功能：

- 在由 AV/C 规范代表对等子驱动程序定义的100毫秒要求内的过渡响应。 *Avc.sys*仅返回 AV/C 命令或查询的最终响应。 虚拟子单位驱动程序仍必须生成过渡和最终响应。

- 将来自 AV/C 子单元连接的响应路由到各自的子源驱动程序。 子单位驱动程序只接收来自其硬件的响应。

- IEC-61883 在内核流式处理（KS）框架内的插入枚举和控制。 有关插入连接和数据格式的详细信息，请参阅[AV/C 子单位插入连接和格式管理](av-c-subunit-plug-connection-and-format-management.md)。

子单位驱动程序可以使用 Stream 类接口或较新的 AVStream 接口。 而且，子单位驱动程序可以提供自己的 KS 代理插件来向用户模式应用程序公开自定义属性页。 有关详细信息，请参阅[AV/C 内核流式处理接口和 KS 代理插件](av-c-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins.md)。

通常情况下，供应商编写 AV/C 子单位驱动程序来提供对以下内容的支持：

- 根据[1394 贸易协会规范](https://1394ta.org/library-2)网站定义的设备类型控制子单位

- 管理插入连接，以便基于 IEEE 1394 总线上的 IEC-61883 标准流式传输数据。 有关61883标准的详细信息，请参阅[IEC](https://www.iec.ch/)网站。
