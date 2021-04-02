---
title: 调试器命令程序示例
description: 调试器命令程序示例
keywords:
- 调试器命令程序，示例
ms.date: 03/30/2021
ms.localizationpriority: medium
ms.openlocfilehash: 7a7507c76f8fb64aa2479a9fae6a058b8c1b3332
ms.sourcegitcommit: 83a11e69f7b175011d032a179e4cfa6d5ede9ac2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2021
ms.locfileid: "106113630"
---
# <a name="debugger-command-program-examples"></a>调试器命令程序示例


以下部分介绍调试器命令程序。

## <a name="using-the-foreach-token"></a>使用 foreach 标记

下面的示例使用 [**foreach**](-foreach.md) 标记搜索5A4D 的 WORD 值。 对于找到的每个5a4d 值，调试器将显示8个 DWORD 值，从找到的 5a4d DWORD 的地址开始。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc place L8 } 
```

下面的示例使用 [**foreach**](-foreach.md) 标记搜索5A4D 的 WORD 值。 对于找到的每个5a4d 值，调试器将显示8个 DWORD 值，并在找到 5a4d DWORD 的地址之前的第4个字节开始。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc place -0x4 L8 } 
```

下面的示例显示相同的值。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc ( place -0x4 ) L8 } 
```

**注意**  如果要对命令的 *OutCommands* 部分中的变量名称执行操作，必须在变量名称后面添加一个空格。 例如，在上面的示例中，变量 *位置* 和减法运算符之间有一个空格。

 

**- \[ 1 \]** 选项与 [**(Search Memory)**](s--search-memory-.md)命令一起，使其输出只包含它找到的地址，而不包含在这些地址找到的值。

以下命令显示位于从0x77000000 到0x7F000000 的内存范围内的所有模块的详细模块信息。

```dbgcmd
0:000> .foreach (place { lm1m }) { .if ((${place} >= 0x77000000) & (${place} <= 0x7f000000)) { lmva place } } 
```

**1m** 选项与 " [**lm (List 已加载模块")**](lm--list-loaded-modules-.md)命令一起导致其输出只包含模块地址，而不包含模块的完整说明。

前面的示例使用 [**$ {} (Alias 解释器)**](-------alias-interpreter-.md) 标记，以确保即使在其他文本旁，也会替换别名。 如果该命令不包含此标记，则将 "下一步" 的左括号 **置于** "阻止替换别名"。 请注意， **$ {}** token 适用于在 **foreach** 和 true 别名中使用的变量。

## <a name="walking-the-process-list"></a>遍历进程列表

下面的示例演示内核模式进程列表，并显示列表中每个条目的可执行文件名称。

此示例应存储为文本文件，并使用 [**$$ &gt; &lt; (运行脚本文件)**](-----------------------a---run-script-file-.md)命令执行。 此命令将加载整个文件，并将所有回车返回替换为分号，并执行生成的块。 使用此命令，您可以通过使用多个行和缩进来编写可读程序，而无需将整个程序挤压到一行。

此示例演示了以下功能：

-   **$T 0**、 **$t 1** 和 **$t 2** 伪寄存器在此程序中用作变量。 该程序还使用名为 **Procc** 和 **$ImageName** 的别名。

-   此程序使用 MASM 表达式计算器。 不过， **@ @c + + ( )** 标记会出现一次。 此标记会使程序使用 c + + 表达式计算器来分析括号内的表达式。 此用法使程序能够直接使用 c + + 结构标记。

-   **?** 标志与 [**r (寄存器)**](r--registers-.md) 命令一起使用。 此标志将键入的值分配给伪寄存器 **$t 2**。

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

## <a name="walking-the-ldr_data_table_entry-list"></a>遍历 LDR \_ 数据表 \_ \_ 条目列表

下面的示例演示了用户模式 LDR 数据表 \_ \_ \_ 条目列表，并显示了每个列表项的基址和完整路径。

与前面的示例一样，此程序应保存在文件中，并使用 [**$$ &gt; &lt; (运行脚本文件)**](-----------------------a---run-script-file-.md)命令执行。

此示例演示了以下功能：

- 此程序使用 MASM 表达式计算器。 但在两个位置，将显示 **@ @c + + ( )** 标记。 此标记会使程序使用 c + + 表达式计算器来分析括号内的表达式。 此用法使程序能够直接使用 c + + 结构标记。

- **?** 标志与 [**r (寄存器)**](r--registers-.md) 命令一起使用。 此标志将键入的值分配给伪寄存器 **$t 0** 和 **$t 1**。 在循环的主体中， **$t 1** 的类型为 **ntdll.dll！ \_LDR \_ 数据表 \_ \_ 项 \\ ， \*** 因此程序可以进行直接成员引用。

- 此程序中使用了用户命名的别名 **$Base** 和 **$Mod** 。 美元符号降低了之前在当前调试器会话中使用这些别名的可能性。 美元符号并不是必需的。 [**$ {/V：}**](-------alias-interpreter-.md)标记按原义解释别名，以防在运行脚本之前定义别名。 你还可以将此标记与任何块一起使用，以防止在使用块之前使用别名定义。

- [**Block**](-block.md)标记用于添加额外的别名替换步骤。 加载整个脚本时，会对整个脚本执行别名替换，并在每个块进入时进行一次。 如果没有 **块** 标记及其大括号， **echo** 命令不会接收 **$Mod** 的值，并且 **$Base** 在前面的行中分配的别名。

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
 






