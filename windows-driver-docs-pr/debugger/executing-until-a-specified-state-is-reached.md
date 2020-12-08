---
title: 一直执行到出现指定的状态为止
description: 一直执行到出现指定的状态为止
keywords:
- 在达到指定状态之前执行
- 用于控制执行的断点
- 断点和伪寄存器
- 用于控制执行的脚本文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49a1abdd355875f6fccaae6ae8d1eb94a393beee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838219"
---
# <a name="executing-until-a-specified-state-is-reached"></a>一直执行到出现指定的状态为止


## <span id="ddk_determining_the_acl_of_an_object_dbg"></span><span id="DDK_DETERMINING_THE_ACL_OF_AN_OBJECT_DBG"></span>


在达到指定的状态之前，有几种方法可以使目标执行。

### <a name="span-idusing_a_breakpoint_to_control_executionspanspan-idusing_a_breakpoint_to_control_executionspanusing-a-breakpoint-to-control-execution"></a><span id="using_a_breakpoint_to_control_execution"></span><span id="USING_A_BREAKPOINT_TO_CONTROL_EXECUTION"></span>使用断点控制执行

一种方法是使用断点。 最简单的断点会在程序计数器到达指定地址时暂停执行。 更复杂的断点可以：

-   仅当特定线程执行此地址时才触发。

-   在触发之前，允许通过此地址经过指定数量的传递

-   在触发时自动发出指定的命令，或

-   在无法执行的内存中监视指定的地址，当读取或写入该内存时，将触发该地址。

有关如何设置和控制断点的详细信息，请参阅 [使用断点](using-breakpoints.md)。

在达到指定状态之前执行更复杂的方法是使用 *条件断点*。 此类断点在特定地址设置，但仅当指定的条件保留时才触发。 有关详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

### <a name="span-idbreakpoints_and_pseudo_registersspanspan-idbreakpoints_and_pseudo_registersspanbreakpoints-and-pseudo-registers"></a><span id="breakpoints_and_pseudo_registers"></span><span id="BREAKPOINTS_AND_PSEUDO_REGISTERS"></span>断点和 Pseudo-Registers

在指定所需状态时，使用 *自动伪寄存器* 通常会很有帮助。 这些是由调试器控制的变量，使用这些变量可以引用与目标状态相关的各种值。

例如，下面的断点使用 **$thread** 伪寄存器，该寄存器始终等于当前线程的值。 它在命令中使用时解析为当前线程的值。 通过将 **$thread** 用作 [**Bp (Set 断点**](bp--bu--bm--set-breakpoint-.md)的 **/t** 参数的参数) 命令，你可以创建一个断点，该断点将在每次调用 **NtOpenFile** 时，在发出 **bp** 命令时处于活动状态的线程调用：

```dbgcmd
kd> bp /t @$thread nt!ntopenfile
```

当其他任何线程调用 **NtOpenFile** 时，不会触发此断点。

有关自动伪寄存器的列表，请参阅 [伪寄存器语法](pseudo-register-syntax.md)。

### <a name="span-idusing_a_script_file_to_control_executionspanspan-idusing_a_script_file_to_control_executionspanusing-a-script-file-to-control-execution"></a><span id="using_a_script_file_to_control_execution"></span><span id="USING_A_SCRIPT_FILE_TO_CONTROL_EXECUTION"></span>使用脚本文件控制执行

在达到指定状态之前执行的另一种方法是创建一个以递归方式调用自身的脚本文件，并在每次迭代中测试所需状态。

通常，此脚本文件将包含 [**. if**](-if.md) 和 [**. else**](-else.md) 标记。 您可以使用命令（如 [**t (Trace)**](t--trace-.md) 执行单个步骤，然后测试相关的条件。

例如，如果你想要在 **eax** 注册包含值0x1234 之前执行，则可以创建一个名为 *eaxstep* 的脚本文件，其中包含以下行：

```dbgcmd
.if (@eax == 1234) { .echo 1234 } .else { t "$<eaxstep" }
```

然后从调试器命令窗口发出以下命令：

```dbgcmd
t "$<eaxstep"
```

此 **t** 命令将执行单个步骤，然后执行带引号的命令。 此命令 [**$ &lt; (运行脚本文件) 运行**](-----------------------a---run-script-file-.md) *eaxstep* 文件。 脚本文件测试 **eax** 的值，运行 **t** 命令，然后以递归方式调用自身。 此操作将继续，直到 **eax** 寄存器等于0x1234， (此时， [**)**](-echo--echo-comment-.md) 命令会将消息输出到调试器命令窗口，并停止执行。

有关脚本文件的详细信息，请参阅 [使用脚本文件](using-script-files.md) 和 [使用调试器命令程序](using-debugger-command-programs.md)。

 

 





