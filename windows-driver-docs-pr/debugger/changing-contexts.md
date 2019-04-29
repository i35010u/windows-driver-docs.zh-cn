---
title: 更改上下文
description: 更改上下文
ms.assetid: 3690903c-4281-4c65-98b0-00ca22206168
keywords:
- 上下文
- 登录会话上下文
- 上下文中，会话上下文
- 会话、 上下文
- 用户会话
- 会话
ms.date: 08/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6492c81235a35617a06c52dc8d7982d0789b99c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376100"
---
# <a name="changing-contexts"></a>更改上下文


## <span id="ddk-changing-contexts_dbg"></span><span id="DDK_CHANGING_CONTEXTS_DBG"></span>


在内核模式调试，有很多进程、 线程和有时在同一时间执行的用户会话。 因此，短语如"虚拟地址 0x80002000"或" **eax**注册"不明确。 必须指定*上下文*中此类短语可以理解。

调试器已在进行调试时可以设置五个不同的上下文：

1.  会话上下文指示默认用户会话。 

2.  进程上下文确定调试器如何解释虚拟地址。

3.  *用户模式地址上下文*几乎从不直接设置。 当您更改进程上下文时，将自动设置此上下文中。

4.  寄存器上下文确定调试器如何解释寄存器和堆栈跟踪的结果还可以控制。 此上下文是也称为*线程上下文*，尽管该术语不是完全准确。 *显式上下文*也是寄存器上下文的类型。 如果指定显式上下文，而不是当前寄存器上下文使用该上下文。

5.  本地上下文确定调试器如何解释本地变量。 此上下文是也称为*作用域*。

### <a name="span-idsession-contextspanspan-idsessioncontextspansession-context"></a><span id="session-context"></span><span id="SESSION_CONTEXT"></span>会话上下文

多个登录会话可以在同一时间运行。 每个登录会话具有其自己的进程。

[ **！ 会话**](-session.md)扩展显示所有登录会话或更改当前会话上下文。

