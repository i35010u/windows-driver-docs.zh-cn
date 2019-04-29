---
title: 调试器命令程序示例
description: 调试器命令程序示例
ms.assetid: da756906-6243-4cb9-b4e5-5b0b4540533d
keywords:
- 调试器命令程序中示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 161cd14ede3f952e299631ca29ee252963066230
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368150"
---
# <a name="debugger-command-program-examples"></a>调试器命令程序示例


## <span id="ddk_debugger_command_program_examples_dbg"></span><span id="DDK_DEBUGGER_COMMAND_PROGRAM_EXAMPLES_DBG"></span>


以下各节介绍调试器命令程序。

### <a name="span-idusingtheforeachtokenspanspan-idusingtheforeachtokenspanusing-the-foreach-token"></a><span id="using_the__foreach_token"></span><span id="USING_THE__FOREACH_TOKEN"></span>使用.foreach 令牌

下面的示例使用[ **.foreach** ](-foreach.md)令牌，若要搜索的 5a4d WORD 值。 对于每个找到的 5a4d 值，调试器将显示 8 DWORD 值，在其中找到 5a4d DWORD 的地址开始。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc place L8 } 
```

下面的示例使用[ **.foreach** ](-foreach.md)令牌，若要搜索的 5a4d WORD 值。 对于每个找到的 5a4d 值，调试器将显示 8 DWORD 值，从 4 个字节地址之前在其中找到 5a4d DWORD。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc place -0x4 L8 } 
```

以下示例显示相同的值。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc ( place -0x4 ) L8 } 
```

**请注意**  如果你想要对中的变量名称*OutCommands*部分的命令，必须在变量名之后添加一个空格。 例如，在以上示例中，没有空间变量之间*放置*和减法运算符。

 

**- \[1\]** 选项一起使用[ **s （内存搜索）** ](s--search-memory-.md)命令使其输出，以包括仅地址它会查找，不是，请参阅这些地址的值。

下面的命令显示位于在通过 0x7F000000 0x77000000 内存范围内的所有模块的模块详细信息。

```dbgcmd
0:000> .foreach (place { lm1m }) { .if ((${place} >= 0x77000000) & (${place} <= 0x7f000000)) { lmva place } } 
```

**1m**选项一起使用[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md)命令使其输出，以包含仅的模块的完整说明不的地址模块。

前面的示例使用[ **$ {} （别名解释器）** ](-------alias-interpreter-.md)令牌，以确保替换为别名，即使它们是其他文本旁边。 如果该命令未包括此令牌，左括号，则下一步**放置**阻止别名替换。 请注意， **${}** 令牌适用于使用中的变量 **.foreach**和 true 别名上。

### <a name="span-idwalkingtheprocesslistspanspan-idwalkingtheprocesslistspanwalking-the-process-list"></a><span id="walking_the_process_list"></span><span id="WALKING_THE_PROCESS_LIST"></span>进程列表的每个步骤

以下示例将指导完成内核模式进程列表，并在列表中显示的每个条目的可执行文件名称。

此示例应存储为文本文件并执行[  **$$ &gt; &lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)命令。 此命令加载整个文件，用分号，替换所有回车并执行生成的块。 此命令，可通过使用多个行和缩进，而不让整个程序展开为单行中榨出编写可读程序。

此示例说明了以下功能：

-   **美元 t0**， **$t1**，并 **$t2**伪寄存器用作此程序中的变量。 该程序还使用名为别名**Procc**并 **$ImageName**。

-   此程序使用 MASM 表达式计算器。 但是， **@@c+ + （)** 标记将出现一次。 此令牌会导致程序能够使用C++表达式计算器分析表达式的括号中。 这种用法使程序能够使用C++直接结构令牌。

-   **？** 与使用标志[ **r （寄存器）** ](r--registers-.md)命令。 此标志将类型化的值分配给伪寄存器 **$t2**。

```dbgcmd
$$  Get process list LIST_ENTRY in $t0.
r $t0 = nt!PsActiveProcessHead

$$  Iterate over all processes in list.
.for (r $t1 = poi(@$t0);
      (@$t1 != 0) & (@$t1 != @$t0);
      r $t1 = poi(@$t1))
{
    r? $t2 = #CONTAINING_RECORD(@$t1, nt!_EPROCESS, ActiveProcessLinks);
    as /x Procc @$t2

 $$  Get image name into $ImageName.
 as /ma $ImageName @@c++(&@$t2->ImageFileName[0])

 .block
    {
        .echo ${$ImageName} at ${Procc}
    }

    ad $ImageName
    ad Procc
}
```

### <a name="span-idwalkingtheldrdatatableentrylistspanspan-idwalkingtheldrdatatableentrylistspanwalking-the-ldrdatatableentry-list"></a><span id="walking_the_ldr_data_table_entry_list"></span><span id="WALKING_THE_LDR_DATA_TABLE_ENTRY_LIST"></span>遍历 LDR\_数据\_表\_条目列表

下面的示例演示了用户模式下 LDR\_数据\_表\_条目列表，并显示基址和每个列表项的完整路径。

如前面的示例中，此程序应保存在文件中并执行[  **$$ &gt; &lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)命令。

此示例说明了以下功能：

- 此程序使用 MASM 表达式计算器。 但是，在两个位置 **@@c+ + （)** 标记将出现。 此令牌会导致程序能够使用C++表达式计算器分析表达式的括号中。 这种用法使程序能够使用C++直接结构令牌。

- **？** 与使用标志[ **r （寄存器）** ](r--registers-.md)命令。 此标志将类型化的值分配给伪寄存器**美元 t0**并 **$t1**。 中的循环，正文 **$t1**具有类型 * * ntdll ！\_LDR\_数据\_表\_条目\\* * *，因此程序可以创建直接成员的引用。

- 用户命名别名 **$Base**并 **$Mod**此程序中使用。 美元符号降低当前的调试器会话中以前使用这些别名的可能性。 不需要美元符号的。 [ **${/ V 部分:}** ](-------alias-interpreter-.md)令牌解释别名按字面意思，阻止它被替换，如果运行该脚本之前定义它。 此令牌以及任何块还可用于防止使用别名定义块的前面。

- [ **.Block** ](-block.md)令牌用于添加一个额外的别名的更换步骤。 一次完整的脚本在加载时，输入每个块时一次执行了别名替换。 无需 **.block**令牌和及其左大括号 **.echo**命令不会收到的值 **$Mod**并 **$Base**的别名在以前的行中分配。

```dbgcmd
$$ Get module list LIST_ENTRY in $t0.
r? $t0 = &@$peb->Ldr->InLoadOrderModuleList
 
$$ Iterate over all modules in list.
.for (r? $t1 = *(ntdll!_LDR_DATA_TABLE_ENTRY**)@$t0;
 (@$t1 != 0) & (@$t1 != @$t0);
      r? $t1 = (ntdll!_LDR_DATA_TABLE_ENTRY*)@$t1->InLoadOrderLinks.Flink)
{
    $$ Get base address in $Base.
 as /x ${/v:$Base} @@c++(@$t1->DllBase)
 
 $$ Get full name into $Mod.
 as /msu ${/v:$Mod} @@c++(&@$t1->FullDllName)
 
 .block
    {
        .echo ${$Mod} at ${$Base}
    }
 
    ad ${/v:$Base}
    ad ${/v:$Mod}
}
```

 

 





