---
title: 使用 IPsec 卸载版本 2 接收网络数据
description: 使用 IPsec 卸载版本 2 接收网络数据
ms.assetid: c09ce374-6dd6-4d16-914b-5576304d4440
keywords:
- IPsecOV2 WDK TCP/IP 传输，接收数据
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 253236da99a26f8a5fda4a2b8323df7975bac817
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216948"
---
# <a name="receiving-network-data-with-ipsec-offload-version-2"></a>使用 IPsec 卸载版本 2 接收网络数据

\[IPsec 任务卸载功能已弃用，不应使用。\]




NIC 执行 IPsec 卸载版本 2 (IPsecOV2) 在从传输中卸载的安全关联 (SA) 指定的接收数据包上进行处理。

微型端口驱动程序在将接收的数据 IPsecOV2 到过量驱动程序之前，设置带外 (OOB) 信息。 有关访问 OOB 信息的详细信息，请参阅 [ \_ \_ IPsec 卸载版本2中的访问网络缓冲区列表信息](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)。

**注意**   小型端口驱动程序应指示所有接收到过量驱动程序的数据包，即使在处理 NIC 中的 IPsec 数据时发生错误。 驱动程序必须指示有错误的数据包，使驱动程序堆栈能够监视网络流量并对其进行故障排除。

 

在小型端口驱动程序指示在驱动程序堆栈上收到的数据数据包之前，微型端口驱动程序：

-   验证是否已将硬件配置为处理 IPsec 卸载任务。 如果不是，微型端口驱动程序将执行接收指示，无其他 IPsec 卸载处理。

-   查看安全参数索引 (SPI) 以确定是否存在匹配的卸载 SA。 微型端口驱动程序确认数据包上的目标地址与在卸载 SA 中指定的地址相同。 如果没有任何匹配的 SA，则 NIC 会指示接收的数据，而不会设置 IPsecOV2 OOB 信息。

-   验证它是否可以根据微型端口驱动程序报告给传输的功能处理数据包，或在不进行 IPsec 处理的情况下做出接收指示。 例如，数据包可能具有 IP 选项，其中 NIC 不支持此类数据包的 IPsec 卸载处理，而微型端口驱动程序则执行 IPsec 处理。

-   在[**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)结构中设置**CryptoDone**标志，以指示 NIC 对接收的数据包中的至少一个 IPSEC 负载执行 ipsec 检查。

-   在 NDIS **NextCryptoDone** \_ IPSEC \_ 卸载 \_ V2 \_ 网络缓冲区列表信息结构中设置 NextCryptoDone 标志， \_ \_ \_ 以指示 NIC 对接收数据包的隧道和传输部分执行 IPSEC 检查。 只有当数据包同时具有隧道和传输负载时，微型端口驱动程序才会设置此标志;否则，此标志应为零。

-   设置 NDIS **CryptoStatus** \_ IPSEC \_ 卸载 \_ V2 \_ 网络缓冲区列表信息结构的正确 CryptoStatus 值 \_ \_ \_ ，以指示 IPSEC 检查的结果。

如果 NIC 未对传入数据包执行卸载处理，则微型端口驱动程序会清除 **CryptoDone** 和 **NextCryptoDone** 标志。 小型端口驱动程序会清除 NIC 不会解密的所有接收数据包的这些标志，而不管数据包是受 AH 保护还是受 ESP 保护。

微型端口驱动程序可以在 "接收[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)" 的 " [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)结构" 中设置**SaDeleteReq**。 接下来，TCP/IP 传输会发出 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ delete \_ sa](./oid-tcp-task-ipsec-offload-v2-delete-sa.md) ，以便删除接收数据包的入站 sa，并再次删除与已删除的入站 sa 相对应的出站 sa。 有关添加和删除 SAs 的详细信息，请参阅 [在 IPsec 卸载版本2中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

在微型端口驱动程序指示 \_ tcp/ip 传输的网络缓冲区 \_ 列表结构后，tcp/ip 传输会检查 NIC 在数据包上执行的 IPsec 检查的结果，检查数据包的序列号，并确定如何处理无法通过校验和或顺序测试的数据包。

 

