---
title: list
description: 列表扩展为链接列表中的每个元素重复执行指定的调试器命令。
keywords:
- 列出 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- list
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 88882210c9ff1bee35019ee7b55a4134045f0d5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828943"
---
# <a name="list"></a>!list


**！列表** 扩展为链接列表中的每个元素重复执行指定的调试器命令。

```dbgcmd
!list -t [Module!]Type.Field -x "Commands" [-a "Arguments"] [Options] StartAddress 
!list " -t [Module!]Type.Field -x \"Commands\" [-a \"Arguments\"] [Options] StartAddress " 
!list -h 
```

## <a name="span-idddk__list_dbgspanspan-idddk__list_dbgspanparameters"></a><span id="ddk__list_dbg"></span><span id="DDK__LIST_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定定义此结构的模块的可选参数。 如果可能 *类型* 与不同模块中的有效符号相匹配，则应包含 *模块* 以消除多义性。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span>*类型*   
指定数据结构的名称。

<span id="_______Field______"></span><span id="_______field______"></span><span id="_______FIELD______"></span>*字段*   
指定包含列表链接的字段。 这实际上可以是由句点分隔的一系列字段 (换言之， **Subsubfield**，等等) 。

<span id="_______-x__Commands_"></span><span id="_______-x__commands_"></span><span id="_______-X__COMMANDS_"></span>**-x "**<em>命令</em>**"**  
指定要执行的命令。 这可以是调试器命令的任意组合。 必须用引号将其引起来。 如果指定了多个命令，请用分号分隔它们，将 **！ list** 参数的整个集合用引号引起来，并在 \\ 这些外引号内使用转义符 ( ) 。 如果省略 *命令* ，则默认值为 [**Dp (显示内存)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)。

<span id="_______-a__Arguments_"></span><span id="_______-a__arguments_"></span><span id="_______-A__ARGUMENTS_"></span>**-a "**<em>Arguments</em>**"**  
指定要传递给 *命令* 参数的参数。 必须用引号将其引起来。 *自* 变量可以是任何有效的参数字符串（通常允许使用此命令），但 *参数* 不能包含引号。 如果 *命令* 中包含伪寄存器 **$extret** ，则可以省略 **-a "**<em>Arguments</em>**"** 参数。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列任意数量的选项：

<span id="-e"></span><span id="-E"></span>**-e**  
回显为每个元素执行的命令。

<span id="-m_Max"></span><span id="-m_max"></span><span id="-M_MAX"></span>**-m** *最大值*  
指定要对其执行命令的元素的最大数目。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定第一个数据结构的地址。 这是结构顶部的地址，不一定是链接字段的地址。

<span id="_______-h______"></span><span id="_______-H______"></span>**-h**   
在调试器命令窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**！列表** 扩展将通过链接列表，并对每个列表元素发出指定的命令一次。

伪寄存器 **$extret** 设置为每个列表元素的列表项地址的值。 对于每个元素，都会执行命令字符串 *命令* 。 此命令字符串可以使用 **$extret** 语法来引用此伪寄存器。 如果此命令未出现在命令字符串中，则在执行之前，列表输入地址的值将追加到命令字符串的末尾。 如果需要指定此值应在命令中出现的位置，则必须显式指定此伪寄存器。

此命令序列将运行，直到列表在空指针中终止，或循环返回到第一个元素。 如果列表循环返回到后面的元素，则此命令不会停止。 但是，你可以通过在 KD 和 CDB 中使用 [**CTRL + C**](ctrl-c--break-.md) 来随时停止此命令，也可以使用 [Debug |](debug---break.md) 在 WinDbg 中中断或 CTRL + break。

每次执行命令时，如果所使用的命令具有可选的地址参数，则将使用当前结构的地址作为 *默认地址* 。

下面是如何在用户模式下使用此命令的两个示例。 请注意，也可能采用不同的语法，也可以使用内核模式。

作为一个简单的示例，假设你有一个类型名称为 **MYTYPE** 的结构，该结构的链接中有链接 **。Flink** 和 **。闪烁** 字段。 您有一个链接列表，该列表以0x6BC000 的结构开头。 以下扩展命令将经过列表，每个元素将执行 [**dd**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) L2 命令。 由于没有为 **dd** 命令指定地址，它会将列表标题的地址作为所需的地址。 这将导致显示每个结构中的前两个 Dword。

```dbgcmd
0:000> !list -t MYTYPE.links.Flink -x "dd" -a "L2" 0x6bc00 
```

更复杂的示例，请考虑使用 **$extret** 的情况。 它位于 RtlCriticalSectionList 的类型列表项的列表之后 \_ \_ 。 **RtlCriticalSectionList** 对于每个元素，它将显示前四个 DWORD，然后 \_ \_ \_ \_ 在列表项的 **Flink** 元素之前的偏移量上显示 "RTL 临界区调试结构"。

```dbgcmd
0:000> !list "-t ntdll!_LIST_ENTRY.Flink -e -x \"dd @$extret l4; dt ntdll!_RTL_CRITICAL_SECTION_DEBUG @$extret-0x8\" ntdll!RtlCriticalSectionList"
dd @$extret l4; dt ntdll!_RTL_CRITICAL_SECTION_DEBUG @$extret-0x8
7c97c0c8  7c97c428 7c97c868 01010000 00000080
   +0x000 Type             : 1
   +0x002 CreatorBackTraceIndex : 0
   +0x004 CriticalSection  : (null)
   +0x008 ProcessLocksList : _LIST_ENTRY [ 0x7c97c428 - 0x7c97c868 ]
   +0x010 EntryCount       : 0x1010000
   +0x014 ContentionCount  : 0x80
   +0x018 Spare            : [2] 0x7c97c100

dd @$extret l4; dt ntdll!_RTL_CRITICAL_SECTION_DEBUG @$extret-0x8
7c97c428  7c97c448 7c97c0c8 00000000 00000000
   +0x000 Type             : 0
   +0x002 CreatorBackTraceIndex : 0
   +0x004 CriticalSection  : 0x7c97c0a0
   +0x008 ProcessLocksList : _LIST_ENTRY [ 0x7c97c448 - 0x7c97c0c8 ]
   +0x010 EntryCount       : 0
   +0x014 ContentionCount  : 0
   +0x018 Spare            : [2] 0
```

 

 





