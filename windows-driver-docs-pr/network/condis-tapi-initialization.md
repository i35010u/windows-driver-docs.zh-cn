---
title: CoNDIS TAPI 初始化
description: CoNDIS TAPI 初始化
ms.assetid: eabb2038-ab64-4f48-8c94-e47d1139727b
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，TAPI 服务
- telephonic services WDK WAN，initiliazing
- CoNDIS TAPI WDK 网络，初始化
- 初始化 CoNDIS TAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f01a468cf95705049dca8ccc821c19954818e6e5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218469"
---
# <a name="condis-tapi-initialization"></a>CoNDIS TAPI 初始化





本部分讨论 CoNDIS WAN 微型端口驱动程序如何枚举应用程序的 TAPI 功能。 这些 TAPI 功能包括：

-   线路设备数量微型端口驱动程序支持的线路设备，例如调制解调器、传真板和 ISDN 卡。

-   有关特定行的信息，例如行标识符和通道地址的数目 (电话号码) 行支持同时传输语音和数据。

-   有关设备行上特定通道地址的信息-地址信息包括调用方的标识 (调用方 ID) 和可能的活动调用数。

若要检索有关基础硬件的信息，NDPROXY 会发出请求线路和通道地址的请求。 也就是说，NDPROXY 驱动程序查询 CoNDIS WAN 微型端口驱动程序的 TAPI 功能。 NDPROXY 驱动程序调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 函数来查询微型端口驱动程序的 TAPI 功能。 在此调用中，NDPROXY 将传递 NDIS \_ OID \_ 请求结构。 NDPROXY 在 NDIS OID 请求中指定以下 \_ \_ 内容：

-   **RequestType**成员中的**NdisRequestQueryInformation**值

-    (OID) 的对象标识符，指定要从 **OID** 成员的微型端口驱动程序中检索的 TAPI 功能

-   用于保存在 **InformationBuffer** 成员中返回的 TAPI 功能信息的缓冲区

通过 NDPROXY 驱动程序发送到 CoNDIS WAN 微型端口驱动程序的所有查询均可同步或异步完成。 如果 CoNDIS WAN 微型端口驱动程序确定它无法立即完成查询，则它可以只返回 NDIS 状态 "挂起"， \_ \_ 并在它已完成查询时从其*ProtocolCoOidRequest*函数内调用[**NdisMCmOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete)函数。

在 CoNDIS WAN 微型端口驱动程序通知 NDPROXY 注册 [CONDIS TAPI 注册](condis-tapi-registration.md)中指定的新地址族后，NDPROXY 将查询以下 oid，以确定 CoNDIS WAN 微型端口驱动程序和微型端口驱动程序 NIC 的特定于 TAPI 的功能。

-   NDPROXY 使用 [OID \_ CO \_ TAPI \_ CM \_ cap](./oid-co-tapi-cm-caps.md) 查询小型小型驱动程序，以确定微型端口驱动程序的设备所支持的行数 (提供 TAPI 服务的设备) 。 此 OID 还请求微型端口驱动程序，以指示这些行是否具有不同的行功能。

-   接下来，NDPROXY 将通过 [OID \_ CO \_ TAPI \_ LINE \_ cap](./oid-co-tapi-line-caps.md) 查询微型端口驱动程序，以确定指定行的电话功能。 此 OID 还请求微型端口驱动程序，以指示此行上的地址是否具有不同的地址功能。
    -   如果前面的 OID \_ co \_ tapi \_ CM cap 查询 \_ 指出微型端口驱动程序的设备仅支持一行，或者如果设备支持多行具有相同的线路功能，则 NDPROXY 只需查询 OID \_ CO \_ tapi \_ 行 \_ 帽一次即可获取设备的线路功能。 在这种情况下，微型端口驱动程序返回的线路功能适用于设备上的所有线条。
    -   如果设备支持多行具有不同的线路功能，则 NDPROXY 必须 \_ \_ 针对每行查询 OID CO TAPI \_ line \_ cap 一次，以获取每行的行功能。
-   最后，NDPROXY 使用 [OID \_ CO \_ TAPI \_ 地址 \_ 上限](./oid-co-tapi-address-caps.md) 查询微型端口驱动程序，以确定指定行上指定地址的电话功能。
    -   如果前面的 OID \_ co \_ tapi \_ 行帽查询 \_ 指出该行仅支持一个地址，或者该行上的所有地址都具有相同的地址功能，则 NDPROXY 仅查询 OID \_ co \_ tapi \_ 地址 \_ 上限一次，以确定线路上所有地址的功能。
    -   如果某行支持具有不同功能的多个地址，则 NDPROXY \_ 会 \_ \_ \_ 在行的每个地址上查询 OID CO TAPI 地址 cap 一次。

NDPROXY 驱动程序使用通过 TAPI 枚举 Oid 获取的信息来执行以下操作：

-   为后续 TAPI 调用创建 TAPI 参数。

-   确定是接受还是拒绝后续的传入 TAPI 调用。

-   将一个或多个 TAPI 服务接入点注册 (Sap) ，以接收后续的传入 TAPI 呼叫。

 

