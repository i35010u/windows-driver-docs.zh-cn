---
title: wmitrace.dumpmini
description: Wmitrace. dumpmini 扩展显示系统跟踪片段，它存储在转储文件中。
keywords:
- wmitrace dumpmini Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dumpmini
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1a6a0034805ffb4fd90ae9afae7425734dae25e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823561"
---
# <a name="wmitracedumpmini"></a>!wmitrace.dumpmini


**！ Wmitrace dumpmini** 扩展显示系统跟踪片段，它存储在转储文件中。

```dbgcmd
!wmitrace.dumpmini
```

## <span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 Windows Vista 和更高版本的 Windows 中可用。

此扩展仅在调试小型转储文件或完整转储文件时才有用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows 驱动程序工具包 (WDK) 。

<a name="remarks"></a>备注
-------

*系统跟踪片段* 是系统上下文日志的最后一个缓冲区的内容副本。 在正常情况下，这是跟踪会话，其记录器 ID 为2。

 

 





