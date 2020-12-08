---
title: .sympath（设置符号路径）
description: Sympath 命令设置或更改符号路径。 符号路径指定调试器查找符号文件的位置。
keywords:
- 设置符号路径 ( sympath) 命令
- 符号文件和路径，将符号路径 ( 设置) 命令
- sympath (设置) Windows 调试的符号路径
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sympath (Set Symbol Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56fb6514db04ad4090f8fd42cc704cded549df85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832015"
---
# <a name="sympath-set-symbol-path"></a>.sympath（设置符号路径）


**Sympath** 命令设置或更改符号路径。 符号路径指定调试器查找符号文件的位置。

```dbgcmd
.sympath[+] [Path [; ...]]
```

## <a name="span-idddk_meta_set_symbol_path_dbgspanspan-idddk_meta_set_symbol_path_dbgspanparameters"></a><span id="ddk_meta_set_symbol_path_dbg"></span><span id="DDK_META_SET_SYMBOL_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
指定新位置将追加到 (而不是替换) 上一个符号搜索路径。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span>*路径*   
完全限定的路径或完全限定路径的列表。 多个路径之间用分号分隔。 如果省略 *路径* ，则显示当前的符号路径。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关更改此路径的详细信息和其他方式，请参阅 [符号路径](symbol-path.md)。

<a name="remarks"></a>备注
-------

更改符号路径时，不会加载新的符号信息。 您可以使用 [**. reload.sql (重载模块)**](-reload--reload-module-.md) 命令重新加载符号。

 

 





