---
title: 基本 AML 调试
description: 基本 AML 调试
ms.assetid: 2897abd4-7fef-4f9e-a4d8-10302d555fe4
keywords:
- AMLI 调试器，基本用法
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50b7c7a420aec9633ef368da3bf363b3aeca96eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357045"
---
# <a name="basic-aml-debugging"></a>基本 AML 调试


## <span id="ddk_basic_aml_debugging_dbg"></span><span id="DDK_BASIC_AML_DEBUGGING_DBG"></span>


AMLI 调试器支持两种类型的专用命令：*AMLI 调试器扩展*并*AMLI 调试器命令*。

执行 AML 调试时，应仔细区分两种不同的调试器命令窗口中将显示的提示：

-   当您看见**kd&gt;** 提示时，即控制内核调试程序。 所有标准内核调试器命令和扩展都可用。 此外，AMLI 调试器扩展插件也是可用的。 这些扩展的语法，请使用 **！ amli** *命令*。 AMLI 调试器命令不可用在此模式下。

-   当您看见**AMLI(? for help)-&gt;** 提示时，即控制 AMLI 调试器。 (当使用 WinDbg 时，此提示将出现在调试器命令窗口的顶部窗格和一个**输入&gt;** 提示符会在底部窗格中。)在此提示符下，可以输入任何 AMLI 调试器命令。 您还可以输入任何 AMLI 调试器扩展;这些扩展不应带有前缀 **！ amli**。 标准内核调试命令不可用在此模式下。

-   当您看到的根本无提示时，目标计算机运行。

在任何调试会话开始时，应设置 AMLI 调试器选项[ **！ amli 集**](-amli-set.md)扩展。 **Verboseon**， **traceon**，并**errbrkon**选项也是非常有用。 应考虑进行激活**spewon**选项。 请参阅详细信息的扩展引用页。

AMLI 调试器处于活动状态，有多种：

-   如果遇到 AML 代码中的断点，ACPI 将进入 AMLI 调试器。

-   如果 AML 代码内发生严重的错误或异常 (如**int 3**)，ACPI 将进入 AMLI 调试器。

-   如果**errbrkon**设置选项，任何 AML 错误将导致 ACPI AMLI 调试器中中断。

-   如果你想要故意中断 AMLI 调试器，使用[ **！ amli 调试器**](-amli-debugger.md)扩展，然后[ **g （转向）** ](g--go-.md)命令。 AMLI 调试器会取代任何 AML 代码执行由解释器，下一次。

当你在 AMLI 调试器提示符下，您可以键入**q**返回到内核调试程序或类型**g**继续正常执行。

以下扩展是对于 AML 调试特别有用：

-   [ **！ Amli dns** ](-amli-dns.md)扩展显示特定对象，从属于该对象的命名空间树或甚至整个命名空间树中的 ACPI 命名空间。 此命令是在确定什么特别有用的特定命名空间对象是-它是一种方法、 fieldunit、 一台设备或另一种类型的对象。

-   [ **！ Amli 查找**](-amli-find.md)扩展将任何命名空间对象的名称，并返回其完整路径。

-   [ **！ Amli u** ](-amli-u.md)扩展 unassembles AML 代码。

-   [ **！ Amli lc** ](-amli-lc.md)扩展显示有关所有活动的 ACPI 上下文的信息摘要。

-   [ **！ Amli r** ](-amli-r.md)扩展显示有关当前上下文的解释器的详细的信息。 时，此操作很有用 AMLI 调试器检测到错误后，会显示提示。

-   可以设置断点，并控制 AML 代码中。 使用[ **！ amli bp** ](-amli-bp.md)若要设置断点， [ **！ amli bc** ](-amli-bc.md)清除断点的行， [ **！ amli bd**](-amli-bd.md)禁用断点[ **！ amli 是**](-amli-be.md)若要重新启用断点，和[ **！ amli bl** ](-amli-bl.md)以列出所有断点。

-   AMLI 调试器都可以运行、 单步执行，并跟踪通过 AML 代码。 使用**运行**， **p**，并**t**命令来执行这些操作。

扩展和命令的完整列表，请参阅[使用 AMLI 调试器扩展](using-amli-debugger-extensions.md)并[使用 AMLI 调试器命令](using-amli-debugger-commands.md)。

## <a name="see-also"></a>请参阅

[AMLI 调试器](the-amli-debugger.md)
