---
title: 使用 UDP 封装的 ESP 数据包遍历 NAT 和 NAPT
description: 使用 UDP 封装的 ESP 数据包遍历 NAT 和 NAPT
ms.assetid: 9bfd6a7c-2c24-419e-b82d-ef6ef8fe1fa5
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载，transversing Nat 和 NAPTs
- 网络地址转换器 WDK IPsec 卸载
- 网络地址端口转换器 WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c693348f9c27edb7ecf801998178a10fc6140759
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215789"
---
# <a name="traversing-nats-and-napts-with-udp-encapsulated-esp-packets"></a>使用 UDP 封装的 ESP 数据包遍历 NAT 和 NAPT

\[IPsec 任务卸载功能已弃用，不应使用。\]




网络地址转换器 (Nat) 和网络地址端口转换器 (NAPTs) 将多个专用网络地址转换为一个路由 IP 公用地址，反之亦然，从而允许多个系统共享单个 IP 地址。 通过这种方式，Nat 和 NAPTs 有助于缓解路由 IPv4 地址的不足。

但是，Nat 和 NAPTs 可能 (IPsec) 导致 Internet 协议安全问题。 由于 Nat 和 NAPTs 修改了数据包的 IP 标头，因此它们会导致受 AH 保护的数据包的校验和验证失败。 用于修改 TCP 和 UDP 端口的 NAPTs 无法修改受 ESP 保护的数据包的加密 TCP 标头中的端口。

UDP 封装解决了此问题。 实际上，UDP 封装仅用于 ESP 数据包。 NAT 或 NAPT 可以修改 UDP 封装的 ESP 包的未加密的 IP 和 UDP 标头，而不会中断 ESP 身份验证，也不会通过 ESP 加密来 stymied。 有关 ESP 数据包的 UDP 封装的详细说明，请参阅 [Udp 封装的 IPsec OVER NAT 理由](https://go.microsoft.com/fwlink/p/?linkid=9856)。

Microsoft 支持端口4500上的 ESP 数据包的 UDP 封装。 IKE 对等节点在端口500上启动协商后，检测对 NAT 遍历的支持，并按路径检测 NAT 或 NAPT，它们可以协商到端口4500的 "float" IKE 和 UDP-ESP 流量。 有关此协商的详细信息，请参阅 [IKE 中的 NAT 遍历协商](https://go.microsoft.com/fwlink/p/?linkid=9857)。

为 NAT 遍历浮动到端口4500具有以下优势：

-   它会绕过在端口500上打破 UDP ESP 封装的 "IPsec 感知" Nat 或 NAPTs。

-   它提高了性能。 与端口500相比，ESP 数据包的 UDP 封装在端口4500上更有效。 有关详细信息，请参阅 [UDP-ESP 封装类型](udp-esp-encapsulation-types.md)。

若要支持 UDP ESP 封装，可以使用微型端口驱动程序或 NIC (或二者) ：

-   如在接收路径中 [卸载 IPsec 任务](offloading-ipsec-tasks-in-the-receive-path.md)中所述，可以在接收路径中处理 ESP 数据包。

-   维护分析器条目的列表。 分析器条目包含 NIC 需要解析 (SAs) 上的一个或多个安全关联上的传入 UDP ESP 数据包的信息。 有关分析器条目的详细信息，请参阅 [UDP-ESP SAs 和分析器条目](udp-esp-sas-and-parser-entries.md)。

-   维护传输已卸载到 NIC 的 SAs 列表。

-   支持以下 Oid：
    -   [OID \_ TCP \_ 任务 \_ IPSEC \_ ADD \_ UDPESP \_ SA](./oid-tcp-task-ipsec-add-udpesp-sa.md)
    -   [OID \_ TCP \_ 任务 \_ IPSEC \_ DELETE \_ UDPESP \_ SA](./oid-tcp-task-ipsec-delete-udpesp-sa.md)

 

