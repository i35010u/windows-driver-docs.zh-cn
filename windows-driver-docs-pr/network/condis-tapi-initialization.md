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
ms.openlocfilehash: 78c21c9f178d70dbe353afc8034b5c4e08910baf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835054"
---
# <a name="condis-tapi-initialization"></a>CoNDIS TAPI 初始化





本部分讨论 CoNDIS WAN 微型端口驱动程序如何枚举应用程序的 TAPI 功能。 这些 TAPI 功能包括：

-   线路设备数量微型端口驱动程序支持的线路设备，例如调制解调器、传真板和 ISDN 卡。

-   有关特定行的信息，例如行标识符和通道地址（电话号码）的数量，该行支持同时传输语音和数据。

-   有关设备行上特定通道地址的信息-地址信息包括调用方的标识（调用方 ID）和可能的活动调用数。

若要检索有关基础硬件的信息，NDPROXY 会发出请求线路和通道地址的请求。 也就是说，NDPROXY 驱动程序查询 CoNDIS WAN 微型端口驱动程序的 TAPI 功能。 NDPROXY 驱动程序调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)函数来查询微型端口驱动程序的 TAPI 功能。 在此调用中，NDPROXY 将 NDIS\_OID\_请求结构。 NDPROXY 在 NDIS\_OID\_请求中指定以下内容：

-   **RequestType**成员中的**NdisRequestQueryInformation**值

-   一个对象标识符（OID），指定要从**OID**成员的微型端口驱动程序中检索的 TAPI 功能

-   用于保存在**InformationBuffer**成员中返回的 TAPI 功能信息的缓冲区

通过 NDPROXY 驱动程序发送到 CoNDIS WAN 微型端口驱动程序的所有查询均可同步或异步完成。 如果 CoNDIS WAN 微型端口驱动程序确定它无法立即完成查询，则它可以直接将 NDIS\_状态返回\_挂起，并从其 ProtocolCoOidRequest 中调用[**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete)函数。函数完成查询。

CoNDIS WAN 微型端口驱动程序通知 NDPROXY 注册[CONDIS TAPI 注册](condis-tapi-registration.md)中指定的新地址系列时，NDPROXY 会查询以下 oid，以确定 CoNDIS WAN 微型端口驱动程序的 TAPI 特定功能和微型端口驱动程序的 NIC。

-   NDPROXY 使用 OID 查询小型端口驱动程序[\_CO\_TAPI\_CM\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-cm-caps)来确定微型端口驱动程序的设备（它为其提供 TAPI 服务的设备）支持的行数。 此 OID 还请求微型端口驱动程序，以指示这些行是否具有不同的行功能。

-   接下来，NDPROXY 会查询带有 OID 的小型小型驱动程序[\_CO\_TAPI\_行\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-line-caps)来确定指定行的电话功能。 此 OID 还请求微型端口驱动程序，以指示此行上的地址是否具有不同的地址功能。
    -   如果以前的 OID 查询\_CO\_TAPI\_CM\_CAP 指示微型端口驱动程序的设备只支持一行，或者如果设备支持多行具有相同的线路功能，NDPROXY 必须查询 OID\_仅\_的 TAPI\_LINE\_CAP，以获取设备的线路功能。 在这种情况下，微型端口驱动程序返回的线路功能适用于设备上的所有线条。
    -   如果设备支持多个线路功能不同的行，则 NDPROXY 必须\_的\_CO TAPI\_行\_CAP 一次，以获取每行的行功能。
-   最后，NDPROXY 使用 OID 查询小型端口驱动程序[\_CO\_TAPI\_地址\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-address-caps)来确定指定行上指定地址的电话功能。
    -   如果上次查询 OID\_CO\_TAPI\_行\_CAP 指示该行仅支持一个地址，或者该行上的所有地址都具有相同的地址功能，NDPROXY 查询 OID\_CO\_TAPI\_ADDRESS 仅\_CAP 一次，以确定行中所有地址的功能。
    -   如果某行支持具有不同功能的多个地址，则 NDPROXY 查询 OID\_每条地址的\_TAPI\_地址\_CAP。

NDPROXY 驱动程序使用通过 TAPI 枚举 Oid 获取的信息来执行以下操作：

-   为后续 TAPI 调用创建 TAPI 参数。

-   确定是接受还是拒绝后续的传入 TAPI 调用。

-   注册一个或多个要在其上接收后续传入 TAPI 调用的 TAPI 服务访问点（Sap）。

 

 





