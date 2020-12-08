---
title: 控制流标记
description: 控制流标记
keywords:
- 脚本文件，控制流标记
- 控制流标记
- 调试器命令程序，控制流标记
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28460a0d24dd51584f04a8d1708a4a94a3ffd283
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809721"
---
# <a name="control-flow-tokens"></a>控制流标记


## <span id="ddk_control_flow_tokens_dbg"></span><span id="DDK_CONTROL_FLOW_TOKENS_DBG"></span>


可以使用 *控制流令牌* 在调试器命令程序中创建条件执行和执行循环。

控制流令牌的行为类似于 C 和 c + + 中的对应项，但有以下一般例外：

-   必须将每个命令块括在大括号中执行或重复执行，即使只有一个这样的命令。 例如，在下面的命令中不能省略大括号。

    ```dbgcmd
    0:000> .if (ebx>0) { r ebx }
    ```

-   每个条件都必须是一个表达式。 不允许使用命令。 例如，下面的示例生成语法错误。

    ```dbgcmd
    0:000> .while (r ebx) { .... }
    ```

-   右大括号前的最后一个命令无需后跟分号。

调试器命令程序中支持以下控制流标记。 有关每个标记的语法的详细信息，请参阅各个参考主题。

-   如果标记在 C 中的行为类似于 **if** 关键字，则为 [**。**](-if.md)

-   [**Else**](-else.md)标记在 C 中的行为类似于 **else** 关键字。

-   在 C 中， [**elsif**](-elsif.md) 标记的行为类似于 **else if** 关键字。

-   [**Foreach**](-foreach.md)标记分析调试器命令、字符串或文本文件的输出。 然后，此令牌将获取找到的每个项，并将其用作指定的调试器命令列表的输入。

-   的 [**. for**](-for.md) 标记的行为类似于 C 中的 **for** 关键字，只不过你必须用分号（而不是逗号）分隔多个增量命令。

-   [**While**](-while.md)标记的行为类似于 C 中的 **while** 关键字。

-   在 C 中， [**do**](-do.md) 标记的行为类似于 **do** 关键字，只是在条件前不能使用单词 "while"。

-   [**Break**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)标记在 C 中的行为类似于 **break** 关键字。可以在任何中使用此标记 **。用于**、 **. while** 或 **. do** 循环。

-   在 C 中，continue 标记的行为与 **continue** 关键字相同 [**。**](-continue.md)可以在任何中使用此标记 **。用于**、 **. while** 或 **. do** 循环。

-   如果发生错误， [**catch**](-catch.md) 标记会阻止程序结束。 **Catch** 标记后跟包含一个或多个命令的大括号。 如果其中一条命令生成错误，则会显示错误消息，并且将忽略大括号内的所有剩余命令，并使用右大括号后面的第一个命令继续执行。

-   [**Leave**](-leave.md)标记用于退出 **catch** 块。

-   [**Printf**](-printf.md)标记的行为类似于 C 中的 **printf** 语句。

-   [**Block**](-block.md)标记不执行任何操作。 只应将此标记用于引入块，因为不能仅使用一对大括号创建块。 必须在左大括号前添加一个控制流标记。

对于每个模块，！对于每个 [**\_ \_ 模块**](-for-each-module.md)，每个的！; 对于每个 [**\_ \_ 本地**](-for-each-local.md)扩展，还可以使用调试器命令程序。 [**\_ \_**](-for-each-frame.md)

 

