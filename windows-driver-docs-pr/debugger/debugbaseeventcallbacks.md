---
title: debugbaseeventcallbacks
description: DebugBaseEventCallbacks 类提供了 IDebugEventCallbacks 接口的基实现。
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
ms.openlocfilehash: b03e86ab589997584c3900a4c236c30004a6bcf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361413"
---
# <a name="debugbaseeventcallbacks-class"></a>DebugBaseEventCallbacks 类 

DebugBaseEventCallbacks 类提供的基实现[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)接口。 

程序可以从 DebugBaseEventCallbacks 派生事件回调类并实现所需方法。 

请注意适当地实现 GetInterestMask。
 
### <a name="requirements"></a>要求

Header

Dbgeng.h （包括 Dbgeng.h）  


### <a name="see-also"></a>请参阅
[DebugBaseEventCallbacksWide](debugbaseeventcallbackswide.md)

 

 





