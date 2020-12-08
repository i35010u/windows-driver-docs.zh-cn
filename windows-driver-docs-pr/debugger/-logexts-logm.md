---
title: logexts.logm
description: Logexts. logm 扩展创建或显示模块包含列表或模块排除列表。
keywords:
- logexts logm Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c56a36578d0b861fe768c6f0a3ffc60d2f6b67d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829783"
---
# <a name="logextslogm"></a>!logexts.logm


**！ Logexts logm** 扩展创建或显示模块包含列表或模块排除列表。

```dbgcmd
!logexts.logm i Modules 
!logexts.logm x Modules 
!logexts.logm 
```

## <a name="span-idddk__logexts_logm_dbgspanspan-idddk__logexts_logm_dbgspanparameters"></a><span id="ddk__logexts_logm_dbg"></span><span id="DDK__LOGEXTS_LOGM_DBG"></span>参数


<span id="_______i______"></span><span id="_______I______"></span>**i**   
使记录器使用模块包含列表。 它将包含指定的 *模块*。

<span id="_______x______"></span><span id="_______X______"></span>**x**   
导致记录器使用模块排除列表。 它将包含 Logexts.dll、kernel32.dll 和指定的 *模块*。

<span id="_______Modules______"></span><span id="_______modules______"></span><span id="_______MODULES______"></span>*模块*   
指定要包括或排除的模块。 此列表不是累积性的;使用此命令时，将创建一个全新的列表。 如果列出了多个模块，请将它们与空格分隔开。 \*可以使用星号 () 来指示所有模块。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [记录器和 LogViewer](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

如果没有参数，则 **！ logexts. logm** 扩展将显示当前包含列表或排除列表。

Extension **！ logexts; logm \\ x** _ 和 _ *！ logexts* 等效：它们会导致完全空的包含列表。

Extension **！ logexts; logm \\ i** _ 和 _ *！ logexts* 等效：它们会生成一个排除列表，其中仅包含 Logexts.dll 和 kernel32.dll。 始终会排除这两个模块，因为记录器不允许记录自身。

下面是一些示例：

```dbgcmd
0:001> !logm
Excluded modules:
  LOGEXTS.DLL      [mandatory]
  KERNEL32.DLL     [mandatory]
  USER32.DLL
  GDI32.DLL
  ADVAPI32.DLL

0:001> !logm x winmine.exe
Excluded modules:
  Logexts.dll      [mandatory]
  kernel32.dll     [mandatory]
  winmine.exe

0:001> !logm x user32.dll gdi32.dll
Excluded modules:
  Logexts.dll      [mandatory]
  kernel32.dll     [mandatory]
  user32.dll
  gdi32.dll

0:001> !logm i winmine.exe mymodule2.dll
Included modules:
  winmine.exe
  mymodule2.dll
```

 

 





