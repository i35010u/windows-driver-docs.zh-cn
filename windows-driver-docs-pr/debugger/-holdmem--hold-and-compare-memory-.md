---
title: .holdmem（保留和比较内存）
description: .Holdmem 命令保存内存范围并将其与其他内存范围比较。
ms.assetid: d8caa0df-c87d-4378-9a39-cc04760ca0db
keywords:
- 保存并比较内存 (.holdmem) 命令
- 内存中，保存并比较内存 (.holdmem) 命令
- .holdmem （保留和比较内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .holdmem (Hold and Compare Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ffc93cde2e93e7781b494d6d9768b4869b4d4394
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563273"
---
# <a name="holdmem-hold-and-compare-memory"></a>.holdmem（保留和比较内存）


**.Holdmem**命令保存内存范围并将其与其他内存范围比较。

```dbgcmd
.holdmem -a Range 
.holdmem -d { Range | Address } 
.holdmem -D 
.holdmem -o 
.holdmem -c Range 
```

## <a name="span-idddkmetaholdandcomparememorydbgspanspan-idddkmetaholdandcomparememorydbgspanparameters"></a><span id="ddk_meta_hold_and_compare_memory_dbg"></span><span id="DDK_META_HOLD_AND_COMPARE_MEMORY_DBG"></span>参数


<span id="_______-a_Range_____________"></span><span id="_______-a_range_____________"></span><span id="_______-A_RANGE_____________"></span> **-a** **** *Range*   
指定要保存的内存范围。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______-d___Range___Address__"></span><span id="_______-d___range___address__"></span><span id="_______-D___RANGE___ADDRESS__"></span> **-d** **** { *Range* | *Address* }  
指定要删除的内存范围。 如果指定*地址*，调试器将删除任何已保存的范围，其中包含该地址。 如果指定*范围*，调试器将删除与重叠的任何已保存的范围*范围*。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______-D______"></span><span id="_______-d______"></span> **-D**   
删除所有已保存的内存范围。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
显示所有已保存的内存范围。

<span id="_______-c_______Range______"></span><span id="_______-c_______range______"></span><span id="_______-C_______RANGE______"></span> **-c** *Range*   
将指定范围内为所有已保存的内存范围进行比较。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

有关如何内存和其他与内存相关的命令的说明进行操作的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

**.Holdmem**命令将内存范围的逐字节进行比较。

如果虚拟地址空间中不存在任何指定的内存位置，该命令将返回错误。

 

 





