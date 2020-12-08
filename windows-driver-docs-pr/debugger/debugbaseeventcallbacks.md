---
title: debugbaseeventcallbacks
description: DebugBaseEventCallbacks 类提供 IDebugEventCallbacks 接口的基实现。
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
ms.openlocfilehash: e577507044d082bc410fed3c1e89dff775d725e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788823"
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

 

