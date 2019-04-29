---
title: UDP-ESP SA 和分析器项
description: UDP-ESP SA 和分析器项
ms.assetid: 1682b077-07ba-4b2e-9c01-fd7662f3f189
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载、 分析器条目
- 分析器条目 WDK IPsec 卸载
- 卸载的 UDP 封装的 ESP 数据包 WDK IPsec 安全关联
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a5d655628e902bccdd434081706651c56f5cc88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358255"
---
# <a name="udp-esp-sas-and-parser-entries"></a>UDP-ESP SA 和分析器项

\[IPsec 任务卸载功能已弃用，不应使用。\]




支持 UDP ESP 封装的微型端口驱动程序必须维护的分析器条目的列表。 分析器条目包含 NIC 分析已卸载的安全关联 (Sa) 上的传入 UDP ESP 数据包所需的信息。

分析器条目包含以下信息：

-   UDP ESP 封装类型。

    目前，只有一种封装类型支持。 有关基本 UDP ESP 封装类型的说明，请参阅[UDP ESP 封装类型](udp-esp-encapsulation-types.md)。

-   目标封装端口。

    它对卸载 SAs 可以处理入站 UDP 封装的数据包的 UDP 标头中的目标端口应查找 NIC。 目前，只能在端口 4500 上支持的 ESP 数据包的 UDP 封装。

TCP/IP 传输维护自己的分析程序条目，它已卸载到微型端口驱动程序列表。 在添加或删除一个 UDP ESP SA，传输和微型端口驱动程序使用一个句柄来标识特定分析器条目。

请注意，分析器条目允许 UDP ESP 功能被扩展，如有必要，以适应不同封装类型和每个封装类型的多个端口。

### <a name="adding-a-udp-esp-sa-and-parser-entry"></a>添加 UDP ESP SA 和分析器条目

TCP/IP 传输请求微型端口驱动程序通过发出针对这些 SAs，添加一个或多个 UDP ESP SAs 和分析器条目[OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569809)请求。 **EncapTypeEntry**卸载成员\_IPSEC\_添加\_UDPESP\_SA 结构包含分析器条目信息。

之前发出 OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA 请求，TCP/IP 传输确定正在卸载针对该 SAs 的分析器条目是否在其指定的 IP 接口的分析器条目列表。

-   如果分析器条目不在列表中的传输，传输将创建其自己的条目和集的副本**EncapTypeEntryOffloadHandle**卸载成员\_IPSEC\_添加\_UDPESP\_SA 结构**NULL**。 传输然后颁发[OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569809)请求。 收到请求后，该微型端口驱动程序确定是否分析器条目的**EncapTypeEntry**指定位于 NIC 的分析器条目列表。

    -   如果指定的分析器条目不在 NIC 的分析器条目列表中，微型端口驱动程序通过封装类型来创建分析器条目和目标端口中指定**EncapTypeEntry**并将分析器条目添加到 NIC 的分析器条目列表。 微型端口驱动程序随后将负载分流 OID 中指定 SAs\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA 请求。 已成功完成后 OID 请求，微型端口驱动程序返回的句柄**EncapTypeEntryOffloadHandle**用于标识新创建的解析器条目。 微型端口驱动程序也会返回一个句柄，标识在卸载的 SAs **OffloadHandle**卸载成员\_IPSEC\_添加\_UDPESP\_SA 结构。
    -   如果指定的分析器条目已在分析器条目列表中的 NIC，微型端口驱动程序只需返回中的句柄**EncapTypeEntryOffloadHandle**为现有的分析程序条目。 微型端口驱动程序也会返回一个句柄，标识在卸载的 SAs **OffloadHandle**卸载成员\_IPSEC\_添加\_UDPESP\_SA 结构。

    如果微型端口驱动程序完成 OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA 请求成功，传输将其副本的新的分析器条目添加到其自己的分析器条目给定的 IP 接口的列表。 此外，传输逐个增加分析器条目的引用计数。 传输使用此引用计数来枚举多少卸载的 UDP ESP SAs 与相关联的分析程序条目。

    如果微型端口驱动程序失败 OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA 请求时，传输将放弃其分析程序条目的副本。 此类请求微型端口驱动程序时，必须确保它已不是，实际上，添加了分析器条目并卸载 SAs。

-   如果分析程序条目已传输的分析器条目列表中，微型端口驱动程序已添加的分析器条目以响应上一个 OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA 的请求。 在这种情况下，传输的一个，集递增分析器条目的引用计数**EncapTypeEntryOffloadHandle**微型端口驱动程序之前返回的值。 传输然后发出 OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA 请求这用于请求微型端口驱动程序使用的是其他 SAs 分析器的某个现有条目正在卸载。 在这种情况下，微型端口驱动程序只应返回**OffloadHandle**标识卸载的 SAs。 如果 OID\_TCP\_任务\_IPSEC\_添加\_UDPESP\_SA 请求失败，传输递减引用计数为分析器条目。

### <a name="deleting-a-udp-esp-sa-and-parser-entry"></a>UDP ESP SA 和分析器条目删除

TCP/IP 传输请求微型端口驱动程序来删除这些 SAs 通过发出一个或多个 SAs 和可能的分析器条目[OID\_TCP\_任务\_IPSEC\_删除\_UDPESP\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569811)请求。

发出此请求前, TCP/IP 与要删除的 SAs 关联的分析器项的引用计数传输递减。 传输然后测试是否引用计数为零。

-   如果引用计数不为零，分析器条目是与当前卸载到 NIC 的一个或多个其他 SAs 关联 在这种情况下，传输设置**EncapTypeEntryOffldHandle**卸载成员\_IPSEC\_删除\_UDPESP\_SA 结构**NULL**. 收到 OID 后\_TCP\_任务\_IPSEC\_删除\_UDPESP\_SA 请求，微型端口驱动程序只需删除 OID 中指定 SAs\_TCP\_任务\_IPSEC\_删除\_UDPESP\_SA 请求。

-   如果引用计数为零，分析器项不与任何其他已卸载到 NIC 的 SAs 在这种情况下，传输设置**EncapTypeEntryOffldHandle**微型端口驱动程序之前返回的分析器条目句柄的值的成员。 微型端口驱动程序中删除指定的分析器条目和指定的 SAs。

如果微型端口驱动程序失败 OID\_TCP\_任务\_IPSEC\_删除\_UDPESP\_SA 请求，它应将指定的 SAs 标记并在适当时指定的分析器条目删除和执行删除更高版本。 若要处理传入的数据包，微型端口驱动程序必须使用分析器条目或标记为删除的 SA。

请注意，传输可以请求微型端口驱动程序删除 SA 或分析器条目 （或两者） 的微型端口驱动程序之前完成添加 SA 或分析器该项 （或两者）。 因此，微型端口驱动程序必须序列化具有加法运算的删除操作。

 

 





