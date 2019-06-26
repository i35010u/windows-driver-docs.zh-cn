---
title: 指定呼出通话的参数
description: 指定呼出通话的参数
ms.assetid: 6e11dcd7-33ae-4b9e-8609-1baccec691d5
keywords:
- CoNDIS WAN 的驱动程序 WDK 网络拨出电话
- WDK WAN，拨出电话的电话服务
- 拨出电话的 CoNDIS TAPI WDK 网络
- 流式处理 WDK networing，拨出电话的语音
- WDK 的 CoNDIS WAN 的传出呼叫
- 调用 WDK 的 CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18128c857ec0d5837d054385692141edf0da662f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383626"
---
# <a name="specifying-parameters-for-an-outgoing-call"></a>指定呼出通话的参数





使传出呼叫、 呼叫管理器或 MCM 支持语音的流式处理时必须提供中的以下值[**共同\_调用\_MANAGER\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))结构：

-   最大传输 SDU 大小 (CallMgrParameters-&gt;Transmit.MaxSduSize)

-   最大接收 SDU 大小 (CallMgrParameters-&gt;Receive.MaxSduSize)

呼叫管理器或支持共同以外的地址族的 MCM\_地址\_系列\_TAPI\_代理时，填充这些值转换到 NDIS 的 TAPI 调用参数的查询响应中调用参数[OID\_共同\_TAPI\_TRANSLATE\_TAPI\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)。

呼叫管理器或支持产生的 CO MCM\_地址\_系列\_TAPI\_代理系列将这些值写入到产生的 CO\_调用\_MANAGER\_参数结构上下文及其[ **ProtocolCmMakeCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_make_call)函数。 请注意，SDU 大小最大值传递给*ProtocolCmMakeCall*函数不正确。 *ProtocolCmMakeCall*函数必须使用正确的值覆盖不正确的值。

 

 





