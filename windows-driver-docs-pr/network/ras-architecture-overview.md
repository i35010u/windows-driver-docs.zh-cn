---
title: RAS 体系结构概述
description: RAS 体系结构概述
keywords:
- 远程访问服务 WDK 网络
- RAS WDK 网络
- 体系结构 WDK WAN，RAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a62e67e61a2fe25aeb1f56c0da907d7fe72fec68
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839453"
---
# <a name="ras-architecture-overview"></a>RAS 体系结构概述





远程访问服务 (RAS) 使远程工作站能够建立到 LAN 的拨号连接，并访问 LAN 上的资源，就像远程工作站位于 LAN 上一样。 WAN 微型端口驱动程序提供 RAS 和广域网络之间的接口 (WAN) 卡，如 ISDN、56和交换适配器。

RAS 体系结构的主要系统提供的组件包括以下各项：

-   [NDISWAN](#ddk-ndiswan-ng)

-   [TAPI 服务](#ddk-tapi-service-ng)

-   [NDPROXY](#ddk-ndproxy-ng)

-   [NDISTAPI](#ddk-ndistapi-ng)

开发人员提供了 TAPI 感知的应用程序和 WAN 微型端口驱动程序。 CoNDIS WAN 开发人员还可以提供 WAN 客户端协议驱动程序、微型端口呼叫管理器 (MCM) 或单独的呼叫管理器。

下图显示了 RAS 体系结构。

![说明 ras 体系结构的示意图](images/condsras.png)

以下部分简要介绍了 RAS 体系结构中的组件。

### <a name="ras-and-tapi-components"></a>RAS 和 TAPI 组件

上图右侧的组件可实现与 TAPI 相关的呼叫管理操作，例如设置和撕裂调用和连接。 这些操作的详细信息取决于 WAN 型号 (NDIS WAN 或 CoNDIS WAN) 。

### <a name="ras-functions"></a><a href="" id="ddk-ras-functions-ng"></a>RAS 函数

用户模式应用程序调用 RAS 功能，使 RAS 与远程计算机建立连接。 建立 RAS 连接后，此类应用程序可以通过使用标准网络接口（例如 Microsoft Windows 套接字、NetBIOS、命名管道或 RPC）连接到网络服务。

### <a name="tapi-aware-applications"></a><a href="" id="ddk-tapi-aware-applications-ng"></a>支持 TAPI 的应用程序

可以在应用程序和服务进程中运行的支持 TAPI 的应用程序，这些应用程序都可以进行电话通信。 服务提供商与特定设备通信。 通过 tapi 界面 ( # A0) 与服务提供商进行通信的 TAPI 感知应用程序。 这些服务提供程序在 [TAPI 服务](#ddk-tapi-service-ng) 进程中运行。

### <a name="tapi-service"></a><a href="" id="ddk-tapi-service-ng"></a>TAPI 服务

TAPI 服务 ( # A0) 进程显示了电话服务提供程序 [接口， (](#ddk-tapi-aware-applications-ng)提供程序的服务提供程序的 TSPI) 。 这些服务提供程序是在 TAPI 服务进程的上下文中运行的 Dll。

操作系统提供了服务提供程序，NDIS WAN 或 CoNDIS WAN 微型端口驱动程序使用该服务提供程序与用户模式应用程序进行通信。 用于 NDIS WAN 微型端口驱动程序的服务提供程序为 [KMDDSP](#ddk-kmddsp-ng)。 用于 CoNDIS WAN 微型端口驱动程序的服务提供程序 (和 MCMs) 为 [NDPTSP](#ddk-ndptsp-ng)。

### <a name="kmddsp"></a><a href="" id="ddk-kmddsp-ng"></a>KMDDSP

KMDDSP (Kmddsp) 是在 TAPI 服务进程的上下文中运行的服务提供程序 DLL。 KMDDSP 提供了一个 TSPI 接口，该接口可让 TAPI 服务向 [tapi 感知应用程序](#ddk-tapi-aware-applications-ng) 提供，以便 [NDISTAPI](#ddk-ndistapi-ng) 能够与用户模式应用程序进行通信。

KMDDSP 使用 NDISTAPI 将用户模式请求转换为相应的 TAPI Oid (OID \_ tapi \_ *Xxx*) 。 有关 TAPI Oid 的详细信息，请参阅 [Tapi 对象](/previous-versions/windows/hardware/network/ff564235(v=vs.85))。

### <a name="ndptsp"></a><a href="" id="ddk-ndptsp-ng"></a>NDPTSP

NDPTSP (Ndptsp) 是在 TAPI 服务进程的上下文中运行的服务提供程序 DLL。 NDPTSP 提供了一个 TSPI 接口，该接口可让 TAPI 服务向 TAPI 感知应用程序提供，以便 [NDPROXY](#ddk-ndproxy-ng) 能够与用户模式应用程序进行通信。

NDPTSP 使用 NDPROXY 将用户模式请求转换为面向 TAPI 连接的 Oid (OID \_ CO \_ TAPI \_ *Xxx*) 。 有关 TAPI 面向连接的 Oid 的详细信息，请参阅 [Connection-Oriented NDIS 的 Tapi 扩展](./tapi-extension-oids-for-connection-oriented-ndis.md)。

### <a name="ndistapi"></a><a href="" id="ddk-ndistapi-ng"></a>NDISTAPI

NDISTAPI ( # A0) 接收来自 [KMDDSP](#ddk-kmddsp-ng) 的 TAPI 请求，然后调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 将相应的 TAPI OID 路由到 NDIS WAN 微型端口驱动程序。 有关 NDISTAPI 的详细信息，请参阅 [NDISTAPI 概述](ndistapi-overview.md)。

### <a name="ndproxy"></a><a href="" id="ddk-ndproxy-ng"></a>NDPROXY

NDPROXY ( # A0) 通过 [NDPTSP](#ddk-ndptsp-ng) 提供的 TSPI 接口与 TAPI 通信。 NDPROXY 通过 NDISWAN 和 CoNDIS WAN 微型端口驱动程序、MCMs 和呼叫管理器进行 NDIS 通信。

有关 NDPROXY 的详细信息，请参阅 [NDPROXY 概述](ndproxy-overview.md)。

### <a name="driver-stack"></a>驱动程序堆栈

### <a name="wan-transports"></a><a href="" id="ddk-wan-transports-ng"></a>WAN 传输

RAS 系统组件提供诸如 PPP Authentication (PAP、CHAP) 和网络配置协议驱动程序的传输， (IPCP、IPXCP、NBFCP、LCP 等) 。 WAN 微型端口驱动程序 (或 MCM) 仅实现特定于 PPP 媒体的帧。

### <a name="ndiswan"></a><a href="" id="ddk-ndiswan-ng"></a>NDISWAN

NDISWAN ( # A0) 是一个 NDIS 中间驱动程序。 NDISWAN 在其上部边缘和 [WAN 微型端口驱动程序](wan-miniport-drivers.md) 上绑定到 NDIS 协议驱动程序。

NDISWAN 提供 PPP 协议/链接帧、压缩/解压缩和加密/解密。 具有 NDIS WAN 和 CoNDIS WAN 微型端口驱动程序的 NDISWAN 接口。

有关 NDISWAN 的详细信息，请参阅 [NDISWAN 概述](ndiswan-overview.md)。

### <a name="serial-driver"></a><a href="" id="ddk-serial-driver-ng"></a>串行驱动程序

串行驱动程序组件是用于内部串行端口或多端口串行卡的标准设备驱动程序。 Microsoft Windows 2000 和更高版本附带的异步 WAN 微型端口驱动程序使用内部串行驱动程序进行调制解调器通信。 任何与串行驱动程序导出相同功能的驱动程序都可以与内置的异步 WAN 微型端口驱动程序交互。

**注意**  与25个供应商可以为一个 X-blade 接口卡实现串行驱动程序仿真程序。 在这种情况下，每个虚拟电路都显示为一个串行端口，其中包含一个带有 (PAD) 的 X 25 包组装器/拆装器。 连接接口必须正确地模拟串行信号，如 DTR、DCD、CTS、RTS 和 DSR。
为其 X-blade 卡实现串行驱动程序模拟器的 x 25 供应商还必须在 Pad .inf 文件中为其填充提供一个条目。 此文件包含通过连接到连接到连接的连接所需的命令/响应脚本。 有关 Pad .inf 文件的详细信息，请参阅 Microsoft Windows SDK 文档。

 

### <a name="wan-miniport-driver"></a>WAN 微型端口驱动程序

WAN 微型端口驱动程序提供 [NDISWAN](#ddk-ndiswan-ng) 和 WAN nic 之间的接口。

WAN 微型端口驱动程序可作为 NDIS WAN 微型端口驱动程序或 CoNDIS WAN 微型端口驱动程序实现。 有关选择最适合于你的应用程序的微型端口驱动程序模型的详细信息，请参阅 [选择 WAN 驱动程序模型](choosing-a-wan-driver-model.md)。

 

