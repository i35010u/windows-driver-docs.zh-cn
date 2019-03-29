---
title: 使用 UDP 封装的 ESP 数据包遍历 NAT 和 NAPT
description: 使用 UDP 封装的 ESP 数据包遍历 NAT 和 NAPT
ms.assetid: 9bfd6a7c-2c24-419e-b82d-ef6ef8fe1fa5
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载、 transversing Nat 和 NAPTs
- 网络地址转换器 WDK IPsec 卸载
- 网络地址端口转换器 WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1948ea7e6e5b0f136d8726a2fad8794731e9c07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563029"
---
# <a name="traversing-nats-and-napts-with-udp-encapsulated-esp-packets"></a>使用 UDP 封装的 ESP 数据包遍历 NAT 和 NAPT

\[IPsec 任务卸载功能已弃用，不应使用。\]




网络地址转换器 (Nat) 和网络地址端口转换器 (NAPTs) 将转换多个专用网络地址转换一个路由的 IP 公共地址，反之亦然，从而允许多个系统共享单个 IP 地址。 在这种方式，Nat 和 NAPTs 有助于缓解的路由的 IPv4 地址不足。

但是，Nat 和 NAPTs 可能导致问题的 Internet 协议安全性 (IPsec)。 由于 Nat 和 NAPTs 修改数据包的 IP 标头，它们会导致受保护的 AH 数据包校验和验证失败。 NAPTs 修改 TCP 和 UDP 端口，不能修改的 ESP 保护的数据包加密的 TCP 标头中的端口。

UDP 封装可解决此问题。 在实践中，仅用于 ESP 数据包的 UDP 封装。 NAT 或 NAPT 可以修改的 UDP 封装 ESP 数据包而不需要重大 ESP 身份验证并正在知难而退由 ESP 加密的加密的 IP 和 UDP 标头。 ESP 数据包的 UDP 封装的详细说明，请参阅[UDP 封装的 NAT 理由通过 IPsec](https://go.microsoft.com/fwlink/p/?linkid=9856)。

Microsoft 支持上端口 4500 ESP 数据包的 UDP 封装。 IKE 对等机端口 500 上的启动协商后，检测支持 NAT 遍历和检测在路径上的 NAT 或 NAPT，它们可以"浮动"IKE 和 UDP ESP 通信传输到端口 4500 协商。 有关此协商的详细信息，请参阅[协商的 NAT 遍历在 IKE 中](https://go.microsoft.com/fwlink/p/?linkid=9857)。

浮点到端口 4500 为 NAT 遍历提供以下优势：

-   它会绕过"ipsec"Nat 或 NAPTs 中断端口 500 UDP ESP 封装。

-   它可以提高性能。 ESP 数据包的 UDP 封装端口 4500 比端口 500 上会更有效。 有关详细信息，请参阅[UDP ESP 封装类型](udp-esp-encapsulation-types.md)。

若要支持 UDP ESP 封装，微型端口驱动程序或 NIC （或两者） 必须：

-   能够处理在接收路径中，ESP 数据包中所述[接收路径中卸载 IPsec 任务](offloading-ipsec-tasks-in-the-receive-path.md)。

-   维护分析器条目的列表。 分析器条目包含 NIC 分析一个或多个安全关联 (Sa) 上的传入 UDP ESP 数据包所需的信息。 有关分析程序的条目的详细信息，请参阅[UDP ESP SAs 和分析器条目](udp-esp-sas-and-parser-entries.md)。

-   维护一份 SAs，以便传输已卸载到 nic。

-   支持以下 Oid:
    -   [OID\_TCP\_TASK\_IPSEC\_ADD\_UDPESP\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569809)
    -   [OID\_TCP\_TASK\_IPSEC\_DELETE\_UDPESP\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569811)

 

 





