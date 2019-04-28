---
title: logexts.logm
description: Logexts.logm 扩展创建或显示模块包含列表或模块的排除列表。
ms.assetid: 1037ba25-ffa6-4edd-99fd-bd0e249f4b37
keywords:
- logexts.logm Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b0d75d3eda156570b2ddfec2a11544465382ca8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336124"
---
# <a name="logextslogm"></a>!logexts.logm


**！ Logexts.logm**扩展创建或显示模块包含列表或模块的排除列表。

```dbgcmd
!logexts.logm i Modules 
!logexts.logm x Modules 
!logexts.logm 
```

## <a name="span-idddklogextslogmdbgspanspan-idddklogextslogmdbgspanparameters"></a><span id="ddk__logexts_logm_dbg"></span><span id="DDK__LOGEXTS_LOGM_DBG"></span>参数


<span id="_______i______"></span><span id="_______I______"></span> **i**   
会导致记录器要使用模块包含列表。 它将包含的指定*模块*。

<span id="_______x______"></span><span id="_______X______"></span> **x**   
会导致记录器要使用模块的排除列表。 它将包含 Logexts.dll、 kernel32.dll，以及指定*模块*。

<span id="_______Modules______"></span><span id="_______modules______"></span><span id="_______MODULES______"></span> *模块*   
指定要包括或排除的模块。 此列表不是累积计数器;每次使用此命令创建一个全新的列表。 如果列出多个模块，请用空格分隔它们。 一个星号 (\*) 能用来表示所有模块。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[记录器和日志查看器](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

不带任何参数， **！ logexts.logm**扩展显示当前的包含列表或排除列表。

扩展 **！ logexts.logm x \\** * 和 **！ logexts.logm 我**是等效的： 它们会导致完全为空的包含列表。

扩展 **！ logexts.logm 我\\** * 和 **！ logexts.logm x**是等效的： 它们会导致包含仅 Logexts.dll 和 kernel32.dll 的排除列表。 这两个模块始终为排除，因为不允许使用记录器以记录本身。

下面是一些可能的恶意活动：

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

 

 





