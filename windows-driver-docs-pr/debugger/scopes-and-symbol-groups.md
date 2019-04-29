---
title: 范围和符号组
description: 范围和符号组
ms.assetid: f14b6361-9962-4fa3-bb1a-dfde066754b9
keywords:
- 调试器引擎 API、 符号、 符号组
- 符号组中，作用域
- 调试器引擎 API、 符号、 作用域
- 作用域
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9937d4ccbf7a6472c935d116e1a94f255c0cc134
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382011"
---
# <a name="scopes-and-symbol-groups"></a>范围和符号组


## <span id="ddk_scopes_and_symbol_groups_dbx"></span><span id="DDK_SCOPES_AND_SYMBOL_GROUPS_DBX"></span>


一个*符号组*包含一组作为一个组的有效操作的符号。 符号组可以创建并手动填充或可以自动生成和更新词法作用域，如本地变量和函数参数中的基于的符号。 接口[IDebugSymbolGroup](https://msdn.microsoft.com/library/windows/hardware/ff550838)用于表示符号组。

有两种方法来创建符号组。 返回一个空符号组[ **CreateSymbolGroup**](https://msdn.microsoft.com/library/windows/hardware/ff540093)，并返回当前词法范围的符号组[ **GetScopeSymbolGroup**](https://msdn.microsoft.com/library/windows/hardware/ff548280).

**请注意**  生成从当前作用域的符号组是本地变量的快照。 在目标中任何执行时，符号可能不再准确。 此外，如果当前范围内发生更改，符号组将无法再代表*当前*作用域 （因为它将继续表示为其创建的作用域）。

 

可以将符号添加到符号组使用[ **AddSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff537925)，并使用删除[ **RemoveSymbolByIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff554510)或[ **RemoveSymbolByName**](https://msdn.microsoft.com/library/windows/hardware/ff554518)。 该方法[ **OutputAsType** ](https://msdn.microsoft.com/library/windows/hardware/ff553191)告知调试器处理符号的数据时使用的不同符号类型。

**请注意**  限定了作用域的符号的值可能不准确。 具体而言，计算机体系结构和编译器优化可能会阻止调试器准确地确定符号的值。

 

*符号条目信息*是一个符号，包括其位置以及其类型的说明。 若要在模块中查找符号此信息，请使用[ **IDebugSymbols3::GetSymbolEntryInformation**](https://msdn.microsoft.com/library/windows/hardware/ff548484)。 若要查找符号组中的一个符号此信息，请使用[ **IDebugSymbolGroup2::GetSymbolEntryInformation**](https://msdn.microsoft.com/library/windows/hardware/ff548487)。 请参阅[**调试\_符号\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff541662)符号项信息的详细信息。

以下方法返回有关符号的信息符号组：

-   [**GetSymbolName** ](https://msdn.microsoft.com/library/windows/hardware/ff549121)返回符号的名称。

-   [**GetSymbolOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff549135)返回的符号的目标的虚拟地址空间中的绝对地址，如果符号具有一个绝对地址。

-   [**GetSymbolRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff549165)返回包含的符号的寄存器，如果该符号包含在寄存器中。

-   [**GetSymbolSize** ](https://msdn.microsoft.com/library/windows/hardware/ff549169)返回的符号数据大小。

-   [**GetSymbolTypeName** ](https://msdn.microsoft.com/library/windows/hardware/ff549188)返回符号的类型名称。

-   [**GetSymbolValueText** ](https://msdn.microsoft.com/library/windows/hardware/ff549201)返回以字符串形式的符号的值。

如果在寄存器中或在调试器引擎已知的内存位置中存储一个符号，可以使用更改其值[ **WriteSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff561457)。

符号是由*父符号*如果它包含其他符号。 例如，一种结构包含其成员。 符号是由*子符号*如果包含在另一个符号。 符号可能的父和子符号。 每个符号组具有平面的结构，并包含父符号和其子级。 每个符号*深度*--没有符号组中的父级的符号拥有的深度为零，并且每个子级符号的深度是一个大于其父级的深度。 子级的父符号可能会或可能不会显示符号组中。 符号组中存在子级时，父符号被称为*展开*。 若要添加或移除符号组中的符号的子级，请使用[ **ExpandSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff543271)。

返回的符号组中的符号的数量[ **GetNumberSymbols**](https://msdn.microsoft.com/library/windows/hardware/ff547975)。 *索引*符号在符号中的组是一个标识号; 索引范围是从零到减一的符号数。 每次添加或删除从符号组-例如，通过展开符号-符号的符号组中的所有符号索引可能会更改。

可以使用找到的符号参数，包括有关父-子关系的信息[ **GetSymbolParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549146)。 此方法返回[**调试\_符号\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff541673)结构。

符号组中的符号可以打印到调试器的输出流使用的方法[ **OutputSymbols**](https://msdn.microsoft.com/library/windows/hardware/ff553264)。

### <a name="span-idscopesspanspan-idscopesspanscopes"></a><span id="scopes"></span><span id="SCOPES"></span>作用域

*当前作用域*，或*当前本地上下文*，确定由调试器引擎的本地变量。 该作用域具有三个组件：

1.  堆栈帧。

2.  当前的指令。

3.  寄存器上下文。

如果在调用堆栈顶部的堆栈帧，当前指令是导致的最后一个事件的指令。 否则当前指令是在函数调用，从而产生了下一步的更高堆栈帧。

方法[ **GetScope** ](https://msdn.microsoft.com/library/windows/hardware/ff548270)并[ **SetScope** ](https://msdn.microsoft.com/library/windows/hardware/ff556773)可用于获取和设置当前作用域。 事件发生时，当前作用域设置为事件的作用域。 当前作用域可以重置为最后一个事件使用的作用域[ **ResetScope**](https://msdn.microsoft.com/library/windows/hardware/ff554577)。

### <a name="span-idthread-contextspanspan-idthreadcontextspanthread-context"></a><span id="thread-context"></span><span id="THREAD_CONTEXT"></span>线程上下文

*线程上下文*是切换线程时，由 Windows 保留的状态。 它类似于寄存器上下文，只不过是寄存器上下文但不是线程上下文的一部分某些仅限内核的处理器状态。 在内核模式调试期间，此额外状态是可用寄存器。

由 ntddk.h 中定义的上下文结构表示的线程上下文。 此结构是依赖于平台的其解释依赖于有效的处理器类型。 方法[ **GetThreadContext** ](https://msdn.microsoft.com/library/windows/hardware/ff549291)并[ **SetThreadContext** ](https://msdn.microsoft.com/library/windows/hardware/ff556829)可用于获取和设置的线程上下文。

 

 





