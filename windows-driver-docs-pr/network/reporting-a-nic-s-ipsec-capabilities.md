---
title: 报告 NIC 的 IPsec 功能
description: 报告 NIC 的 IPsec 功能
ms.assetid: 6ed02d4a-9b5e-4245-a3f9-f0b5fc8366a7
keywords:
- 任务卸载 WDK TCP/IP 传输，IPsec 任务
- IPsec 卸载 WDK TCP/IP 传输，功能
- IPsec 卸载 WDK TCP/IP 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156a121ab89f450c6ecf169cd618ab63f761e232
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842059"
---
# <a name="reporting-a-nics-ipsec-capabilities"></a>报告 NIC 的 IPsec 功能

\[IPsec 任务卸载功能已弃用，不应使用。\]




NDIS 微型端口驱动程序在 NDIS\_IPSEC 中指定 NIC 的当前 Internet 协议安全性（IPsec）卸载配置[ **\_卸载\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)结构。微型端口驱动程序必须在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)中包含当前 IPsec 卸载配置，\_卸载\_属性结构。 微型端口驱动程序从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将 NDIS\_微型端口\_适配器中的信息传入\_卸载\_特性。

微型端口驱动程序必须在[**NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示中报告 IPsec 卸载功能的更改（如果有）。

为了响应[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，ndis 在 NDIS [ **\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构中包含 NDIS\_IPSEC\_卸载，该结构在[ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员。\_ NDIS 使用微型端口驱动程序提供的信息。

微型端口驱动程序在 NDIS\_IPSEC\_卸载\_V1 结构中指出以下信息：

-   封装设置，位于**封装**成员中。 有关此成员的详细信息，请参阅 NDIS\_IPSEC 中的 "备注" 部分[ **\_卸载\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)。

-   NIC 是否可以在数据包上执行合并 IPsec 操作，即 NIC 是否可以使用以下格式处理包含身份验证标头（AH）和数据包中的封装安全负载（ESP）的数据包：

    \[IP\]\[AH\]\[\]\[的其余部分\]

-   NIC 是否可以在发送和接收数据包的传输模式部分和隧道模式部分执行 IP 安全处理。 数据包的传输模式部分适用于端到端安全关联，而数据包的隧道模式部分则属于隧道安全关联。

-   如果数据包的 IP 标头包含 IP 选项，NIC 是否可以在数据包上执行 IP 安全操作。

微型端口驱动程序指定 NIC 的以下功能，以便计算或验证（或计算和验证） AH 负载和身份验证信息的加密校验和：

-   NIC 可以使用的完整性算法（MD5 或 SHA 1）

-   NIC 是否可以处理 AH 安全负载：
    -   数据包的传输模式部分
    -   数据包的隧道模式部分
    -   发送数据包
    -   接收数据包

微型端口驱动程序指定 NIC 的以下功能来处理 ESP 负载：

-   NIC 可以使用的机密性算法（DES、三重 DES 或两者）

-   NIC 是否支持 null 加密（即 ESP 负载，无需加密但具有身份验证哈希）

-   NIC 是否可以对执行 ESP 处理：
    -   数据包的传输模式部分
    -   数据包的隧道模式部分
    -   发送数据包
    -   接收数据包

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






