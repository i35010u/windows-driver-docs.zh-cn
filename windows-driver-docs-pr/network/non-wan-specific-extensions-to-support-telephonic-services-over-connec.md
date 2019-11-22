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
ms.openlocfilehash: a108ce51e90f654cd87465a95dcf00fd336b8b87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842766"
---
# <a name="non-wan-specific-extensions-to-support-telephonic-services-over-connection-oriented-ndis"></a>用于通过面向连接的 NDIS 支持电话服务的非 WAN 特定扩展





本主题介绍针对面向连接的 NDIS 的 TAPI 支持的非 WAN 特定扩展。 这些扩展是 NDIS/TAPI 转换 Oid。 这些扩展允许非 WAN 特定呼叫管理器和集成微型端口调用管理器（MCM）驱动程序，将 TAPI 参数转换为 NDIS 参数，将 tapi 参数转换为 NDIS 参数。 这些扩展允许支持 ATM 的呼叫管理器和 MCMs，例如，通过面向连接的媒体提供 TAPI 访问。 有关面向连接的 NDIS 的 TAPI 支持的特定于 WAN 的扩展的信息，请参阅[支持 Telephonic 服务的 CONDIS WAN 操作](condis-wan-operations-that-support-telephonic-services.md)。

不应将 NDIS/TAPI 转换 Oid 用于调用管理器或 MCMs，它们分别向[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)或[**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)注册结合\_地址\_系列\_TAPI\_代理。 相反，此类调用管理器和 MCMs 以及其 TAPI 客户端应在面向连接的结构中封装 TAPI 参数，如[CoNDIS 支持 Telephonic Services 的 WAN 操作](condis-wan-operations-that-support-telephonic-services.md)中所述。

NDIS/TAPI 转换 Oid 如下所示：

-   [OID\_CO\_TAPI\_转换\_TAPI\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)

    此 OID 请求调用管理器或 MCM 将客户端提供的 TAPI 调用参数转换为 NDIS 调用参数。 客户端通常使用调用管理器或 MCM 返回的 NDIS 调用参数作为输入（格式化为[**CO\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构）到[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)。 客户端使用**NdisClMakeCall**启动面向连接的调用。

-   [OID\_CO\_TAPI\_转换\_NDIS\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-ndis-callparams)

    此 OID 请求调用管理器或 MCM 将传入调用的 NDIS 调用参数（通过 CO\_调用\_参数结构传递到客户端的[**ProtocolClIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call)函数）转换为 TAPI 调用参数。 客户端使用由呼叫管理器或 MCM 返回的已翻译的 TAPI 调用参数来确定是接受还是拒绝传入呼叫。

-   [OID\_CO\_TAPI\_转换\_SAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-sap)

    此 OID 请求一个调用管理器或 MCM，以从客户端提供的 TAPI 调用参数中准备一个或多个 NDIS Sap。 客户端通常使用由呼叫管理器或 MCM 返回的 NDIS SAP 作为输入（格式化为[**CO\_SAP**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))结构）发送到[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)，客户端将在该 sap 上注册要接收传入调用的 SAP。

 

 





