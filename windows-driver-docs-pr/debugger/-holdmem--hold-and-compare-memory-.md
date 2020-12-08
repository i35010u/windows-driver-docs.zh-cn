---
title: .holdmem（保留和比较内存）
description: Holdmem 命令保存内存范围，并将其与其他内存范围进行比较。
keywords:
- 保持和比较内存 ( holdmem) 命令
- 内存，保留并比较内存 ( holdmem) 命令
- holdmem (在) Windows 调试时保留和比较内存
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .holdmem (Hold and Compare Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 41c10a83f90f495a399300bf83ff116f3c38b108
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825823"
---
# <a name="holdmem-hold-and-compare-memory"></a>.holdmem（保留和比较内存）


**Holdmem** 命令保存内存范围，并将其与其他内存范围进行比较。

```dbgcmd
.holdmem -a Range 
.holdmem -d { Range | Address } 
.holdmem -D 
.holdmem -o 
.holdmem -c Range 
```

## <a name="span-idddk_meta_hold_and_compare_memory_dbgspanspan-idddk_meta_hold_and_compare_memory_dbgspanparameters"></a><span id="ddk_meta_hold_and_compare_memory_dbg"></span><span id="DDK_META_HOLD_AND_COMPARE_MEMORY_DBG"></span>参数


<span id="_______-a_Range_____________"></span><span id="_______-a_range_____________"></span><span id="_______-A_RANGE_____________"></span>**-a**  **** *范围*   
指定要保存的内存范围。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______-d___Range___Address__"></span><span id="_______-d___range___address__"></span><span id="_______-D___RANGE___ADDRESS__"></span>**-d** * * * * {*范围*  |  *地址*}  
指定要删除的内存范围。 如果指定 *address*，则调试器将删除任何包含该地址的已保存范围。 如果指定 *range*，则调试器将删除与 *范围* 重叠的任何已保存范围。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______-D______"></span><span id="_______-d______"></span>**-D**   
删除所有保存的内存范围。

<span id="_______-o______"></span><span id="_______-O______"></span>**-o**   
显示所有已保存的内存范围。

<span id="_______-c_______Range______"></span><span id="_______-c_______range______"></span><span id="_______-C_______RANGE______"></span>**-c** *范围*   
将指定的范围与所有保存的内存范围进行比较。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何操作内存的详细信息以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

**Holdmem** 命令比较内存范围字节的字节。

如果任何指定的内存位置在虚拟地址空间中不存在，则该命令将返回一个错误。

 

 





