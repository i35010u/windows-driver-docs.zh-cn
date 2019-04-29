---
title: m（移动内存）
description: M 命令将从一个位置的内存的内容复制到另一个。 不要混淆此命令使用 ~ m （恢复线程） 命令。
ms.assetid: afcac933-6bba-4566-ae07-bb9110f851d2
keywords:
- m （移动内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- m (Move Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 837478b76e8307f050d9e4e9a6a0064acef5e74a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383307"
---
# <a name="m-move-memory"></a>m（移动内存）


**M**命令将内存中的内容从一个位置复制到另一个。

不要将使用此命令相混淆[ **~ （恢复线程） 的 m** ](-m--resume-thread-.md)命令。

```dbgcmd
m Range Address 
```

## <a name="span-idddkcmdmovememorydbgspanspan-idddkcmdmovememorydbgspanparameters"></a><span id="ddk_cmd_move_memory_dbg"></span><span id="DDK_CMD_MOVE_MEMORY_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定要复制的内存区域。 此参数的语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的目标内存区域的起始地址。 此参数的语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

有关内存操作和其他与内存相关的命令的说明的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

内存区域的*地址*指定可以是内存区域的一部分的*范围*指定。 重叠移动已正确处理。

 

 





