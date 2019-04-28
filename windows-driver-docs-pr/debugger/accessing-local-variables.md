---
title: 访问局部变量
description: 访问局部变量
ms.assetid: 0aab3fdf-fe0c-46ad-aa2f-90992811b001
keywords:
- 本地变量访问
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 505ee2fd9b253aa145410ce4c101ee2b41cce713
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351518"
---
# <a name="accessing-local-variables"></a>访问局部变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


本地变量，类似于全局变量，存储在符号文件。 和与全局变量，调试器会解释其名称作为地址。 它们可以读取和写入与全局变量相同的方式。 但是，如果你需要向符号是本地命令指示前, 加上美元符号 （$） 和符号感叹号 （！ )，如`$!var`。

Visual Studio 和 WinDbg 提供可以使用 （除了命令） 来查看和编辑本地变量的用户界面元素。 有关详细信息，请参阅[查看和编辑内存和 Visual Studio 中的寄存器](viewing-memory--variables--and-registers-in-visual-studio.md)并[查看和编辑在 WinDbg 中的本地变量](locals-window.md)。

此外可以使用以下方法来显示、 更改和使用本地变量：

-   [ **Dv （显示本地变量）** ](dv--display-local-variables-.md)命令显示的名称和值的所有本地变量。

-   [ **！ 有关\_每个\_本地**](-for-each-local.md)扩展使您能够执行单个命令重复一次为每个本地变量。

但是，没有本地和全局变量的一个主要区别。 应用程序是在执行时，本地变量的含义取决于位置的程序计数器，因为此类变量的作用域仅扩展到在其中定义的函数。

调试器会根据本地变量解释[本地上下文](changing-contexts.md#local-context)。 默认情况下，此上下文匹配的程序计数器的位置。 但在调试器可以更改上下文。 有关本地上下文的详细信息，请参阅本地上下文。

当本地上下文更改时，局部变量窗口是立即更新以反映新的本地变量的集合。 [ **Dv** ](dv--display-local-variables-.md)命令还会显示新变量。 所有这些变量的名称然后正确解释通过前面所述的内存命令。 然后，你可以读取或写入到这些变量。

 

 





