---
title: RAS 体系结构概述
description: RAS 体系结构概述
ms.assetid: 1ff285d7-2aed-46e1-979e-3b77614dcbf5
keywords:
- 远程访问服务 WDK 网络
- RAS WDK 网络
- 体系结构 WDK WAN RAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9901d484f64a3a1eb56dff45c2758f3b49500400
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343225"
---
# <a name="ras-architecture-overview"></a>RAS 体系结构概述





远程访问服务 (RAS) 使远程工作站，像远程工作站在 LAN 上建立拨号连接到 LAN 唤醒 LAN 并访问资源。 WAN 微型端口驱动程序提供 RAS 和 ISDN、 x.25 线路和切换 56 适配器如广域网 (WAN) 的网络卡之间的接口。

RAS 体系结构的系统提供的主要组件包括：

-   [NDISWAN](#ddk-ndiswan-ng)

-   [TAPI 服务](#ddk-tapi-service-ng)

-   [NDPROXY](#ddk-ndproxy-ng)

-   [NDISTAPI](#ddk-ndistapi-ng)

开发人员提供的 TAPI 感知应用程序和 WAN 微型端口驱动程序。 WAN 的 CoNDIS 开发人员还可以提供 WAN 的客户端协议驱动程序、 微型端口呼叫管理器 (MCM) 或单独调用管理器。

下图显示了 RAS 体系结构。

![说明 ras 体系结构的关系图](images/condsras.png)

以下各节简要介绍 RAS 体系结构中的组件。

### <a name="ras-and-tapi-components"></a>RAS 和 TAPI 组件

在前面的右侧的组件图实现 TAPI 相关调用管理操作，如设置和拆除调用和连接。 这些操作的详细信息依赖于 WAN 的模型 （NDIS WAN 或 CoNDIS WAN）。

### <a href="" id="ddk-ras-functions-ng"></a>RAS 函数

用户模式应用程序调用 RAS 函数来建立与远程计算机的 RAS 连接。 RAS 连接建立后，此类应用程序可以通过使用标准网络接口，如 Microsoft Windows 套接字、 NetBIOS、 命名管道或 RPC 连接到网络服务。

### <a href="" id="ddk-tapi-aware-applications-ng"></a>TAPI 感知应用程序

TAPI 感知应用程序，即支持电话服务通信的应用程序和服务进程中运行。 服务提供程序与特定设备通信。 TAPI 感知应用程序通过其服务提供商的 TAPI 接口 (Tapi32.dll) 进行通信。 在中运行这些服务提供商[TAPI 服务](#ddk-tapi-service-ng)过程。

### <a href="" id="ddk-tapi-service-ng"></a>TAPI 服务

TAPI 服务 (Tapisrv.exe) 程序会显示电话服务提供程序接口 (TSPI) 到服务提供商[TAPI 感知应用程序](#ddk-tapi-aware-applications-ng)。 这些服务提供程序是 TAPI 服务过程的上下文中运行的 Dll。

操作系统提供 NDIS WAN 或 WAN 的 CoNDIS 微型端口驱动程序使用与用户模式应用程序进行通信的服务提供程序。 NDIS WAN 微型端口驱动程序的服务提供程序是[KMDDSP](#ddk-kmddsp-ng)。 WAN 的 CoNDIS 微型端口驱动程序 （和 MCMs） 的服务提供程序是[NDPTSP](#ddk-ndptsp-ng)。

### <a href="" id="ddk-kmddsp-ng"></a>KMDDSP

KMDDSP (Kmddsp.tsp) 是服务提供程序的 TAPI 服务进程的上下文中运行的 DLL。 KMDDSP 提供程序的 TAPI 服务提供给 TSPI 界面[TAPI 感知应用程序](#ddk-tapi-aware-applications-ng)以便[NDISTAPI](#ddk-ndistapi-ng)可以与用户模式应用程序进行通信。

KMDDSP 配合 NDISTAPI 若要将用户模式下请求转换为相应的 TAPI Oid (OID\_TAPI\_*Xxx*)。 有关 TAPI Oid 的详细信息，请参阅[TAPI 对象](https://msdn.microsoft.com/library/windows/hardware/ff564235)。

### <a href="" id="ddk-ndptsp-ng"></a>NDPTSP

NDPTSP (Ndptsp.tsp) 是服务提供程序的 TAPI 服务进程的上下文中运行的 DLL。 NDPTSP 提供了向 TAPI 感知应用程序的 TAPI 服务提供一个 TSPI 界面，以便[NDPROXY](#ddk-ndproxy-ng)可以与用户模式应用程序进行通信。

NDPTSP 配合 NDPROXY 若要将用户模式下请求转换为 TAPI 面向连接的 Oid (OID\_CO\_TAPI\_*Xxx*)。 详细了解 TAPI 面向连接的 Oid，请参阅[Connection-Oriented ndis TAPI 扩展](https://msdn.microsoft.com/library/windows/hardware/ff570924)。

### <a href="" id="ddk-ndistapi-ng"></a>NDISTAPI

NDISTAPI (Ndistapi.sys) 接收来自的 TAPI 请求[KMDDSP](#ddk-kmddsp-ng) ，然后调用[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)将相应的 TAPI Oid 路由到 NDIS WAN 微型端口驱动程序。 有关 NDISTAPI 详细信息，请参阅[NDISTAPI 概述](ndistapi-overview.md)。

### <a href="" id="ddk-ndproxy-ng"></a>NDPROXY

与通过 TSPI TAPI NDPROXY (Ndproxy.sys) 进行通信的接口[NDPTSP](#ddk-ndptsp-ng)提供。 NDPROXY 通过 NDIS NDISWAN 和 WAN 的 CoNDIS 微型端口驱动程序、 MCMs，与调用管理器进行通信。

有关 NDPROXY 详细信息，请参阅[NDPROXY 概述](ndproxy-overview.md)。

### <a name="driver-stack"></a>驱动程序堆栈

### <a href="" id="ddk-wan-transports-ng"></a>WAN 传输

RAS 系统组件提供的传输如 PPP 身份验证 （PAP、 CHAP） 和网络配置协议驱动程序 （IPCP、 IPXCP、 NBFCP、 LCP，等）。 WAN 微型端口驱动程序 （或 MCM） 实现仅 PPP 特定于媒体的帧。

### <a href="" id="ddk-ndiswan-ng"></a>NDISWAN

NDISWAN (Ndiswan.sys) 是 NDIS 中间驱动程序。 NDISWAN 将绑定到在其上边缘的 NDIS 协议驱动程序和[WAN 微型端口驱动程序](wan-miniport-drivers.md)在其下边缘。

NDISWAN 提供 PPP 帧协议/链接、 压缩/解压缩和加密/解密。 NDISWAN NDIS WAN 和 WAN 的 CoNDIS 微型端口驱动程序接口。

有关 NDISWAN 详细信息，请参阅[NDISWAN 概述](ndiswan-overview.md)。

### <a href="" id="ddk-serial-driver-ng"></a>串行驱动程序

串行驱动程序组件是内部的串行端口或多端口的串行卡的标准设备驱动程序。 Microsoft Windows 2000 和更高版本附带的异步 WAN 微型端口驱动程序使用的调制解调器通信的内部串行驱动程序。 将相同的功能以串行驱动程序导出任何驱动程序可以使用内置异步 WAN 微型端口驱动程序的接口。

**请注意**  X.25 供应商可以实现串行驱动程序的 X.25 接口卡的仿真程序。 在这种情况下，每个虚拟线路 X.25 卡上的显示为具有 X.25 数据包组装器/拆装器 （填充） 附加到它的串行端口。 连接接口必须正确模拟串行信号如 DTR、 DCD、 CTS 中，RTS 和 DSR。
X.25 供应商实现其 X.25 卡串行驱动程序仿真程序还必须为其填充 Pad.inf 文件中生成一个条目。 此文件包含使通过 X.25 板建立的连接所需的命令/响应脚本。 有关 Pad.inf 文件的详细信息，请参阅 Microsoft Windows SDK 文档。

 

### <a name="wan-miniport-driver"></a>WAN 微型端口驱动程序

WAN 微型端口驱动程序之间提供接口[NDISWAN](#ddk-ndiswan-ng)和 WAN Nic。

WAN 微型端口驱动程序可以作为 NDIS WAN 的微型端口驱动程序或 CoNDIS WAN 的微型端口驱动程序实现。 有关选择最适合你的应用程序的微型端口驱动程序模型的详细信息，请参阅[选择 WAN 的驱动程序模型](choosing-a-wan-driver-model.md)。

 

 





