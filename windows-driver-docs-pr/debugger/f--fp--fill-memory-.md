---
title: f、fp（填充内存）
description: F 和 fp 命令使用重复模式填充指定的内存范围。不应将这些命令与 ~ F (冻结线程) 命令混淆。
keywords:
- f、fp (填充内存) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- f, fp (Fill Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b67a82328c6d9246fb46fbe625370cc3e21c03f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819182"
---
# <a name="f-fp-fill-memory"></a>f、fp（填充内存）


**F** 和 **fp** 命令使用重复模式填充指定的内存范围。

不应将这些命令与 [**~ F (冻结线程)**](-f--freeze-thread-.md) 命令混淆。

```dbgcmd
f Range Pattern 
fp [MemoryType] PhysicalRange Pattern
```

## <a name="span-idddk_cmd_fill_memory_dbgspanspan-idddk_cmd_fill_memory_dbgspanparameters"></a><span id="ddk_cmd_fill_memory_dbg"></span><span id="DDK_CMD_FILL_MEMORY_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定虚拟内存中要填充的范围。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______PhysicalRange______"></span><span id="_______physicalrange______"></span><span id="_______PHYSICALRANGE______"></span>*PhysicalRange*   
仅 (内核模式) 在物理内存中指定要填充的范围。 *PhysicalRange* 的语法与虚拟内存范围的语法相同，不同之处在于不允许使用符号名。

<span id="_______MemoryType______"></span><span id="_______memorytype______"></span><span id="_______MEMORYTYPE______"></span>*MemoryType*   
仅 (内核模式) 指定物理内存的类型，可以是以下类型之一：

<span id="_c_"></span><span id="_C_"></span>**\[ansi-c\]**  
缓存的内存。

<span id="_uc_"></span><span id="_UC_"></span>**\[通信\]**  
未缓存内存。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc.exe\]**  
写入合并内存。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
指定一个或多个用于填充内存的字节值。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p></p>
<strong>f：</strong> 用户模式，内核模式 <strong>fp：</strong> 仅限内核模式</td>
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

此命令用指定 *模式* 填充 *范围* 指定的内存区域，并根据需要多次重复。

*Pattern* 参数的输入必须为一系列字节。 这些字符可以作为数字或 ASCII 字符输入。

数值将被解释为当前基数 (16、10或 8) 中的数字。 若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。 可以通过指定 **0x** 前缀 (十六进制) 、 **0n** 前缀 (decimal) 、 **0t** 前缀 (八进制) 或 **w..1 ....** 前缀 (binary) 来替代默认基数。

**注意**   使用 c + + 表达式时，默认基数的行为会有所不同。 有关详细信息，请参阅 [计算表达式](evaluating-expressions.md) 主题。

 

如果使用了 ASCII 字符，则每个字符必须用单引号引起来。 不能使用 C 样式转义字符，如 " \\ 0" 或 " \\ n" )  (。

如果指定了多个字节，则它们必须用空格分隔。

如果 *模式* 具有的值多于范围中的字节数，则调试器将忽略额外的值。

下面是一些示例。 假设当前基数为16，则以下命令将使用模式 "ABC" 填充内存位置0012FF40 到0012FF5F，重复多次：

```dbgcmd
0:000> f 0012ff40 L20 'A' 'B' 'C'
```

以下命令具有完全相同的效果：

```dbgcmd
0:000> f 0012ff40 L20 41 42 43
```

下面的示例演示如何使用内核模式下的 **fp** 命令 (**c**、 **uc** 和 **wc.exe**) 中的物理内存类型：

```dbgcmd
kd> fp [c] 0012ff40 L20 'A' 'B' 'C'
```

```dbgcmd
kd> fp [uc] 0012ff40 L20 'A' 'B' 'C'
```

```dbgcmd
kd> fp [wc] 0012ff40 L20 'A' 'B' 'C'
```

 

 





