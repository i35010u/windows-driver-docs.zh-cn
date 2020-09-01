---
title: 面向连接的 NDIS 上用于 TAPI 的非 WAN 特定扩展
description: 用于通过面向连接的 NDIS 支持电话服务的非 WAN 特定扩展
ms.assetid: be677971-8c4a-435a-81b1-ff1ad9d849b4
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，TAPI 服务
- telephonic services WDK WAN，非 WAN 特定扩展
- CoNDIS TAPI WDK 网络，非 WAN 特定扩展
- NDIS/TAPI 转换 Oid WDK 网络
- 面向连接的 NDIS WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f902ee49ed82c486925fdf3e3a4240b57f2d8a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211031"
---
# <a name="non-wan-specific-extensions-to-support-telephonic-services-over-connection-oriented-ndis"></a>用于通过面向连接的 NDIS 支持电话服务的非 WAN 特定扩展





本主题介绍针对面向连接的 NDIS 的 TAPI 支持的非 WAN 特定扩展。 这些扩展是 NDIS/TAPI 转换 Oid。 这些扩展允许非 WAN 特定呼叫管理器和集成微型端口呼叫管理器 (MCM) 驱动程序，将 TAPI 参数转换为 NDIS 参数或将 TAPI 参数转换为 NDIS 参数。 这些扩展允许支持 ATM 的呼叫管理器和 MCMs，例如，通过面向连接的媒体提供 TAPI 访问。 有关面向连接的 NDIS 的 TAPI 支持的特定于 WAN 的扩展的信息，请参阅 [支持 Telephonic 服务的 CONDIS WAN 操作](condis-wan-operations-that-support-telephonic-services.md)。

不应将 NDIS/TAPI 转换 Oid 用于调用管理器或 MCMs，它们分别向 \_ \_ NdisCmRegisterAddressFamilyEx 或 NDISMCMREGISTERADDRESSFAMILYEX 注册 CO ADDRESS 系列 \_ TAPI \_ [**NdisCmRegisterAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)代理。 [**NdisMCmRegisterAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex) 相反，此类调用管理器和 MCMs 以及其 TAPI 客户端应在面向连接的结构中封装 TAPI 参数，如 [CoNDIS 支持 Telephonic Services 的 WAN 操作](condis-wan-operations-that-support-telephonic-services.md)中所述。

NDIS/TAPI 转换 Oid 如下所示：

-   [OID \_ CO \_ TAPI \_ 转换 \_ TAPI \_ CALLPARAMS](./oid-co-tapi-translate-tapi-callparams.md)

    此 OID 请求调用管理器或 MCM 将客户端提供的 TAPI 调用参数转换为 NDIS 调用参数。 客户端通常使用调用管理器或 MCM 返回的 NDIS 调用参数作为输入 (格式设置为) 到[**NdisClMakeCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)的[**联合 \_ 调用 \_ 参数**](/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构。 客户端使用 **NdisClMakeCall** 启动面向连接的调用。

-   [OID \_ CO \_ TAPI \_ 转换 \_ NDIS \_ CALLPARAMS](./oid-co-tapi-translate-ndis-callparams.md)

    此 OID 请求调用管理器或 MCM 将传入调用的 NDIS 调用参数转换为传入调用 (传递给 \_ \_ 客户端的 [**ProtocolClIncomingCall**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call) 函数) 到 TAPI 调用参数。 客户端使用由呼叫管理器或 MCM 返回的已翻译的 TAPI 调用参数来确定是接受还是拒绝传入呼叫。

-   [OID \_ 联合 \_ TAPI \_ 转换 \_ SAP](./oid-co-tapi-translate-tapi-sap.md)

    此 OID 请求一个调用管理器或 MCM，以从客户端提供的 TAPI 调用参数中准备一个或多个 NDIS Sap。 客户端通常使用由呼叫管理器或 MCM 返回的 NDIS SAP 作为) 到[**NdisClRegisterSap**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)的[**共同 \_ SAP**](/previous-versions/windows/hardware/network/ff545392(v=vs.85))结构的输入 (，并使用客户端注册要在其上接收传入调用的 sap。

 

