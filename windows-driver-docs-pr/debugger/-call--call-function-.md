---
title: .call （调用函数）
description: .Call 命令会使目标进程执行函数。
ms.assetid: 93265c2a-ea4d-4523-928c-1bb75a9356b1
keywords:
- .call （调用函数） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .call (Call Function)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a4d7edfab7998d62d2696b5d351264cbfeb37f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521897"
---
# <a name="call-call-function"></a>.call （调用函数）


**.Call**命令将导致目标过程执行函数。

```dbgsyntax
.call [/v] Function( Arguments ) 
.call /s Prototype Function( Arguments ) 
.call /c 
.call /C 
```

## <a name="span-idddkmetacallfunctiondbgspanspan-idddkmetacallfunctiondbgspanparameters"></a><span id="ddk_meta_call_function_dbg"></span><span id="DDK_META_CALL_FUNCTION_DBG"></span>参数


<span id="________v______"></span><span id="________V______"></span> **/v**   
显示有关调用和其参数的详细信息。

<span id="________s________Prototype______"></span><span id="________s________prototype______"></span><span id="________S________PROTOTYPE______"></span> **/s** *Prototype*   
可以调用指定的函数*函数*即使您没有正确的符号。 在这种情况下，您必须具有与要调用的函数调用原型的相同的另一个函数的符号。 *原型*参数是此原型函数的名称。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span> *函数*   
指定要调用的函数。 这可以是 （最好是用模块名称限定），该函数或任何其他表达式的计算结果为函数地址的名称。 如果你需要调用构造函数或析构函数，必须提供该地址也可以使用 c + + 表达式评估命名的语法的运算符 (请参阅[数值表达式语法](numerical-expression-syntax.md)有关详细信息)。

<span id="_______Arguments______"></span><span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> *自变量*   
指定传递给函数的参数。 如果正在调用的方法，第一个参数必须是**这**，并且所有其他参数遵循它。 参数应该用逗号分隔，并且应与匹配的常用参数语法。 支持的长度可变的参数列表。 由 c + + 表达式计算器; 中参数的表达式进行分析请参阅[c + + 数字和运算符](c---numbers-and-operators.md)有关详细信息。 不能输入文本字符串作为参数，但可以使用一个字符串或其他任何可以访问目标进程内存的指针。

<span id="________c______"></span><span id="________C______"></span> **/c**   
清除当前线程上的任何现有调用。

<span id="________C______"></span><span id="________c______"></span> **/C**   
清除当前线程上的任何现有调用并将当前线程的上下文重置为存储的未处理调用的上下文。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>x86 和仅限 x64</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定的函数调用由当前线程的当前进程中。

仅**cdecl**， **stdcall**， **fastcall**，以及**thiscall**支持调用约定。 不能通过此命令调用托管的代码。

之后 **.call**是使用，调试器将更新堆栈，、 更改指令指针以指向被调用函数的开头，然后停止。 使用[ **g （转向）** ](g--go-.md)若要继续执行，或 **~。 g**执行调用线程。

当函数返回时，发生中断，调试器将显示该函数的返回值。 返回值也存储在 **$callret**伪寄存器，将获取返回值的类型。

如果在已中断到目标中，使用 CTRL + C 或 CTRL + BREAK，当前线程是创建用于处理 breakin 一个其他线程。 如果发出 **.call**此时，命令将被调用函数使用额外的线程。

如果你已达到预定义的断点，则没有额外的 breakin 线程。 如果您使用 **.call**同时在用户模式下一个断点，可以使用[ **g** ](g--go-.md)执行整个过程中，或 **~。 g**执行只需当前线程。 使用**g**可能误报应用程序的行为，因为拍摄一个线程并转移到此新函数。 但是，此线程仍将其锁和其他属性，从而 **~。 g**可能会有死锁风险。

若要使用的最安全方式 **.call**是在代码中设置断点，在其中可以安全地调用某函数的位置。 当到达该断点时，可以使用 **.call**如果你需要运行该函数。 如果您使用 **.call**可能会在其中调用此函数可能不正常点，导致死锁或目标的损坏。

可能需要将额外的函数添加到源代码不调用通过现有代码中，但旨在由调试器调用。 例如，可以添加用于调查你的代码和其环境的当前状态并将状态信息存储在已知的内存位置的函数。 确保不要将优化你的代码，或这些函数可能会删除由编译器。 作为最后的手段，仅使用此方法，因为如果你的应用程序崩溃 **.call**调试转储文件时将不可用。

**.Call /c**并 **.call /C**应仅使用命令，如果尝试使用 **.call**失败，或者如果您进入前改变了主意[ **g** ](g--go-.md)命令。 这些不应使用偶然，因为后，将放弃未完成的调用可能会导致损坏的目标状态。

下面的代码示例演示如何 **.call /s**使用命令。

```dbgcmd
.call /s KnownFunction UnknownFunction( 1 )
```

在此示例中，有私有符号**KnownFunction**，其中将一个整数作为其唯一参数并返回，例如，指向数组的指针。 没有符号，或者可能仅有公共符号**UnknownFunction**，但您知道它采用整数作为其唯一参数并返回指向数组的指针。 通过使用 **/s**选项，可以指定**UnknownFunction**同样有效的方式**KnownFunction** does。 因此，您可以成功生成调用**UnknownFunction**。

 

 





