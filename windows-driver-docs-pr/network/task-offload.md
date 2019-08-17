---
title: TCP/IP 任务卸载概述
description: TCP/IP 任务卸载概述
ms.assetid: e73cc4e8-574b-438b-acd2-f0aaf5c20589
keywords:
- TCP/IP 卸载 WDK 网络, 任务卸载
- 卸载 WDK TCP/IP 传输, 任务卸载
- 任务卸载 WDK TCP/IP 传输
- 任务卸载 WDK TCP/IP 传输, 关于任务卸载
- 功能 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2757c34d2b720fc5173d47229c9c1aff6b8c6083
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565695"
---
# <a name="tcpip-task-offload-overview"></a>TCP/IP 任务卸载概述





为了提高性能, Microsoft TCP/IP 传输可将任务卸载到具有适当任务卸载功能的网络接口卡 (NIC)。

从 Windows Vista 开始, Windows 操作系统支持以下任务卸载服务:

### <a name="checksum-tasks"></a>校验和任务

TCP/IP 传输可以卸载 IP 和 TCP 校验和的计算和验证。

### <a name="internet-protocol-security-ipsec-offload-version-1-ipsecov1"></a>Internet 协议安全 (IPsec) 卸载版本 1 (IPsecOV1)

\[IPsec 任务卸载功能已弃用, 不应使用。\]

TCP/IP 传输可以为身份验证标头 (AH)、封装安全有效负载 (ESP) 或两者, 卸载加密校验和的计算和验证。 TCP/IP 传输还可以卸载 ESP 有效负载的加密和解密以及用户数据报协议 (UDP) 封装的 ESP 数据包的加密和解密。

有关 IPsecOV1 的详细信息, 请参阅[IPsec 卸载版本 1](ipsec-offload-version-1.md)。

### <a name="internet-protocol-security-ipsec-offload-version-2-ipsecov2"></a>Internet 协议安全 (IPsec) 卸载版本 2 (IPsecOV2)

\[IPsec 任务卸载功能已弃用, 不应使用。\]

TCP/IP 传输可以为身份验证标头 (AH)、封装安全有效负载 (ESP) 或两者, 卸载加密校验和的计算和验证。 TCP/IP 传输还可以卸载 ESP 有效负载的加密和解密以及用户数据报协议 (UDP) 封装的 ESP 数据包的加密和解密。 在 NDIS 6.1 和更高版本中支持 IPsecOV2。

有关 IPsecOV2 的详细信息, 请参阅[IPsec 卸载版本 2](ipsec-offload-version-2.md)。

### <a name="large-send-offload-version-1-lsov1"></a>大规模发送卸载版本 1 (LSOV1)

TCP/IP 传输支持大型发送卸载版本 1 (LSOV1)。 通过 LSOV1, TCP/IP 传输可以卸载 IPv4 的大 (最多 64 KB, 包括 IP 标头) TCP 数据包的分段。

### <a name="large-send-offload-version-2-lsov2"></a>大型发送卸载版本 2 (LSOV2)

大型发送卸载版本 2 (LSOV2) 接口是 LSOV1 的增强版本。 对于大于64K 的大型 TCP 数据包, LSOV2 支持 IPv6、IPv4 和分段。 有关卸载大数据包的细分的详细信息, 请参阅[卸载大 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)。

从 Windows 8 和 Windows Server 2012 开始, Windows 操作系统支持以下附加任务重载服务:

### <a name="receive-segment-coalescing-rsc"></a>Receive Segment Coalescing (RSC)

接收段合并 (RSC) 使网卡驱动程序可以合并多个 TCP 段, 并将它们作为单个合并单元 (SCU) 指示到操作系统的网络子系统。

### <a name="network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>使用通用路由封装 (NVGRE) 任务卸载实现网络虚拟化

[使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)使你可以使用通用路由封装 (GRE) 封装的数据包:

-   大量发送卸载 (LSO)
-   Receive Side Scaling (RSS)
-   虚拟机队列 (VMQ)

本部分包括：

-   [确定任务卸载功能](determining-task-offload-capabilities.md)
-   [启用和禁用任务卸载服务](enabling-and-disabling-task-offload-services.md)
-   [确定当前任务卸载设置](determining-the-current-task-offload-settings.md)
-   [合并任务的类型卸载](combining-types-of-task-offloads.md)
-   [使用注册表值启用和禁用任务卸载](using-registry-values-to-enable-and-disable-task-offloading.md)
-   [卸载校验和任务](offloading-checksum-tasks.md)
-   [卸载 IPsec 任务](offloading-ipsec-tasks.md)
    - \[IPsec 任务卸载功能已弃用, 不应使用。\]
-   [卸载大 TCP 数据包的细分](offloading-the-segmentation-of-large-tcp-packets.md)

 

 





