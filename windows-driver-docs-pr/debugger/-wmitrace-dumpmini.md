---
title: wmitrace.dumpmini
description: Wmitrace.dumpmini 扩展显示系统跟踪片断，它存储在转储文件。
ms.assetid: c6b4c09f-3a73-4467-849b-8570477bc9af
keywords:
- wmitrace.dumpmini Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dumpmini
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ee4b78a48d3b20ee2a72f550f08da81499562f40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546439"
---
# <a name="wmitracedumpmini"></a>!wmitrace.dumpmini


**！ Wmitrace.dumpmini**扩展显示系统跟踪片断，它存储在转储文件。

```dbgcmd
!wmitrace.dumpmini
```

## <span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows Vista 和更高版本的 Windows 中可用。

仅调试小型转储文件或完整转储文件时，此扩展很有用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

*系统跟踪片断*是系统上下文日志的最后一个缓冲区的内容的副本。 正常情况下，这是跟踪会话记录器 ID 为 2。

 

 





