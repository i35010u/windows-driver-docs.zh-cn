---
title: 指定呼出通话的参数
description: 指定呼出通话的参数
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，传出呼叫
- telephonic services WDK WAN，传出呼叫
- CoNDIS TAPI WDK 网络，传出呼叫
- 语音流 WDK networing，传出呼叫
- 传出呼叫 WDK CoNDIS WAN
- 调用 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8657efc16602e47a900080e4b44b286d372b963
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831227"
---
# <a name="specifying-parameters-for-an-outgoing-call"></a>指定呼出通话的参数





发出传出呼叫时，支持语音 [**流的呼叫 \_ \_ \_**](/previous-versions/windows/hardware/network/ff545381(v=vs.85)) 管理器或 MCM 必须提供以下值：

-   最大传输 SDU 大小 (CallMgrParameters &gt; MaxSduSize) 

-   最大接收 SDU 大小 (CallMgrParameters &gt; MaxSduSize) 

如果呼叫管理器或 MCM 支持除 CO 地址族以外的地址族，则在将 \_ \_ \_ \_ tapi 调用参数转换为 NDIS 调用参数以响应 [OID \_ 联合 \_ tapi \_ 转换 \_ TAPI \_ CALLPARAMS](./oid-co-tapi-translate-tapi-callparams.md)的查询时，将填充这些值。

支持 CO ADDRESS 系列 TAPI 代理系列的呼叫管理器或 MCM 将 \_ \_ \_ \_ 这些值写入 \_ \_ \_ 其 [**ProtocolCmMakeCall**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_make_call) 函数上下文中的共同调用管理器参数结构。 请注意，传递给 *ProtocolCmMakeCall* 函数的最大 SDU 大小不正确。 *ProtocolCmMakeCall* 函数必须用正确的值覆盖不正确的值。

 

