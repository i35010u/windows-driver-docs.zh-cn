---
title: rcdrkd.rcdrsearchpath
description: Rcdrkd.rcdrsearchpath 扩展设置的跟踪消息格式 (TMF) 和跟踪消息控件 (TMC) 文件的搜索路径。
ms.assetid: AB19DC1B-009E-445A-B66B-5CC7EF54086F
keywords:
- rcdrkd.rcdrsearchpath Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrsearchpath
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edf7feb4f5665989db20cac792a09e019697a305
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542766"
---
# <a name="rcdrkdrcdrsearchpath"></a>!rcdrkd.rcdrsearchpath


**！ Rcdrkd.rcdrsearchpath**扩展设置消息控件 (TMC) 文件的跟踪消息格式 (TMF) 和跟踪的搜索路径。

```dbgcmd
!rcdrkd.rcdrsearchpath FilePath
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______FilePath______"></span><span id="_______filepath______"></span><span id="_______FILEPATH______"></span> *FilePath*   
格式化文件的路径。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

<a name="remarks"></a>备注
-------

此命令设置的搜索路径优先于跟踪中指定的搜索路径\_格式\_搜索\_PATH 环境变量。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






