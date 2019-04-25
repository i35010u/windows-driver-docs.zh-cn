---
title: 网络适配器 WDF 类扩展 (NetAdapterCx)
description: 网络适配器 WDF 类扩展 (NetAdapterCx)
ms.assetid: 74719A80-AE66-410F-85B7-31B6F455A818
keywords:
- 网络适配器类扩展, 网络适配器 WDF 类扩展, NetAdapterCx, NetCx
ms.date: 03/21/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.custom: 19H1
ms.openlocfilehash: 41184d69be8382429ae6b59e8606afb49c729c0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375392"
---
# <a name="network-adapter-wdf-class-extension-netadaptercx"></a>网络适配器 WDF 类扩展 (NetAdapterCx)

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="overview"></a>概述

从 Windows 10 版本 1703 开始，Windows 驱动程序工具包 (WDK) 包含一个网络适配器 WDF 类扩展模块 (NetAdapterCx)，用于为网络接口控制器 (NIC) 编写基于 KMDF 的客户端驱动程序。 NetAdapterCx 提供 WDF 的强大功能和灵活性以及 NDIS 的网络性能，可以轻松地为 NIC 编写驱动程序。

在旧版 Windows 中，WDF 和 NDIS 各有优点，但互操作性不好。 在过去，编写 NIC 驱动程序的唯一方法是编写 NDIS 微型端口驱动程序。 若要在 NDIS 微型端口驱动程序中使用 WDF，必须在驱动程序中编写额外代码。即使这样，也只能访问 WDF 功能的一小部分。

与之相反，在使用 NetAdapterCx 模型时，则是在为 NIC 编写真实的 WDF 驱动程序。 这意味着 NetAdapterCx 驱动程序可以访问完整的 WDF 功能、特定于网络的 API，以及 NetAdapter 类扩展提供的 I/O 支持。 如下面的方块图所示，使用 NDIS 时，NetAdapterCx 仍在后台运行，但会代表你处理与 NDIS 的所有交互。

<img src="images/architecture.png" alt="NetAdapterCx architecture" title="NetAdapterCx 体系结构" width="600"/>

## <a name="additional-info"></a>其他信息

若要观看讨论 NetAdapterCx 使用优点的视频，请观看第 9 频道的[网络适配器类扩展：概述](https://aka.ms/netadapter/video1)视频。

若要了解如何将 NDIS 6.x 微型端口驱动程序移植到 NetAdapterCx NIC 驱动程序模型，请参阅[将 NDIS 微型端口驱动程序移植到 NetAdapterCx](porting-ndis-miniport-drivers-to-netadaptercx.md)。

若要立刻开始使用 GitHub 上的驱动程序示例，请克隆 [NetAdapter-Cx-Driver-Samples](https://github.com/Microsoft/NetAdapter-Cx-Driver-Samples) 存储库。

若要查看 NetAdapterCx 本身的源代码，或者执行分步调试，请参阅 GitHub 上的 [Network-Adapter-Class-Extension](https://github.com/Microsoft/Network-Adapter-Class-Extension) 存储库。

如果在开发 NetAdapterCx 客户端驱动程序时需要 Microsoft 的帮助，或者需要提供类扩展的反馈，请给我们发送[电子邮件](mailto:netadapter@microsoft.com)。

若要观看讨论未来的路线图和协作机会的视频，请观看第 9 频道的[网络适配器类扩展：路线图和协作](https://aka.ms/netadapter/video4)视频。

## <a name="topics"></a>主题

本部分包含以下主题：

* [将 NDIS 微型端口驱动程序移植到 NetAdapterCx](porting-ndis-miniport-drivers-to-netadaptercx.md)
* [生成 NetAdapterCx 客户端驱动程序](building-a-netadaptercx-client-driver.md)
* [NetAdapterCx 客户端驱动程序的 INF 文件](inf-files-for-netadaptercx-client-drivers.md)
* [管理 NetAdapterCx 中对象的生存期](managing-the-lifetime-of-objects-in-netadaptercx.md)
* [访问配置信息](accessing-configuration-information.md)
* [处理控制请求](handling-control-requests.md)
* [调试 NetAdapterCx 客户端驱动程序](debugging-a-netadaptercx-client-driver.md)
* [传输网络数据](transferring-network-data.md)
* [NetAdapterCx 接收方缩放 (RSS)](netadaptercx-receive-side-scaling-rss-.md)
* [配置电源管理](configuring-power-management.md)
* [NDIS-WDF 函数等效项](ndis-wdf-function-equivalents.md)
* [NetAdapterCx 限制](netadaptercx-limitations.md)
* [移动宽带 (MBB) WDF 类扩展 (MBBCx)](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)