通过使用的会话上下文[ **！ sprocess** ](-sprocess.md)并[ **！ spoolused** ](https://msdn.microsoft.com/library/windows/hardware/ff565361)扩展时会话数"-2"作为输入。

会话上下文更改时，进程上下文自动更改为活动的进程为该会话。

### <a name="span-idprocess-contextspanspan-idprocesscontextspanprocess-context"></a><span id="process-context"></span><span id="PROCESS_CONTEXT"></span>进程上下文

每个进程具有其自己的页面目录，用于记录如何虚拟地址映射到物理地址。 进程内的任何线程执行时，Windows 操作系统将使用此页目录来解释虚拟地址。

用户模式下在调试期间，当前进程确定进程上下文。 在调试器命令、 扩展和调试信息 windows 解释使用当前进程的页目录中使用的虚拟地址。

在内核模式调试中，过程中，您可以设置进程上下文通过使用[ **.process （设置进程上下文）** ](-process--set-process-context-.md)命令。 使用此命令选择哪个进程页目录用于解释虚拟地址。 设置进程上下文后，可以在任何命令中采用地址中使用此上下文。 你可以在此地址甚至设置断点。 通过包括 **/i**选项 **.process**命令来指定侵入性调试，还可以使用内核调试程序在用户空间中设置断点。

此外可以通过内核空间函数上使用特定于进程的断点，从内核调试器中设置用户模式断点。 设置战略断点并等待要提出的相应上下文。

*用户模式地址上下文*是进程上下文的一部分。 通常情况下，不需要直接设置的用户模式地址上下文。 如果将进程上下文，用户模式地址上下文将自动更改为的进程的相关页表目录基础。 

当在内核模式调试过程中设置进程上下文时，该进程上下文将保留，直到另一个 **.process**命令将更改的上下文。 之前，还会保留用户模式地址上下文 **.process**或 **.context**命令更改它。 当目标计算机执行，并不受对寄存器上下文或本地上下文的更改不会更改这些上下文。

### <a name="span-idregister-contextspanspan-idregistercontextspanregister-context"></a><span id="register-context"></span><span id="REGISTER_CONTEXT"></span>注册上下文

每个线程都具有其自己的注册值。 这些值是在线程正在执行时存储在 CPU 寄存器和另一个线程正在执行时存储在内存中。

用户模式下在调试期间，当前线程通常确定寄存器上下文。 根据当前线程的寄存器解释对寄存器的调试器命令、 扩展和调试信息窗口中的任何引用。

执行用户模式下使用以下命令之一进行调试时，可以为当前线程以外的值更改寄存器上下文：

[**.cxr （显示上下文记录）**](-cxr--display-context-record-.md)

[**.ecxr （显示异常上下文记录）**](-ecxr--display-exception-context-record-.md)

在内核模式调试，可以使用各种调试器命令，其中包括以下命令来控制寄存器上下文：

[**.thread （设置寄存器上下文）**](-thread--set-register-context-.md)

[**.cxr （显示上下文记录）**](-cxr--display-context-record-.md)

[**.trap （显示陷阱帧）**](-trap--display-trap-frame-.md)

这些命令不更改 CPU 寄存器的值。 相反，调试器从其位置在内存中检索指定的寄存器上下文。 实际上，调试程序可以仅检索*保存*注册值。 （其他值动态设置，并且不保存。 已保存的值就足够了重新创建的堆栈跟踪。

设置寄存器上下文后，新的寄存器上下文使用的任何命令，使用注册值，如[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)并[ **r （注册）**](r--registers-.md).

但是，当你正在调试多处理器计算机，一些命令，可指定处理器。 (有关此类命令的详细信息，请参阅[包含多个处理器语法](multiprocessor-syntax.md)。)如果指定的命令处理器，该命令使用而不是当前寄存器上下文中，指定的处理器上的活动线程的寄存器上下文，即使在指定的处理器是当前使用的处理器。

此外，如果寄存器上下文不匹配当前处理器模式下设置，这些命令将生成不正确或无意义的输出。 若要避免出现输出错误，取决于注册状态的命令失败，直到更改处理器模式以匹配寄存器上下文。 若要更改处理器模式下，使用[ **.effmach （有效的机器）** ](-effmach--effective-machine-.md)命令，

更改寄存器上下文还可以更改本地上下文。 以这种方式，寄存器上下文可能会影响本地变量的显示。

如果任何应用程序执行、 单步执行，或跟踪发生了寄存器上下文立即重置程序计数器位置以便匹配。 在用户模式下，寄存器上下文也将重置如果更改了当前进程或线程。

寄存器上下文会影响堆栈跟踪，因为堆栈跟踪开始的堆栈指针寄存器的位置 (**esp**在基于 x86 的处理器上) 指向。 如果寄存器上下文设置为无效或不可访问的值，则无法获得堆栈跟踪。

您可以使用的处理器断点 （数据断点） 应用到特定寄存器上下文[ **.apply\_dbp （到上下文应用数据断点）** ](-apply-dbp--apply-data-breakpoint-to-context-.md)命令。

### <a name="span-idlocal-contextspanspan-idlocalcontextspanlocal-context"></a><span id="local-context"></span><span id="LOCAL_CONTEXT"></span>本地上下文

程序是在执行时，本地变量的含义取决于位置的程序计数器，因为此类变量的作用域仅到函数中定义的扩展。

时要执行用户模式或内核模式调试，调试器将使用作为本地上下文的当前函数 （在堆栈上当前的帧） 作用域。 若要更改此上下文，请使用[ **.frame （设置本地上下文）** ](-frame--set-local-context-.md)命令，或双击中所需的帧[调用窗口](calls-window.md)。

在用户模式调试，本地上下文始终是当前线程的堆栈跟踪中的帧。 在内核模式调试中，本地上下文始终是线程的当前寄存器上下文的堆栈跟踪中的帧。

在本地上下文时，可以使用只有一个堆栈帧。 不能访问其他框架中的局部变量。

如果发生以下事件，则会重置本地上下文：

-   单步执行或跟踪任何程序执行

-   任何使用的任何命令中的线程分隔符 （~）

-   对寄存器上下文的任何更改

[ **！ 有关\_每个\_帧**](-for-each-frame.md)扩展使您能够执行单个命令重复一次在堆栈中每个帧。 此命令更改用于每个帧的本地上下文，执行指定的命令，然后返回到其原始值的本地上下文。

 

 





