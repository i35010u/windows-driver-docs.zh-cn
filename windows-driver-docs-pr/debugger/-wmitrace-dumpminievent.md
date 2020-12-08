---
title: wmitrace.dumpminievent
description: Wmitrace. dumpminievent 扩展显示系统事件日志跟踪片段，该片段存储在转储文件中。
keywords:
- wmitrace dumpminievent Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dumpminievent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7df4cd508a33e9082d22c7506380fca9f5d8fe7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823557"
---
# <a name="wmitracedumpminievent"></a>!wmitrace.dumpminievent


**！ Wmitrace dumpminievent** 扩展显示系统事件日志跟踪片段，该片段存储在转储文件中。

```dbgcmd
!wmitrace.dumpminievent
```

## <span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 Windows Vista Service Pack 1 (SP1) 和更高版本的 Windows 中可用。

此扩展仅在调试小型转储文件或完整转储文件时才有用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows 驱动程序工具包 (WDK) 。

<a name="remarks"></a>备注
-------

*系统事件日志跟踪片段* 是系统事件日志的最后一个缓冲区的内容副本。 **！ Wmitrace dumpminievent** 扩展以事件日志格式显示其内容。

 

 





