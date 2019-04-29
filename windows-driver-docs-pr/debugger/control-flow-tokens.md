---
title: 控制流标记
description: 控制流标记
ms.assetid: c38852aa-3dfe-4f70-9ef4-8c86e4a8334d
keywords:
- 脚本文件，控制流令牌
- 控制流令牌
- 调试器命令程序、 控制流令牌
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a52a84a2f0c1dd81b3955cbc7a268069b9fac6c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375036"
---
# <a name="control-flow-tokens"></a>控制流标记


## <span id="ddk_control_flow_tokens_dbg"></span><span id="DDK_CONTROL_FLOW_TOKENS_DBG"></span>


可以使用*控制流令牌*创建条件执行和执行循环内的调试器命令程序。

控制流令牌的行为类似于 C 中的对应项和C++，但以下常规例外：

-   即使只有一个此类命令，必须将每个命令块的大括号，有条件地或重复执行。 例如，不能省略以下命令中的大括号。

    ```dbgcmd
    0:000> .if (ebx>0) { r ebx }
    ```

-   每个条件必须是表达式。 不允许的命令。 例如，下面的示例生成语法错误。

    ```dbgcmd
    0:000> .while (r ebx) { .... }
    ```

-   最后一个命令之前不需要分号后跟一个右大括号。

调试器命令程序中支持以下控制流令牌。 有关每个标记的语法的详细信息，请参阅分立参考主题。

-   [ **.If** ](-if.md)令牌的行为类似于**如果**在 C 中的关键字

-   [ **.Else** ](-else.md)令牌的行为类似于**其他**在 C 中的关键字

-   [ **.Elsif** ](-elsif.md)令牌的行为类似于**的 else if**在 C 中的关键字组合

-   [ **.Foreach** ](-foreach.md)令牌分析的调试器命令、 字符串或文本文件输出。 然后，此令牌将每个项，它将找到并使用它们作为一系列指定的调试器命令的输入。

-   [ **。 有关**](-for.md)令牌的行为类似于**为**关键字在 C 中，不同之处在于必须用分号分隔，而不是逗号分隔多个增量命令。

-   [**管制**](-while.md)令牌的行为类似于**而**在 C 中的关键字

-   [**执行**](-do.md)令牌的行为类似于**执行**关键字在 C 中，只不过不能使用在条件前的在词"while"。

-   [ **.Break** ](https://msdn.microsoft.com/library/windows/hardware/ff556242)令牌的行为类似于**中断**在 C 中的关键字您可以使用此令牌中任何 **。 有关**， **.while**，或**执行**循环。

-   [ **.Continue** ](-continue.md)令牌的行为类似于**继续**在 C 中的关键字您可以使用此令牌中任何 **。 有关**， **.while**，或**执行**循环。

-   [ **.Catch** ](-catch.md)令牌可防止程序出错时结束。 **.Catch**标记后跟括号括起来的一个或多个命令。 如果其中一个命令将生成错误，会显示错误消息、 大括号内的所有其余命令将被忽略，和右大括号之后继续使用第一个命令的执行。

-   [ **.Leave** ](-leave.md)令牌用于退出 **.catch**块。

-   [ **.Printf** ](-printf.md)令牌的行为类似于**printf**在 C 中的语句

-   [ **.Block** ](-block.md)令牌不执行任何操作。 应使用此令牌仅用于引入一个块，因为不能仅通过对大括号之间创建一个块。 您必须添加左大括号前的控制流令牌。

[ **！ 有关\_每个\_模块**](-for-each-module.md)， [ **！ 为\_每个\_帧**](-for-each-frame.md)，和[ **！ 有关\_每个\_本地**](-for-each-local.md)扩展插件也是与调试器命令程序很有用。

 

 





