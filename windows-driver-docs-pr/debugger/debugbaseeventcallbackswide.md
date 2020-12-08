---
title: debugbaseeventcallbackswide
description: DebugBaseEventCallbacksWide 类提供 IDebugEventCallbacksWide 接口的基实现。
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
ms.openlocfilehash: d09b03352b29e2be7c9acda6dae20353de76bb3a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788815"
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

 

