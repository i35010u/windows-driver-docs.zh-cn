---
title: 列表
description: 列表扩展插件指定的调试器命令重复执行，一次的链接列表中的每个元素。
ms.assetid: 763742f3-1cb8-4263-861b-b9d01483245e
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
ms.openlocfilehash: cbd26bdccc2b040a85939746860817aeb175f461
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336199"
---
# <a name="list"></a>!list


**！ 列表**扩展指定的调试器命令重复执行，一次的链接列表中的每个元素。

```dbgcmd
!list -t [Module!]Type.Field -x "Commands" [-a "Arguments"] [Options] StartAddress 
!list " -t [Module!]Type.Field -x \"Commands\" [-a \"Arguments\"] [Options] StartAddress " 
!list -h 
```

## <a name="span-idddklistdbgspanspan-idddklistdbgspanparameters"></a><span id="ddk__list_dbg"></span><span id="DDK__LIST_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
可选参数，指定定义此结构的模块。 如果可能，*类型*可能匹配的有效符号中的另一个模块，应包括*模块*以消除混淆。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *Type*   
指定数据结构的名称。

<span id="_______Field______"></span><span id="_______field______"></span><span id="_______FIELD______"></span> *字段*   
指定包含该列表链接的字段。 实际上，这可以是一系列用句点分隔的字段 (即， **Type.Field.Subfield.Subsubfield**，依此类推)。

<span id="_______-x__Commands_"></span><span id="_______-x__commands_"></span><span id="_______-X__COMMANDS_"></span> **-x "**<em>Commands</em>**"**  
指定要执行的命令。 这可以是调试器命令的任意组合。 它必须括在引号中。 如果指定了多个命令，单独用分号分隔，它们括起来的整个集合 **！ 列表**在引号中，并使用转义符的参数 ( \\ ) 之前在这些外部内每个引号引号引起来。 如果*命令*是省略，默认值是[ **dp （显示内存）**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)。

<span id="_______-a__Arguments_"></span><span id="_______-a__arguments_"></span><span id="_______-A__ARGUMENTS_"></span> **-a "**<em>Arguments</em>**"**  
指定要传递给参数*命令*参数。 这必须括在引号内。 *自变量*可以是任何有效的参数字符串中通常允许执行此命令中的，不同之处在于*自变量*不能包含引号引起来。 如果伪寄存器 **$extret**中包含*命令*，则 **-a"**<em>参数</em>**"** 可以省略参数。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是任意数量的以下选项：

<span id="-e"></span><span id="-E"></span>**-e**  
将回显正在执行的每个元素的命令。

<span id="-m_Max"></span><span id="-m_max"></span><span id="-M_MAX"></span>**-m** *Max*  
指定要执行的命令的元素的最大数目。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定的第一个数据结构的地址。 这是结构的顶部，不一定是结构的链接字段的地址的地址。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

**！ 列表**扩展会经历链接列表，并发出一次为每个列表元素指定的命令。

伪寄存器 **$extret**设置为每个列表元素的列表条目地址的值。 对于每个元素，该命令字符串*命令*执行。 此命令字符串可以引用此伪寄存器，使用 **$extret**语法。 如果这不会显示在命令字符串中，列表条目地址的值追加到前执行的命令字符串的末尾。 如果你需要指定此值应显示在命令中的位置，必须显式指定此伪寄存器。

列表中的 null 指针，终止或终止循环回第一个元素之前，将运行此命令序列。 如果列表循环到更高版本的元素上，此命令不会停止。 但是，通过使用，随时停止此命令[ **CTRL + C** ](ctrl-c--break-.md) KD 和 CDB 中或[调试 |中断](debug---break.md)或 CTRL + BREAK 在 WinDbg 中。

每次执行命令时，当前结构的地址将用作*默认地址*如果正在使用的命令具有可选地址参数。

以下是两个示例说明了如何在用户模式下使用此命令。 请注意，内核模式下使用情况，也可以遵循不同的语法。

作为一个简单的示例，假定您具有其类型名称是一个结构**MYTYPE**，并且具有内的链接其 **.links。Flink**和 **.links。闪烁**字段。 您有一个链接的列表的开头处 0x6BC000 结构。 以下扩展命令将遍历列表并将为每个元素执行[ **dd** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) L2 命令。 因为没有地址指定给**dd**命令时，需要为所需的地址列表开头的地址。 这会导致要显示的每个结构前两个 dword 值。

```dbgcmd
0:000> !list -t MYTYPE.links.Flink -x "dd" -a "L2" 0x6bc00 
```

作为更复杂的示例，请考虑使用的用例 **$extret**。 它遵循类型的列表\_列表\_处项**RtlCriticalSectionList**。 对于每个元素，它显示前四个 dword 值，并随后显示\_RTL\_严重\_部分\_调试结构位于之前的八个字节的偏移量**Flink**列表项的元素。

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

 

 





