---
title: 查看和编辑在 WinDbg 中的全局变量
description: 查看和编辑在 WinDbg 中的全局变量
ms.assetid: 4273F6D8-A2A1-43FA-80BF-97E5673FAF05
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a559fb816042a272e0430f58ec02c96828799448
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520111"
---
# <a name="viewing-and-editing-global-variables-in-windbg"></a>查看和编辑在 WinDbg 中的全局变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


调试器将解释为一个虚拟地址的全局变量的名称。 因此，可以使用的所有命令中所述[访问内存的虚拟地址](accessing-memory-by-virtual-address.md)读取或写入全局变量。

此外，还可以使用[ **？（计算表达式）** ](---evaluate-expression-.md)命令以显示与任何符号相关联的地址。

在 WinDbg 中，您还可以使用监视窗口可显示和更改全局和本地变量。 监视窗口可以显示任何所需的变量的列表。 这些变量可以包含全局变量和局部变量从任何函数。 在任何时候，监视窗口显示与当前函数的作用域匹配这些变量的值。 此外可以更改通过监视窗口的这些变量的值。

若要打开监视窗口，请选择**Watch**从**视图**菜单。 此外可以按 ALT + 2，或单击**Watch**工具栏上的按钮：![监视按钮的屏幕截图](images/tbwatch.png)。 ALT + SHIFT + 2 将关闭监视窗口。

下面的屏幕截图显示了监视窗口的示例。

![监视窗口的屏幕截图 ](images/window-watch.png)

监视窗口可以包含四个列。 **名称**并**值**始终显示列，并**类型**并**位置**列是可选的。 若要显示**类型**并**位置**列，单击**Typecast**并**位置**按钮，分别在工具栏上。

 

 





