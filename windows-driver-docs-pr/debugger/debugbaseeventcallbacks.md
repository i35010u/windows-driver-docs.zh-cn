---
title: debugbaseeventcallbacks
description: DebugBaseEventCallbacks 类提供 IDebugEventCallbacks 接口的基实现。
ms.assetid: B0422248-2F5F-4AE6-93C9-D96B5E4A1B5A
keywords:
- DebugBaseEventCallbacks
ms.date: 01/10/2018
topic_type:
- apiref
api_name:
- debugbaseeventcallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17a95a0b5dc1dbcabccb4070d2675370a73f836e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211201"
---
# <a name="debugbaseeventcallbacks-class"></a>DebugBaseEventCallbacks 类 

DebugBaseEventCallbacks 类提供 [IDebugEventCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) 接口的基实现。 

程序可以从 DebugBaseEventCallbacks 派生事件回调类并仅实现所需的方法。 

请小心地实现 GetInterestMask。
 
### <a name="requirements"></a>要求

标头

Dbgeng (包含 Dbgeng)   


### <a name="see-also"></a>另请参阅
[DebugBaseEventCallbacksWide](debugbaseeventcallbackswide.md)

 

