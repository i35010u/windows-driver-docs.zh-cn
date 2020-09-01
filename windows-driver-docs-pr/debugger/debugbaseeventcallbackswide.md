---
title: debugbaseeventcallbackswide
description: DebugBaseEventCallbacksWide 类提供 IDebugEventCallbacksWide 接口的基实现。
ms.assetid: 38AD8472-1BA3-42EA-99CE-E91098A5B334
keywords:
- DebugBaseEventCallbacksWide
ms.date: 01/10/2018
topic_type:
- apiref
api_name:
- debugbaseeventcallbackswide
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bf9a8783d2b274951c1e4a9c752f619433261c4f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211199"
---
# <a name="debugbaseeventcallbackswide-class"></a>DebugBaseEventCallbacksWide 类 

DebugBaseEventCallbacksWide 类提供 [IDebugEventCallbacksWide](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbackswide) 接口的基实现。 

程序可以从 DebugBaseEventCallbacksWide 派生事件回调类并仅实现所需的方法。 

请小心地实现 GetInterestMask。
 
### <a name="requirements"></a>要求

标头

Dbgeng (包含 Dbgeng)   


### <a name="see-also"></a>另请参阅
[DebugBaseEventCallbacks](debugbaseeventcallbacks.md)

 

