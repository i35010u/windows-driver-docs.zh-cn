---
title: 范围和符号组
description: 范围和符号组
ms.assetid: f14b6361-9962-4fa3-bb1a-dfde066754b9
keywords:
- 调试器引擎 API，符号，符号组
- 符号组，范围
- 调试器引擎 API，符号，范围
- 作用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f1f96f9a37d258c9ded57e205d320dc186dc5bb
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242776"
---
# <a name="scopes-and-symbol-groups"></a>范围和符号组


## <span id="ddk_scopes_and_symbol_groups_dbx"></span><span id="DDK_SCOPES_AND_SYMBOL_GROUPS_DBX"></span>


*符号组*包含一组用于有效操作的符号，作为一个组。 可以手动创建和填充符号组，也可以基于词法范围中的符号（如局部变量和函数参数）自动生成和更新符号组。 Interface [IDebugSymbolGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbolgroup)用于表示符号组。

可以通过两种方法创建符号组。 空符号组由[**CreateSymbolGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-createsymbolgroup)返回，而当前词法范围的符号组由[**GetScopeSymbolGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getscopesymbolgroup)返回。

**请注意**   从当前作用域生成的符号组是本地变量的快照。 如果目标中发生了任何执行，则符号可能不再准确。 此外，如果当前范围发生更改，则符号组将不再表示*当前*范围（因为它将继续表示创建它的范围）。

 

可以使用[**AddSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-addsymbol)将符号添加到符号组，并使用[**RemoveSymbolByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyindex)或[**RemoveSymbolByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyname)将其删除。 方法[**OutputAsType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputastype)通知调试器在处理符号的数据时使用不同的符号类型。

**请注意**   范围符号的值可能不准确。 具体而言，计算机体系结构和编译器优化可能会阻止调试器准确确定符号的值。

 

*符号输入信息*是符号的说明，包括符号的位置和类型。 若要在模块中查找符号的此信息，请使用[**IDebugSymbols3：： GetSymbolEntryInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation)。 若要在符号组中查找符号的此信息，请使用[**IDebugSymbolGroup2：： GetSymbolEntryInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolentryinformation)。 有关符号输入信息的详细信息，请参阅[**调试\_符号\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_entry)。

以下方法返回有关符号组中符号的信息：

-   [**GetSymbolName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolname)返回符号的名称。

-   如果符号具有绝对地址，则[**GetSymbolOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboloffset)将返回该符号目标的虚拟地址空间中的绝对地址。

-   如果符号包含在寄存器中，则[**GetSymbolRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolregister)将返回包含符号的寄存器。

-   [**GetSymbolSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolsize)返回符号的数据大小。

-   [**GetSymbolTypeName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboltypename)返回符号类型的名称。

-   [**GetSymbolValueText**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolvaluetext)将符号值作为字符串返回。

如果符号存储在寄存器中或调试器引擎已知的内存位置，则可以使用[**WriteSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-writesymbol)更改其值。

如果符号包含其他符号，则该符号为*父符号*。 例如，结构包含其成员。 符号是包含在另一个符号中的*子符号*。 符号可以同时为父符号和子符号。 每个符号组都有一个平面结构，并包含父符号及其子级。 每个符号在符号组中有一个没有父级的*深度*符号，其深度为零，每个子符号的深度均大于其父符号的深度。 父符号的子级在符号组中可能存在，也可能不存在。 当符号组中存在子级时，父符号称为*展开*。 若要在符号组中添加或删除符号的子级，请使用[**ExpandSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-expandsymbol)。

[**GetNumberSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getnumbersymbols)返回符号组中的符号数。 符号组中符号的*索引*是标识号;索引的范围为从零到符号的数目减一。 每次在符号组中添加或删除符号时（例如，通过展开符号），符号组中所有符号的索引都可能会更改。

可以使用[**GetSymbolParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolparameters)找到符号参数（包括有关父子关系的信息）。 此方法返回[**调试\_符号\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_parameters)结构。

可以使用方法[**OutputSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputsymbols)将符号组中的符号打印到调试器的输出流。

### <a name="span-idscopesspanspan-idscopesspanscopes"></a><span id="scopes"></span><span id="SCOPES"></span>作用

*当前作用域*或*当前本地上下文*确定调试器引擎公开的局部变量。 作用域包含三个组件：

1.  堆栈帧。

2.  当前指令。

3.  注册上下文。

如果堆栈帧位于调用堆栈的顶部，则当前指令为导致最后一个事件的指令。 否则，当前指令为函数调用，导致下一个更高的堆栈帧。

[**GetScope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getscope)和[**SetScope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setscope)方法可用于获取和设置当前范围。 事件发生时，当前作用域设置为事件的作用域。 可以使用[**ResetScope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-resetscope)将当前作用域重置为最后一个事件的作用域。

### <a name="span-idthread-contextspanspan-idthread_contextspanthread-context"></a><span id="thread-context"></span><span id="THREAD_CONTEXT"></span>线程上下文

*线程上下文*是在切换线程时由 Windows 保留的状态。 这与寄存器上下文类似，只是某些仅限内核的处理器状态是寄存器上下文的一部分，而不是线程上下文。 在内核模式调试过程中，此额外状态作为寄存器提供。

线程上下文由 ntddk 中定义的上下文结构表示。 此结构依赖于平台，它的解释取决于有效的处理器类型。 [**GetThreadContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-getthreadcontext)和[**SetThreadContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-setthreadcontext)方法可用于获取和设置线程上下文。

 

 





