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
ms.openlocfilehash: 2f56ed9cb78424c87378336925439d4eda8a5168
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366399"
---
# <a name="scopes-and-symbol-groups"></a>范围和符号组


## <span id="ddk_scopes_and_symbol_groups_dbx"></span><span id="DDK_SCOPES_AND_SYMBOL_GROUPS_DBX"></span>


一个*符号组*包含一组作为一个组的有效操作的符号。 符号组可以创建并手动填充或可以自动生成和更新词法作用域，如本地变量和函数参数中的基于的符号。 接口[IDebugSymbolGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsymbolgroup)用于表示符号组。

有两种方法来创建符号组。 返回一个空符号组[ **CreateSymbolGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-createsymbolgroup)，并返回当前词法范围的符号组[ **GetScopeSymbolGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getscopesymbolgroup).

**请注意**  生成从当前作用域的符号组是本地变量的快照。 在目标中任何执行时，符号可能不再准确。 此外，如果当前范围内发生更改，符号组将无法再代表*当前*作用域 （因为它将继续表示为其创建的作用域）。

 

可以将符号添加到符号组使用[ **AddSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-addsymbol)，并使用删除[ **RemoveSymbolByIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyindex)或[ **RemoveSymbolByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-removesymbolbyname)。 该方法[ **OutputAsType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputastype)告知调试器处理符号的数据时使用的不同符号类型。

**请注意**  限定了作用域的符号的值可能不准确。 具体而言，计算机体系结构和编译器优化可能会阻止调试器准确地确定符号的值。

 

*符号条目信息*是一个符号，包括其位置以及其类型的说明。 若要在模块中查找符号此信息，请使用[ **IDebugSymbols3::GetSymbolEntryInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation)。 若要查找符号组中的一个符号此信息，请使用[ **IDebugSymbolGroup2::GetSymbolEntryInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolentryinformation)。 请参阅[**调试\_符号\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_symbol_entry)符号项信息的详细信息。

以下方法返回有关符号的信息符号组：

-   [**GetSymbolName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolname)返回符号的名称。

-   [**GetSymbolOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboloffset)返回的符号的目标的虚拟地址空间中的绝对地址，如果符号具有一个绝对地址。

-   [**GetSymbolRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolregister)返回包含的符号的寄存器，如果该符号包含在寄存器中。

-   [**GetSymbolSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolsize)返回的符号数据大小。

-   [**GetSymbolTypeName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymboltypename)返回符号的类型名称。

-   [**GetSymbolValueText** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolvaluetext)返回以字符串形式的符号的值。

如果在寄存器中或在调试器引擎已知的内存位置中存储一个符号，可以使用更改其值[ **WriteSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-writesymbol)。

符号是由*父符号*如果它包含其他符号。 例如，一种结构包含其成员。 符号是由*子符号*如果包含在另一个符号。 符号可能的父和子符号。 每个符号组具有平面的结构，并包含父符号和其子级。 每个符号*深度*--没有符号组中的父级的符号拥有的深度为零，并且每个子级符号的深度是一个大于其父级的深度。 子级的父符号可能会或可能不会显示符号组中。 符号组中存在子级时，父符号被称为*展开*。 若要添加或移除符号组中的符号的子级，请使用[ **ExpandSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-expandsymbol)。

返回的符号组中的符号的数量[ **GetNumberSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getnumbersymbols)。 *索引*符号在符号中的组是一个标识号; 索引范围是从零到减一的符号数。 每次添加或删除从符号组-例如，通过展开符号-符号的符号组中的所有符号索引可能会更改。

可以使用找到的符号参数，包括有关父-子关系的信息[ **GetSymbolParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-getsymbolparameters)。 此方法返回[**调试\_符号\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_symbol_parameters)结构。

符号组中的符号可以打印到调试器的输出流使用的方法[ **OutputSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbolgroup2-outputsymbols)。

### <a name="span-idscopesspanspan-idscopesspanscopes"></a><span id="scopes"></span><span id="SCOPES"></span>作用域

*当前作用域*，或*当前本地上下文*，确定由调试器引擎的本地变量。 该作用域具有三个组件：

1.  堆栈帧。

2.  当前的指令。

3.  寄存器上下文。

如果在调用堆栈顶部的堆栈帧，当前指令是导致的最后一个事件的指令。 否则当前指令是在函数调用，从而产生了下一步的更高堆栈帧。

方法[ **GetScope** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getscope)并[ **SetScope** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setscope)可用于获取和设置当前作用域。 事件发生时，当前作用域设置为事件的作用域。 当前作用域可以重置为最后一个事件使用的作用域[ **ResetScope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-resetscope)。

### <a name="span-idthread-contextspanspan-idthreadcontextspanthread-context"></a><span id="thread-context"></span><span id="THREAD_CONTEXT"></span>线程上下文

*线程上下文*是切换线程时，由 Windows 保留的状态。 它类似于寄存器上下文，只不过是寄存器上下文但不是线程上下文的一部分某些仅限内核的处理器状态。 在内核模式调试期间，此额外状态是可用寄存器。

由 ntddk.h 中定义的上下文结构表示的线程上下文。 此结构是依赖于平台的其解释依赖于有效的处理器类型。 方法[ **GetThreadContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-getthreadcontext)并[ **SetThreadContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-setthreadcontext)可用于获取和设置的线程上下文。

 

 





