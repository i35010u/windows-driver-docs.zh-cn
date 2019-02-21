---
title: wmitrace.dumpminievent
description: Wmitrace.dumpminievent 扩展将显示在转储文件中存储的系统事件日志跟踪片段。
ms.assetid: 94debe5f-d125-44d0-99c4-90d8794525df
keywords:
- wmitrace.dumpminievent Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dumpminievent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2881cbcef477c2b111d43cf0e40ee55566614813
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554155"
---
# <a name="wmitracedumpminievent"></a>!wmitrace.dumpminievent


**！ Wmitrace.dumpminievent**扩展插件都会显示在转储文件中存储的系统事件日志跟踪片段。

```dbgcmd
!wmitrace.dumpminievent
```

## <span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows Vista Service Pack 1 (SP1) 和更高版本的 Windows 中可用。

仅调试小型转储文件或完整转储文件时，此扩展很有用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

*系统事件日志跟踪片断*是最后一个缓冲区的系统事件日志中的内容的副本。 **！ Wmitrace.dumpminievent**扩展事件日志格式显示其内容。

 

 





