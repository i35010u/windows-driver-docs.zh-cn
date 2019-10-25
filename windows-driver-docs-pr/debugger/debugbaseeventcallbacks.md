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
ms.openlocfilehash: 6ed59e435e2d9f040e80e1c89dd83e66de4957ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837782"
---
# <a name="debugbaseeventcallbacks-class"></a>DebugBaseEventCallbacks 类 

DebugBaseEventCallbacks 类提供[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)接口的基实现。 

程序可以从 DebugBaseEventCallbacks 派生事件回调类并仅实现所需的方法。 

请小心地实现 GetInterestMask。
 
### <a name="requirements"></a>要求

标头

Dbgeng （包括 Dbgeng）  


### <a name="see-also"></a>另请参阅
[DebugBaseEventCallbacksWide](debugbaseeventcallbackswide.md)

 

 





