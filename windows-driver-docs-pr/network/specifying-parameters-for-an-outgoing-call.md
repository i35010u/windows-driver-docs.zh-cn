---
title: 指定呼出通话的参数
description: 指定呼出通话的参数
ms.assetid: 6e11dcd7-33ae-4b9e-8609-1baccec691d5
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，传出呼叫
- telephonic services WDK WAN，传出呼叫
- CoNDIS TAPI WDK 网络，传出呼叫
- 语音流 WDK networing，传出呼叫
- 传出呼叫 WDK CoNDIS WAN
- 调用 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5008ed9100247ddb6e342aa62580765d2a2a12ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841871"
---
# <a name="specifying-parameters-for-an-outgoing-call"></a>指定呼出通话的参数





发出传出呼叫时，支持语音流的呼叫管理器或 MCM 必须在[**CO\_调用\_manager\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))结构中提供以下值：

-   最大传输 SDU 大小（CallMgrParameters-&gt;MaxSduSize）

-   最大接收 SDU 大小（CallMgrParameters-&gt;MaxSduSize）

如果呼叫管理器或 MCM 支持除 CO\_ADDRESS\_家族以外的地址族，\_TAPI\_代理会在将 TAPI 调用参数转换为 NDIS 调用参数以响应 OID 的查询[\_CO\_TAPI\_转换\_TAPI\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)。

支持 CO\_地址\_系列的呼叫管理器或 MCM 系列\_TAPI\_代理系列将这些值写入[**ProtocolCmMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_make_call)的上下文中的 co\_才能. 请注意，传递给*ProtocolCmMakeCall*函数的最大 SDU 大小不正确。 *ProtocolCmMakeCall*函数必须用正确的值覆盖不正确的值。

 

 





