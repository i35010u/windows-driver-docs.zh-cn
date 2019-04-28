---
title: chksym
description: Chksym 扩展测试针对符号文件的模块的有效性。
ms.assetid: 52ea75cb-44a2-4c84-a3af-b3fc027348f4
keywords:
- chksym Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- chksym
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f8f6fce41e4fb8e70116fd1c15e38c70d512317
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336901"
---
# <a name="chksym"></a>!chksym


**！ Chksym**扩展测试针对符号文件的模块的有效性。

```dbgsyntax
    !chksym Module [Symbol] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定按其名称或基址的模块的名称。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *符号*   
指定符号文件的名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果未指定字段的符号，则测试加载的符号。 否则，如果指定.pdb 或.dbg 符号文件路径，加载的符号是针对已加载的模块进行测试。

 

 





