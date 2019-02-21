---
title: 达到执行之前指定的状态
description: 达到执行之前指定的状态
ms.assetid: 0657a7bf-4d72-4248-9e45-d79d51b91139
keywords:
- 达到执行到指定的状态
- 断点，用于控制执行
- 断点以及伪寄存器
- 脚本文件，用于控制执行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b49c5dee6c4e08093349fc75ae19f3686104a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523128"
---
# <a name="executing-until-a-specified-state-is-reached"></a>达到执行之前指定的状态


## <span id="ddk_determining_the_acl_of_an_object_dbg"></span><span id="DDK_DETERMINING_THE_ACL_OF_AN_OBJECT_DBG"></span>


有几种方法会导致目标以执行，直到达到指定的状态。

### <a name="span-idusingabreakpointtocontrolexecutionspanspan-idusingabreakpointtocontrolexecutionspanusing-a-breakpoint-to-control-execution"></a><span id="using_a_breakpoint_to_control_execution"></span><span id="USING_A_BREAKPOINT_TO_CONTROL_EXECUTION"></span>使用控制执行断点

一种方法是使用断点。 程序计数器达到了指定的地址时，最简单的断点会暂停执行。 更复杂的断点可以：

-   仅当通过一个特定的线程，执行此地址时触发

-   之前触发，允许通过此地址指定的数目

-   触发后，将自动颁发指定的命令或

-   观看在内存中非可执行文件，读取或写入到内存时触发指定的地址。

有关如何设置和控制断点的详细信息，请参阅[使用断点](using-breakpoints.md)。

一种以执行，直到达到指定的状态的更复杂的方法是使用*条件断点*。 这种类型的断点设置在某个地址，但如果指定的条件有效，则仅触发。 有关详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

### <a name="span-idbreakpointsandpseudoregistersspanspan-idbreakpointsandpseudoregistersspanbreakpoints-and-pseudo-registers"></a><span id="breakpoints_and_pseudo_registers"></span><span id="BREAKPOINTS_AND_PSEUDO_REGISTERS"></span>断点和伪寄存器

在指定所需的状态，通常很有必要使用*自动伪寄存器*。 这些是由调试器控制可用于引用多种与目标状态相关的值的变量。

例如，使用下面的断点 **$thread**伪寄存器，也始终等于当前线程的值。 它解析为当前线程的值时在命令中使用。 通过使用 **$thread**作为参数的 **/t**参数[**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令时，可以创建将一个断点每次触发的**NtOpenFile**调用的线程的处于活动状态的时间向你发放**bp**命令：

```dbgcmd
kd> bp /t @$thread nt!ntopenfile
```

当其他任何线程调用时，此断点将不会触发**NtOpenFile**。

有关自动伪寄存器的列表，请参阅[伪寄存器语法](pseudo-register-syntax.md)。

### <a name="span-idusingascriptfiletocontrolexecutionspanspan-idusingascriptfiletocontrolexecutionspanusing-a-script-file-to-control-execution"></a><span id="using_a_script_file_to_control_execution"></span><span id="USING_A_SCRIPT_FILE_TO_CONTROL_EXECUTION"></span>使用脚本文件来控制执行

若要执行，直到达到指定的状态的另一种方法是创建调用其自身以递归方式，在每次迭代中测试所需的状态的脚本文件。

通常情况下，此脚本文件将包含[ **.if** ](-if.md)并[ **.else** ](-else.md)令牌。 您可以使用命令，如[ **t (Trace)** ](t--trace-.md)执行一个步骤中，，然后测试相关的条件。

例如，如果你想要才执行**eax**注册包含值 0x1234，可以创建一个名为的脚本文件*eaxstep* ，其中包含以下行：

```dbgcmd
.if (@eax == 1234) { .echo 1234 } .else { t "$<eaxstep" }
```

然后，发出从调试器命令窗口运行以下命令：

```dbgcmd
t "$<eaxstep"
```

这**t**命令将执行一个步骤中，并执行带引号的命令。 此命令只碰巧[  **$ &lt; （运行脚本文件）**](-----------------------a---run-script-file-.md)，哪些运行*eaxstep*文件。 脚本文件测试的值**eax**，在运行**t**命令，并调用其自身以递归方式。 这将继续，直至**eax**注册等于 0x1234，此时[ **.echo （Echo 注释）** ](-echo--echo-comment-.md)命令打印到调试器命令窗口中，并执行一条消息将停止。

脚本文件的详细信息，请参阅[使用脚本文件](using-script-files.md)并[使用调试器命令程序](using-debugger-command-programs.md)。

 

 





