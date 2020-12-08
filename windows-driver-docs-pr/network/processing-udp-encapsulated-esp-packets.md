---
title: 处理 UDP 封装的 ESP 数据包
description: 处理 UDP 封装的 ESP 数据包
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载，处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b52c1c7b27ebdcda6a7f16891c00f31866d93cd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822823"
---
# <a name="processing-udp-encapsulated-esp-packets"></a>处理 UDP 封装的 ESP 数据包

\[IPsec 任务卸载功能已弃用，不应使用。\]




当 NIC 在端口4500上收到 UDP 封装的数据包时，它会检查数据包是否为 IKE (控件) 数据包或 ESP (数据) 数据包。 有关 IKE 和 ESP 数据包的 UDP 封装类型的说明，请参阅 [udp-Esp 封装类型](udp-esp-encapsulation-types.md)。

-   如果数据包是 IKE 数据包，则 NIC 会将数据包传递到微型端口驱动程序，而无需进一步进行 IPsec 相关处理。

-   如果数据包是 ESP 数据包，则 NIC 会检查数据包的入站 SA (还是 SAs，以防隧道传输数据包) 当前是否已卸载到 NIC。
    -   如果当前未将入站 SAs 卸载到 NIC，则 NIC 会将数据包传递到微型端口驱动程序，而无需进一步进行 IPsec 相关处理。
    -   如果入站 SAs 当前已卸载到 NIC，则 NIC 将使用与 SAs 关联的分析器条目指定的封装类型来分析数据包。 然后，NIC 处理包中的 ESP 负载，如在 [接收路径中卸载 IPsec 任务](offloading-ipsec-tasks-in-the-receive-path.md)中所述。

如果传入的 ESP 数据包是 UDP 封装的传输 over 隧道数据包，如 [udp-ESP 封装类型](udp-esp-encapsulation-types.md)中所述，NIC 首先会解密数据包的隧道模式部分（不是 UDP 封装的）的 ESP 有效负载。 然后，NIC 处理数据包的 UDP 封装隧道模式部分。

 

 





