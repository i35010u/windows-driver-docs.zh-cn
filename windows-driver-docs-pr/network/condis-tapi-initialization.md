---
title: CoNDIS TAPI 初始化
description: CoNDIS TAPI 初始化
ms.assetid: eabb2038-ab64-4f48-8c94-e47d1139727b
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 联网，TAPI 服务
- WDK WAN，initiliazing 台电话服务
- 连接网络、 初始化的 CoNDIS TAPI WDK
- 正在初始化的 CoNDIS TAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18ae52beb0e0fbbdb94f8dab7d259e349aea1d23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370607"
---
# <a name="condis-tapi-initialization"></a>CoNDIS TAPI 初始化





本部分讨论的 CoNDIS WAN 的微型端口驱动程序如何枚举应用程序及其 TAPI 功能。 这些 TAPI 功能包括：

-   线路设备微型端口驱动程序支持-线路设备包括，例如，调制解调器，传真板和 ISDN 卡的数量。

-   用于信息的特定行-行信息包括，例如，行标识符和通道地址 （电话号码） 支持同时传输的语音和数据的行数。

-   行的设备上的特定通道地址信息地址信息包括，例如，调用方 (调用方 ID) 和活动的调用可能数的标识。

若要检索有关基础硬件的信息，NDPROXY 发出请求的行和通道地址功能。 也就是说，NDPROXY 驱动程序将查询的 CoNDIS WAN 的微型端口驱动程序的 TAPI 功能。 NDPROXY 驱动程序调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)函数查询微型端口驱动程序的 TAPI 功能。 在此调用，NDPROXY 传递 NDIS\_OID\_请求结构。 NDPROXY NDIS 中指定以下\_OID\_请求：

-   **NdisRequestQueryInformation**中的值**RequestType**成员

-   对象标识符 (OID)，指定要检索的微型端口驱动程序的 TAPI 功能**Oid**成员

-   要保存 TAPI 功能信息中返回的缓冲区**InformationBuffer**成员

发送到由 NDPROXY 驱动程序的 CoNDIS WAN 微型端口驱动程序的所有查询可以同步或异步方式都完成。 如果 WAN 的 CoNDIS 微型端口驱动程序确定它不能立即完成查询，则它可以只返回 NDIS\_状态\_PENDING 并调用[ **NdisMCmOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequestcomplete)中的函数及其*ProtocolCoOidRequest*函数完成查询时。

之后的 CoNDIS WAN 的微型端口驱动程序会 NDPROXY 通知有关注册中指定的新地址系列[CoNDIS TAPI 注册](condis-tapi-registration.md)，NDPROXY 查询来确定的 TAPI 特定于功能的以下 OidWAN 的 CoNDIS 微型端口驱动程序和微型端口驱动程序的 nic。

-   NDPROXY 查询微型端口驱动程序与[OID\_共同\_TAPI\_CM\_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-cm-caps)来确定微型端口驱动程序的设备支持的行数 （适用于设备的 it提供的 TAPI 服务）。 此 OID 还会请求微型端口驱动程序，以指示这些行是否具有不同的行的功能。

-   NDPROXY 接下来将查询与微型端口驱动程序[OID\_共同\_TAPI\_行\_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-line-caps)来确定指定的行的电话服务功能。 此 OID 还会请求微型端口驱动程序，以指示该线路上的地址是否具有不同地址功能。
    -   如果前面的查询的 OID\_CO\_TAPI\_CM\_CAPS 指示微型端口驱动程序的设备支持只有一行，或如果设备支持具有相同的行功能的多个行，具有 NDPROXY查询 OID\_CO\_TAPI\_行\_大写字母仅一次，以获取设备的行功能。 在这种情况下，由微型端口驱动程序返回的行功能不适用于在设备上的所有行。
    -   如果设备支持不同的行功能的多个行，NDPROXY 必须查询 OID\_CO\_TAPI\_行\_大写字母一次为每个行，以获取每个行的行功能。
-   最后，NDPROXY 查询微型端口驱动程序与[OID\_共同\_TAPI\_地址\_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-address-caps)来确定指定的行上指定的地址的电话服务功能。
    -   如果前面的查询的 OID\_CO\_TAPI\_行\_行支持只能有一个地址，或在行上的所有地址，都具有相同的地址能力，指示 CAPS NDPROXY 查询 OID\_CO\_TAPI\_地址\_CAPS 仅一次来确定在行上的所有地址的功能。
    -   如果命令行支持具有不同功能的多个地址，NDPROXY 查询 OID\_CO\_TAPI\_地址\_CAPS 一次为每个地址在行上。

NDPROXY 驱动程序使用 TAPI 枚举 Oid 中获得的信息来执行以下操作：

-   创建 TAPI TAPI 的后续调用的参数。

-   确定是否接受或拒绝传入 TAPI 的后续调用。

-   要接收传入的后续 TAPI 调用注册一个或多个 TAPI 服务访问点 (SAPs)。

 

 





