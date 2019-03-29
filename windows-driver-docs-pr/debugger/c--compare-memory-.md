---
title: c（比较内存）
description: C 命令将保存在两个内存方面的值进行比较。
ms.assetid: caa02ec3-35d6-4d41-a777-daa264b0dd18
keywords:
- c （比较内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- c (Compare Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1b9710d3b0d13736095086161908cb074088e85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564391"
---
# <a name="c-compare-memory"></a>c（比较内存）


**C**命令将保存在两个内存方面的值进行比较。

```dbgcmd
c Range Address 
```

## <a name="span-idddkcmdcomparememorydbgspanspan-idddkcmdcomparememorydbgspanparameters"></a><span id="ddk_cmd_compare_memory_dbg"></span><span id="DDK_CMD_COMPARE_MEMORY_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
第一个的两个内存范围进行比较。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
要进行比较的第二个内存范围起始地址。 此范围的大小将与第一个范围为指定的相同。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果两个方面不同，调试器将在他们不同意其中的第一个范围中显示所有的内存地址。

作为示例，请考虑以下代码：

```cpp
void main()
{
    char rgBuf1[100];
    char rgBuf2[100];

    memset(rgBuf1, 0xCC, sizeof(rgBuf1));
    memset(rgBuf2, 0xCC, sizeof(rgBuf2));

    rgBuf1[42] = 0xFF;
}
```

要比较**rgBuf1**并**rgBuf2**，使用以下命令之一：

```dbgcmd
0:000> c rgBuf1 (rgBuf1+0n100) rgBuf2

0:000> c rgBuf1 L 0n100 rgBuf2
```

 

 





