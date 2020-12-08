---
title: 基本 AML 调试
description: 基本 AML 调试
keywords:
- AMLI 调试器，基本用法
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: f7dc87a7b7def3cae1fcef4faba36ec054f90e02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819283"
---
# <a name="basic-aml-debugging"></a>基本 AML 调试


## <span id="ddk_basic_aml_debugging_dbg"></span><span id="DDK_BASIC_AML_DEBUGGING_DBG"></span>


AMLI 调试器支持两种类型的专用命令： *AMLI 调试器扩展* 和 *AMLI 调试器命令*。

执行 AML 调试时，应仔细区分会出现在调试器命令窗口的两种不同类型的提示：

-   当你看到 **kd &gt;** 提示符时，你将控制内核调试器。 所有标准内核调试器命令和扩展都可用。 此外，还提供了 AMLI 调试器扩展。 这些扩展的语法为 **！ amli** *命令*。 在此模式下，AMLI 调试器命令不可用。

-   当你看到 " **AMLI (？" 帮助) &gt;** 提示时，你正在控制 AMLI 调试器。  (在使用 WinDbg 时，此提示将显示在调试器命令窗口的顶部窗格中，并将在底部窗格中显示 **输入 &gt;** 提示 ) 。在此提示符下，可以输入任何 AMLI 调试器命令。 还可以输入任何 AMLI 调试器扩展;这些扩展不应以 **！ amli** 为前缀。 此模式下不提供标准内核调试命令。

-   如果根本看不到任何提示，则目标计算机将运行。

在任意调试会话开始时，应设置 AMLI 调试器选项和 [**！ AMLI set**](-amli-set.md) extension。 **Verboseon**、 **traceon** 和 **errbrkon** 选项也非常有用。 应考虑激活 **spewon** 选项。 有关详细信息，请参阅扩展参考页。

AMLI 调试器可通过多种方法激活：

-   如果遇到 AML 代码中的断点，ACPI 将中断 AMLI 调试器。

-   如果 AML 代码中出现严重错误或异常 (如 **int 3**) ，ACPI 将中断 AMLI 调试器。

-   如果已设置 **errbrkon** 选项，则任何 AML 错误都将导致 ACPI 进入 AMLI 调试器。

-   如果要有意中断 AMLI 调试器，请使用 [**！ AMLI 调试程序**](-amli-debugger.md) 扩展，然后使用 [**g (中转)**](g--go-.md) 命令。 下一次解释器执行任何 AML 代码时，AMLI 调试器会接管。

在 AMLI 调试器提示符下，可以键入 **q** 返回到内核调试器，或键入 **g** 以恢复正常执行。

以下扩展对于 AML 调试特别有用：

-   [**！ Amli dns**](-amli-dns.md)扩展显示特定对象的 ACPI 命名空间、该对象的从属命名空间树，甚至整个命名空间树。 此命令在确定特定的命名空间对象是什么时特别有用，无论该对象是方法、fieldunit、设备还是其他类型的对象。

-   [**！ Amli find**](-amli-find.md) extension 使用任意命名空间对象的名称，并返回其完整路径。

-   [**！ Amli u**](-amli-u.md)扩展 unassembles AML 代码。

-   [**！ Amli lc**](-amli-lc.md)扩展显示有关所有活动 ACPI 上下文的简短信息。

-   [**！ Amli r**](-amli-r.md)扩展显示有关解释器当前上下文的详细信息。 如果在检测到错误后出现 AMLI 调试器提示，这会很有用。

-   可以在 AML 代码中设置和控制断点。 使用 [**！ amli bp**](-amli-bp.md) 设置断点，使用 [**！ amli bc**](-amli-bc.md) 来清除断点，！ [**amli bd**](-amli-bd.md) 禁用断点， [**！ amli**](-amli-be.md) 重新启用断点，使用 [**！ amli bl**](-amli-bl.md) 列出所有断点。

-   AMLI 调试器能够通过 AML 代码运行、单步执行和跟踪。 使用 **run**、 **p** 和 **t** 命令来执行这些操作。

有关扩展和命令的完整列表，请参阅 [使用 AMLI 调试器扩展](using-amli-debugger-extensions.md) 和 [使用 AMLI 调试器命令](using-amli-debugger-commands.md)。

## <a name="see-also"></a>另请参阅

[AMLI 调试器](the-amli-debugger.md)
