---
title: TCP/IP 任务卸载
description: TCP/IP 任务卸载
ms.assetid: e73cc4e8-574b-438b-acd2-f0aaf5c20589
keywords:
- TCP/IP 卸载 WDK 网络任务卸载
- 卸载 WDK TCP/IP 传输，任务卸载
- 任务卸载，WDK TCP/IP 传输
- 任务卸载 WDK TCP/IP 传输，有关任务卸载
- 卸载功能 WDK TCP/IP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb2d2343f1cedb336344ac53cc2f749f562605e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569470"
---
# <a name="tcpip-task-offload"></a>TCP/IP 任务卸载





若要提高其性能，Microsoft TCP/IP 传输可以将任务卸载到具有适当任务卸载能力的网络接口卡 (NIC)。

从开始 Windows Vista，Windows 操作系统支持以下任务卸载服务：

### <a name="checksum-tasks"></a>校验和任务

计算和的 IP 和 TCP 校验和验证，则可以将卸载 TCP/IP 传输。

### <a name="internet-protocol-security-ipsec-offload-version-1-ipsecov1"></a>Internet 协议安全性 (IPsec) 将卸载版本 1 (IPsecOV1)

\[IPsec 任务卸载功能已弃用，不应使用。\]

计算和验证的身份验证标头 (AH) 的加密校验和封装安全有效负载 (ESP)，或两者，则可以将卸载 TCP/IP 传输。 加密和解密的 ESP 有效负载和加密和解密的用户数据报协议 (UDP)，也可以卸载 TCP/IP 传输-封装 ESP 数据包。

有关 IPsecOV1 详细信息，请参阅[IPsec 卸载版本 1](ipsec-offload-version-1.md)。

### <a name="internet-protocol-security-ipsec-offload-version-2-ipsecov2"></a>Internet 协议安全性 (IPsec) 将卸载版本 2 (IPsecOV2)

\[IPsec 任务卸载功能已弃用，不应使用。\]

计算和验证的身份验证标头 (AH) 的加密校验和封装安全有效负载 (ESP)，或两者，则可以将卸载 TCP/IP 传输。 加密和解密的 ESP 有效负载和加密和解密的用户数据报协议 (UDP)，也可以卸载 TCP/IP 传输-封装 ESP 数据包。 IPsecOV2 NDIS 6.1 和更高版本中支持。

有关 IPsecOV2 详细信息，请参阅[IPsec 卸载版本 2](ipsec-offload-version-2.md)。

### <a name="large-send-offload-version-1-lsov1"></a>大量发送卸载版本 1 (LSOV1)

TCP/IP 传输支持大量发送卸载版本 1 (LSOV1)。 TCP/IP 传输可以将大型 （最多 64 KB，包括 IP 标头） 的分段卸载 LSOV1，使用 IPv4 的 TCP 数据包。

### <a name="large-send-offload-version-2-lsov2"></a>大量发送卸载版本 2 (LSOV2)

大量发送卸载版本 2 (LSOV2) 接口是 LSOV1 的增强的版本。 LSOV2 支持大于 64 K 的大型 TCP 数据包的 IPv6、 IPv4 和分段。 有关卸载的大型数据包分段的详细信息，请参阅[卸载分段的大型 TCP 数据包](offloading-the-segmentation-of-large-tcp-packets.md)。

Windows 操作系统从 Windows 8 和 Windows Server 2012 开始，支持以下额外任务重载服务：

### <a name="receive-segment-coalescing-rsc"></a>Receive Segment Coalescing (RSC)

接收段合并 (RSC) 启用网络卡微型端口驱动程序可合并多个 TCP 段，并指示它们作为单个合并单元 (SCU) 到操作系统的网络子系统。

### <a name="network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>使用通用路由封装 (NVGRE) 任务卸载实现网络虚拟化

[网络虚拟化使用通用路由封装 (NVGRE) 任务卸载](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)就可以使用通用路由封装 GRE 封装的数据包，其中：

-   大量发送卸载 (LSO)
-   Receive Side Scaling (RSS)
-   虚拟机队列 (VMQ)

本部分包括：

-   [确定任务卸载功能](determining-task-offload-capabilities.md)
-   [启用和禁用任务卸载服务](enabling-and-disabling-task-offload-services.md)
-   [确定当前的任务卸载设置](determining-the-current-task-offload-settings.md)
-   [组合任务的类型将卸载](combining-types-of-task-offloads.md)
-   [使用注册表值来启用和禁用任务卸载](using-registry-values-to-enable-and-disable-task-offloading.md)
-   [将校验和任务](offloading-checksum-tasks.md)
-   [IPsec 任务卸载](offloading-ipsec-tasks.md)
    - \[IPsec 任务卸载功能已弃用，不应使用。\]
-   [卸载大型 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)

 

 





