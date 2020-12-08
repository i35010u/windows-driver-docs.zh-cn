---
title: wmitrace.traceoperation
description: Wmitrace. traceoperation 扩展显示 Windows 中跟踪组件的进度消息。
keywords:
- wmitrace traceoperation Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.traceoperation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a430685d6e41b4829806fe095ab81e61c4d62423
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819355"
---
# <a name="wmitracetraceoperation"></a>!wmitrace.traceoperation


！ Traceoperation 扩展显示 Windows 中跟踪组件的进度消息 **wmitrace。**

```dbgcmd
!wmitrace.traceoperation {0 | 1 | 2} 
```

## <a name="span-idddk__wmitrace_traceoperation_dbgspanspan-idddk__wmitrace_traceoperation_dbgspanparameters"></a><span id="ddk__wmitrace_traceoperation_dbg"></span><span id="DDK__WMITRACE_TRACEOPERATION_DBG"></span>参数


<span id="_______0______"></span>**0**   
禁用跟踪进度消息的显示。

<span id="_______1______"></span>**1**   
启用跟踪进度消息的显示。 将显示由 WMI 跟踪调试器扩展生成的所有消息。

<span id="_______2______"></span>**2**   
启用跟踪进度消息的显示。 将显示由 WMI 跟踪调试器扩展或 Tracefmt 生成的所有消息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。

<a name="remarks"></a>备注
-------

此扩展导致跟踪组件显示详细输出。 此功能可用于排查软件跟踪问题。

 

 





