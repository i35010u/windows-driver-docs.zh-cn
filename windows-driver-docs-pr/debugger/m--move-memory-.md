---
title: m（移动内存）
description: M 命令将内存内容从一个位置复制到另一个位置。 请勿将此命令与 ~ m 混淆 (Resume Thread) 命令。
keywords:
- m (移动内存) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- m (Move Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c09e8199ab5aa2860073abec31a7de30cfe0809c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808487"
---
# <a name="m-move-memory"></a>m（移动内存）


**M** 命令将内存内容从一个位置复制到另一个位置。

请勿将此命令与 [**~ m 混淆 (Resume Thread)**](-m--resume-thread-.md) 命令。

```dbgcmd
m Range Address 
```

## <a name="span-idddk_cmd_move_memory_dbgspanspan-idddk_cmd_move_memory_dbgspanparameters"></a><span id="ddk_cmd_move_memory_dbg"></span><span id="DDK_CMD_MOVE_MEMORY_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定要复制的内存区域。 有关此参数的语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定目标内存区域的起始地址。 有关此参数的语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

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

有关内存操作的详细信息以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

*地址* 指定的内存区域可以是该 *范围* 指定的内存区域的一部分。 重叠的移动得到正确处理。

 

 





