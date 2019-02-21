---
title: 处理 UDP 封装 ESP 数据包
description: 处理 UDP 封装 ESP 数据包
ms.assetid: b5b10a2c-1080-4c21-a187-1c0aff30b229
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载、 处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5801bcc4d86b78b162b55e51740eba605c073bc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524015"
---
# <a name="processing-udp-encapsulated-esp-packets"></a>处理 UDP 封装 ESP 数据包

\[IPsec 任务卸载功能已弃用，不应使用。\]




当 NIC 接收端口 4500 上的 UDP 封装数据包时，它会检查数据包是 IKE （控制） 数据包或 ESP （数据） 数据包。 IKE 和 ESP 数据包的 UDP 封装类型的说明，请参阅[UDP ESP 封装类型](udp-esp-encapsulation-types.md)。

-   如果数据包的 IKE 数据包，NIC 将数据包传递到微型端口驱动程序而无需进一步与 IPsec 有关的处理。

-   如果数据包的 ESP 数据包，NIC 将检查是否数据包的入站的 SA （或在传输 over 隧道数据包的情况下 SAs） 当前卸载到 nic。
    -   如果入站的 SAs 当前不卸载到 NIC，NIC 将数据包传递到微型端口驱动程序而无需进一步与 IPsec 有关的处理。
    -   如果入站的 SAs 当前卸载到 NIC，NIC 将使用指定的分析器条目与 SAs 关联的封装类型分析数据包。 NIC 然后处理该数据包中的 ESP 负载中所述[接收路径中卸载 IPsec 任务](offloading-ipsec-tasks-in-the-receive-path.md)。

如果传入的 ESP 数据包是 UDP 封装传输 over 隧道数据包，如中所述[UDP ESP 封装类型](udp-esp-encapsulation-types.md)，NIC 首次解密时的隧道模式数据包，这不是部分 ESP 有效负载UDP 封装。 然后，NIC 将处理该数据包的 UDP 封装隧道模式部分。

 

 





