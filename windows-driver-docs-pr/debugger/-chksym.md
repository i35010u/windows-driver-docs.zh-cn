---
title: chksym
description: Chksym 扩展会根据符号文件测试模块的有效性。
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
ms.openlocfilehash: 5d7452f80d1102ded08a8b116dbd3de4e4a02a5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795751"
---
# <a name="chksym"></a>!chksym


**！ Chksym** extension 根据符号文件测试模块的有效性。

```dbgsyntax
    !chksym Module [Symbol] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
按名称或基址指定模块的名称。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span>*符号*   
指定符号文件的名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果未指定符号，则会测试加载的符号。 否则，如果指定 .pdb 或 dbg 符号文件路径，则已加载的符号将针对已加载的模块进行测试。

 

 





