---
title: wmitrace.traceoperation
description: Wmitrace.traceoperation 扩展在 Windows 中显示从跟踪组件的进度消息。
ms.assetid: 92d189fe-fb3b-40a6-81a8-9e66868c4d1d
keywords:
- wmitrace.traceoperation Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.traceoperation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f87ca73192cdd724136b772b1f04ada53e35f39a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331026"
---
# <a name="wmitracetraceoperation"></a>!wmitrace.traceoperation


**！ Wmitrace.traceoperation**扩展在 Windows 中将显示从跟踪组件的进度消息。

```dbgcmd
!wmitrace.traceoperation {0 | 1 | 2} 
```

## <a name="span-idddkwmitracetraceoperationdbgspanspan-idddkwmitracetraceoperationdbgspanparameters"></a><span id="ddk__wmitrace_traceoperation_dbg"></span><span id="DDK__WMITRACE_TRACEOPERATION_DBG"></span>参数


<span id="_______0______"></span> **0**   
禁止显示跟踪进度消息。

<span id="_______1______"></span> **1**   
启用跟踪进度消息的显示功能。 显示生成的 WMI 跟踪调试器扩展的所有消息。

<span id="_______2______"></span> **2**   
启用跟踪进度消息的显示功能。 显示由 WMI 跟踪调试器扩展或 Tracefmt 生成的所有消息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。

<a name="remarks"></a>备注
-------

此扩展会导致跟踪组件以显示详细输出。 此功能可用于对软件跟踪进行故障排除。

 

 





