---
title: 在 WinDbg 中查看和编辑全局变量
description: 在 WinDbg 中查看和编辑全局变量
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7f8e6cf10ca5dd7bc44544c3fc24e77104e7019
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802893"
---
# <a name="viewing-and-editing-global-variables-in-windbg"></a>在 WinDbg 中查看和编辑全局变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


调试器将全局变量的名称解释为虚拟地址。 因此，你可以使用 " [按虚拟地址访问内存](accessing-memory-by-virtual-address.md) " 中所述的所有命令来读取或写入全局变量。

此外，还可以使用 [**？ (计算 Expression)**](---evaluate-expression-.md) 命令来显示与任何符号关联的地址。

在 WinDbg 中，还可以使用监视窗口显示和更改全局变量和局部变量。 监视窗口可以显示所需的任何变量列表。 这些变量可以包含来自任何函数的全局变量和局部变量。 在任何时候，监视窗口都将显示与当前函数的作用域匹配的那些变量的值。 还可以通过监视窗口更改这些变量的值。

若要打开监视窗口，请从 "**视图**" 菜单中选择 "**监视**"。 还可以按 ALT + 2，或单击工具栏上 **的 "监视** " 按钮： ![ "监视" 按钮的屏幕截图 ](images/tbwatch.png) 。 ALT + SHIFT + 2 关闭监视窗口。

下面的屏幕截图显示了一个监视窗口的示例。

!["监视" 窗口的屏幕截图 ](images/window-watch.png)

监视窗口可以包含四列。 " **名称** " 和 " **值** " 列始终显示，" **类型** " 和 " **位置** " 列是可选的。 若要显示 " **类型** " 和 " **位置** " 列，请分别单击工具栏上的 " **转换** " 和 " **位置** " 按钮。

 

 





