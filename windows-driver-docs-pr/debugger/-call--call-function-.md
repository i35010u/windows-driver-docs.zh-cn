---
title: .call（调用函数）
description: Call 命令导致目标进程执行某个函数。
keywords:
- 。调用 (调用函数) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .call (Call Function)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c1195fda6d4cbf3aeb701d90e15616726721648
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814107"
---
# <a name="call-call-function"></a>.call（调用函数）


**Call** 命令导致目标进程执行某个函数。

```dbgsyntax
.call [/v] Function( Arguments ) 
.call /s Prototype Function( Arguments ) 
.call /c 
.call /C 
```

## <a name="span-idddk_meta_call_function_dbgspanspan-idddk_meta_call_function_dbgspanparameters"></a><span id="ddk_meta_call_function_dbg"></span><span id="DDK_META_CALL_FUNCTION_DBG"></span>参数


<span id="________v______"></span><span id="________V______"></span>**/v**   
将显示有关调用及其参数的详细信息。

<span id="________s________Prototype______"></span><span id="________s________prototype______"></span><span id="________S________PROTOTYPE______"></span>**/S** *原型*   
允许调用 *函数* 指定的函数，即使您没有正确的符号。 在这种情况下，必须具有与尝试调用的函数具有相同调用原型的另一个函数的符号。 *Prototype* 参数是此原型函数的名称。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span>*函数*   
指定正在调用的函数。 这可以是函数的名称， (最好使用模块名称进行限定，) 或者计算结果为函数地址的任何其他表达式。 如果需要调用构造函数或析构函数，则必须提供地址--或使用 c + + 表达式来计算运算符的命名语法 (参阅 [数值表达式语法](numerical-expression-syntax.md) 获取详细信息) 。

<span id="_______Arguments______"></span><span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span>*参数*   
指定传递给函数的参数。 如果调用的是方法，则第一个参数必须是 **此** 参数，并且所有其他参数跟在其后。 参数应用逗号分隔，并且应与常规参数语法匹配。 支持可变长度参数列表。 C + + 表达式计算器分析参数中的表达式;有关详细信息，请参阅 [c + + 编号和运算符](c---numbers-and-operators.md) 。 不能输入文本字符串作为参数，但可以使用指向字符串的指针或目标进程可访问的任何其他内存。

<span id="________c______"></span><span id="________C______"></span>**/c**   
清除当前线程上的任何现有调用。

<span id="________C______"></span><span id="________c______"></span>**/C**   
清除当前线程上的任何现有调用，并将当前线程的上下文重置为未完成调用所存储的上下文。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅限 x86 和 x64</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当前进程的当前线程调用指定的函数。

仅支持 **cdecl**、 **stdcall**、 **fastcall** 和 **thiscall** 调用约定。 此命令不能调用托管代码。

在 **调用** 后，调试器将更新堆栈，将指令指针更改为指向被调用函数的开头，然后停止。 使用 [**g (中转)**](g--go-.md) 继续执行，或使用 **~. g** 只执行发出调用的线程。

当函数返回时，将发生中断并且调试器显示函数的返回值。 返回值也存储在 **$callret** 伪寄存器中，后者获取返回值的类型。

如果使用 CTRL + C 或 CTRL + BREAK 将目标分成目标，则当前线程会创建一个额外的线程来处理 breakin。 如果在此时发出一个 **call** 命令，则会将额外线程用于被调用函数。

如果已达到预定义的断点，则没有额外的 breakin 线程。 如果在用户模式下，在断点处使用 **. call** ，则可以使用 [**g**](g--go-.md) 执行整个进程，或使用 **~. g** 仅执行当前线程。 使用 **g** 可能会导致程序的行为失真，因为你已拍摄一个线程并将其转移到此新函数。 另一方面，此线程仍将具有其锁和其他属性，因此 **~. g** 可能会导致风险死锁。

最安全的使用方法 **。调用** 是在代码中的某个位置设置断点，可以安全地调用某个函数。 命中该断点时，如果希望运行该函数，则可以使用 **。** 如果使用，则在通常无法调用此函数的点上 **调用** 时，可能会导致死锁或目标损坏。

将额外函数添加到不由现有代码调用的源代码，但要由调试器调用，这可能会很有用。 例如，你可以添加用于调查代码的当前状态及其环境的函数，并将有关状态的信息存储在已知的内存位置。 请确保不要优化代码，否则编译器可能会删除这些函数。 仅将此方法用作最后的手段，因为如果应用程序发生崩溃，则在调试转储文件时调用将不可用 **。**

仅当尝试使用时，才应使用 **call/c** 和 **. call/c** 命令。 **调用** 失败，或者如果你在输入 [**g**](g--go-.md) 命令之前更改了主意。 不应随意使用这些类，因为放弃未完成的调用可能会导致目标状态损坏。

下面的代码示例演示如何使用 **调用/s** 命令。

```dbgcmd
.call /s KnownFunction UnknownFunction( 1 )
```

在此示例中，你具有 **KnownFunction** 的私有符号，该符号采用整数作为其唯一参数并返回，例如，指向数组的指针。 你没有符号，或者可能只有 **UnknownFunction** 的公共符号，但你知道它只使用整数作为参数，并返回指向数组的指针。 通过使用 **/s** 选项，可以指定 **UnknownFunction** 的工作方式与 **KnownFunction** 的工作方式相同。 因此，你可以成功地生成对 **UnknownFunction** 的调用。

 

 





