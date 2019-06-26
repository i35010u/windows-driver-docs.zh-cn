---
title: 通过面向连接的 NDIS TAPI 的非 WAN 特定扩展
description: 用于通过面向连接的 NDIS 支持电话服务的非 WAN 特定扩展
ms.assetid: be677971-8c4a-435a-81b1-ff1ad9d849b4
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 联网，TAPI 服务
- 台电话服务 WDK WAN，非特定于 WAN 的扩展
- CoNDIS TAPI WDK 网络连接、 非 WAN 特定扩展
- NDIS/TAPI 翻译 Oid WDK 网络
- 面向连接的 NDIS WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa5744ef33c0e2485e374c10ec07bbcf69dd5ce6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354534"
---
# <a name="non-wan-specific-extensions-to-support-telephonic-services-over-connection-oriented-ndis"></a>用于通过面向连接的 NDIS 支持电话服务的非 WAN 特定扩展





本主题介绍通过面向连接的 NDIS TAPI 支持的非 WAN 特定扩展。 这些扩展是 NDIS/TAPI 翻译 Oid。 这些扩展允许非 WAN 特定调用管理器并集成微型端口调用管理器 (MCM) 驱动程序转换到 NDIS 参数或 TAPI 参数为 NDIS 参数 TAPI 参数。 这些扩展允许调用管理器和 MCMs 支持 ATM，例如，支持 TAPI 通过面向连接的媒体。 有关通过面向连接的 NDIS TAPI 支持的特定于 WAN 的扩展的信息，请参阅[CoNDIS WAN 操作支持台电话服务的](condis-wan-operations-that-support-telephonic-services.md)。

不应调用管理器或 MCMs 分别注册共同使用 NDIS/TAPI 翻译 Oid\_地址\_系列\_TAPI\_与代理[ **NdisCmRegisterAddressFamilyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregisteraddressfamilyex)或[ **NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregisteraddressfamilyex)。 相反，此类调用管理器和 MCMs，以及其 TAPI 客户端，应封装 TAPI 参数在面向连接的结构，如中所述[CoNDIS WAN 操作台电话服务的支持](condis-wan-operations-that-support-telephonic-services.md)。

NDIS/TAPI 翻译 Oid 如下所示：

-   [OID\_CO\_TAPI\_TRANSLATE\_TAPI\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)

    此 OID 请求呼叫管理器或 MCM 转换 TAPI 提供的客户端到 NDIS 调用参数的调用参数。 客户端通常使用返回的呼叫管理器或作为输入的 MCM 的 NDIS 调用参数 (格式为[**共同\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构) 到[ **NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)。 客户端使用**NdisClMakeCall**启动面向连接的调用。

-   [OID\_CO\_TAPI\_TRANSLATE\_NDIS\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-ndis-callparams)

    此 OID 请求要转换的传入呼叫的 NDIS 调用参数的呼叫管理器或 MCM (传入共同\_调用\_到客户端的参数结构[ **ProtocolClIncomingCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_call)函数) 到 TAPI 调用参数。 客户端使用返回的呼叫管理器或 MCM 的已翻译的 TAPI 调用参数来确定是否接受或拒绝传入呼叫。

-   [OID\_CO\_TAPI\_TRANSLATE\_SAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-sap)

    此 OID 请求呼叫管理器或 MCM 准备从客户端提供的 TAPI 调用参数的一个或多个 NDIS SAPs。 客户端通常使用 NDIS SAP 返回的呼叫管理器或作为输入的 MCM (格式为[**共同\_SAP** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))结构) 到[ **NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap)，与其客户端注册 SAP 要接收传入的呼叫。

 

 





