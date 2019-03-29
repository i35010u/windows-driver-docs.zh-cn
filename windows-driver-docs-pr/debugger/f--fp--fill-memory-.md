---
title: f、fp（填充内存）
description: F 和 fp 命令填充指定的内存范围由重复图案。这些命令不应混淆和 ~ F （冻结的线程） 命令。
ms.assetid: 9ef4eb88-dc6f-4f0f-ac01-a6b0bb42b33e
keywords:
- f，fp （填充内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- f, fp (Fill Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 26cc71ffeb8e555fae92b5408a3adf823cb96cca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565930"
---
# <a name="f-fp-fill-memory"></a>f、fp（填充内存）


**F**并**fp**命令填充指定的内存范围由重复图案。

不要将这些命令与相混淆[ **~ （冻结的线程） 的 F** ](-f--freeze-thread-.md)命令。

```dbgcmd
f Range Pattern 
fp [MemoryType] PhysicalRange Pattern
```

## <a name="span-idddkcmdfillmemorydbgspanspan-idddkcmdfillmemorydbgspanparameters"></a><span id="ddk_cmd_fill_memory_dbg"></span><span id="DDK_CMD_FILL_MEMORY_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
若要填充的虚拟内存中指定的范围。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______PhysicalRange______"></span><span id="_______physicalrange______"></span><span id="_______PHYSICALRANGE______"></span> *PhysicalRange*   
（仅适用于内核模式）中的物理内存来填充指定的范围。 语法*PhysicalRange*是虚拟内存范围相同，只允许有无符号的名称。

<span id="_______MemoryType______"></span><span id="_______memorytype______"></span><span id="_______MEMORYTYPE______"></span> *MemoryType*   
（仅适用于内核模式）指定的类型的物理内存，可以是以下之一：

<span id="_c_"></span><span id="_C_"></span>**\[c\]**  
内存缓存。

<span id="_uc_"></span><span id="_UC_"></span>**\[uc\]**  
未缓存的内存。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc\]**  
写入组合内存。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
指定一个或多个用来填充内存的字节值。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p></p>
<strong>f:</strong>用户模式下，内核模式<strong>fp:</strong>内核模式下</td>
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

此命令将填充指定的内存区域*范围*具有指定*模式*时，根据需要多次重复。

*模式*参数必须输入为一系列字节。 这些可以输入为 numeric 或作为 ASCII 字符。

数字值将被解释为当前基数 （16、 10 或 8） 中的数字。 若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。 可以通过指定重写默认基数**0x**前缀 （十六进制） **0n**前缀 （十进制） **0t**前缀 （八进制） 或**0y**前缀 （二进制）。

**请注意**  默认基数以不同方式行为时正在使用 c + + 表达式。 有关详细信息，请参阅[评估表达式](evaluating-expressions.md)主题。

 

如果使用 ASCII 字符，则每个字符必须括在直单引号中。 C 样式转义字符 (如\\0 或\\n) 不能使用。

如果指定了多个字节，它们必须由空格分隔。

如果*模式*的范围中具有值的字节数多于，调试器将忽略多余的值。

下面是一些示例。 假设当前基数为 16，以下命令将填充通过使用模式"ABC"重复几次 0012FF5F 内存位置 0012FF40:

```dbgcmd
0:000> f 0012ff40 L20 'A' 'B' 'C'
```

下面的命令具有完全相同的效果：

```dbgcmd
0:000> f 0012ff40 L20 41 42 43
```

下面的示例演示如何使用物理内存类型 (**c**， **uc**，并**wc**) 与**fp**命令在内核模式下：

```dbgcmd
kd> fp [c] 0012ff40 L20 'A' 'B' 'C'
```

```dbgcmd
kd> fp [uc] 0012ff40 L20 'A' 'B' 'C'
```

```dbgcmd
kd> fp [wc] 0012ff40 L20 'A' 'B' 'C'
```

 

 





