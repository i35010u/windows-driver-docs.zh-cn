---
title: 指定来电的参数
description: 指定来电的参数
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，传入呼叫
- telephonic services WDK WAN，传入呼叫
- CoNDIS TAPI WDK 网络，传入呼叫
- 语音流 WDK networing，传入呼叫
- 呼入 CoNDIS WAN
- 调用 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 875c0975181b5c82c1a0ddda3c0b59e3e3d964a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831235"
---
# <a name="specifying-parameters-for-an-incoming-call"></a>指定来电的参数





当使用 **Ndis (M) CmDispatchIncomingCall** 指示传入调用时，支持语音流的调用管理器或 MCM 必须在 [**共同 \_ 调用 \_ 管理器 \_ 参数**](/previous-versions/windows/hardware/network/ff545381(v=vs.85)) 结构中指定以下值：

-   最大传输 SDU 大小 (CallMgrParameters &gt; MaxSduSize) 

-   最大接收 SDU 大小 (CallMgrParameters &gt; MaxSduSize) 

此外，呼叫管理器或 MCM 必须在行 \_ 调用信息结构中指定以下值 \_ ：

-   **ulMediaMode**

    此字段应包含 \_ 映射到 TAPI 3.0 TAPIMEDIAMODE 音频的 LINEMEDIAMODE AUTOMATEDVOICE \_ 。

-   **ulCallerIDFlags**

-   **ulCallerIDSize**

-   **ulCallerIDOffset**

-   **ulCallerIDNameSize**

-   **ulCallerIDNameOffset**

-   **ulCalledIDFlags**

-   **ulCalledIDSize**

-   **ulCalledIDOffset**

-   **ulCalledIDNameSize**

-   **ulCalledDNameOffset**

-   **ulCallerIDAddressType**

-   **ulCalledIDAddressType**

如果呼叫管理器或 MCM 支持除 CO address 系列 TAPI 代理之外的地址族，则在 \_ \_ \_ \_ \_ \_ 响应 [OID \_ CO \_ tapi \_ 转换 \_ NDIS \_ CALLPARAMS](./oid-co-tapi-translate-ndis-callparams.md) 查询时，将指定前面的行调用信息成员。

呼叫管理器或支持 CO \_ ADDRESS \_ 系列 \_ TAPI 代理系列的 MCM 指定了在 \_ \_ \_ \_ \_ \_ 其提供给 **Ndis (M) CmDispatchIncomingCall** 的共同调用管理器参数结构的媒体特定部分中列出的行调用信息成员。

有关行调用信息结构中成员的说明 \_ \_ ，请参阅 Microsoft Windows SDK 文档中的 LINECALLINFO 结构。

 

