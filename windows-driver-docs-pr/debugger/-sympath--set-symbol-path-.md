---
title: .sympath （设置符号路径）
description: .Sympath 命令设置或更改的符号路径。 符号路径指定的调试器查找符号文件的位置。
ms.assetid: 32146871-a59f-4c93-b886-137c5ecf5c99
keywords:
- 设置符号路径 (.sympath) 命令
- 符号文件和路径，设置符号路径 (.sympath) 命令
- .sympath （设置符号路径） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sympath (Set Symbol Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35abbd135a02d86ef44baab83858a989ec4f3d4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525251"
---
# <a name="sympath-set-symbol-path"></a>.sympath （设置符号路径）


**.Sympath**命令设置或更改的符号路径。 符号路径指定的调试器查找符号文件的位置。

```dbgcmd
.sympath[+] [Path [; ...]]
```

## <a name="span-idddkmetasetsymbolpathdbgspanspan-idddkmetasetsymbolpathdbgspanparameters"></a><span id="ddk_meta_set_symbol_path_dbg"></span><span id="DDK_META_SET_SYMBOL_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
指定的新位置将追加到 （而不是替换） 的前一个符号搜索路径。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *路径*   
完全限定的路径或完全限定的路径的列表。 由分号分隔多个路径。 如果*路径*是省略，则显示当前符号路径。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和更改此路径的其他方法，请参阅[符号路径](symbol-path.md)。

<a name="remarks"></a>备注
-------

更改符号路径时，将不加载新符号信息。 可以使用[ **.reload （重新加载模块）** ](-reload--reload-module-.md)命令以重新加载符号。

 

 





