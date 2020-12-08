---
title: c（比较内存）
description: C 命令比较两个内存区域中的值。
keywords:
- c (比较内存) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- c (Compare Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2ce893dafe67368861f02af316dd81f39d458d0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839323"
---
# <a name="c-compare-memory"></a>c（比较内存）


**C** 命令比较两个内存区域中的值。

```dbgcmd
c Range Address 
```

## <a name="span-idddk_cmd_compare_memory_dbgspanspan-idddk_cmd_compare_memory_dbgspanparameters"></a><span id="ddk_cmd_compare_memory_dbg"></span><span id="DDK_CMD_COMPARE_MEMORY_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
要进行比较的两个内存范围中的第一个。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
要比较的第二个内存范围的起始地址。 此范围的大小将与为第一个范围指定的大小相同。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

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

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果这两个区域不完全相同，则调试器将显示第一个范围中不一致的所有内存地址。

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

若要比较 **rgBuf1** 和 **rgBuf2**，请使用以下命令之一：

```dbgcmd
0:000> c rgBuf1 (rgBuf1+0n100) rgBuf2

0:000> c rgBuf1 L 0n100 rgBuf2
```

 

 





