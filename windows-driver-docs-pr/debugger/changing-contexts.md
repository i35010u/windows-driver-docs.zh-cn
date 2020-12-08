---
title: 更改上下文
description: 更改上下文
keywords:
- 上下文
- 登录会话，上下文
- 上下文，会话上下文
- 会话，上下文
- 用户会话
- 会话
ms.date: 08/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6d1f2657b2c4ef209061f296003ddc08f40ebed8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823487"
---
# <a name="changing-contexts"></a>更改上下文


## <span id="ddk-changing-contexts_dbg"></span><span id="DDK_CHANGING_CONTEXTS_DBG"></span>


在内核模式调试中，有许多进程、线程，以及有时同时执行的用户会话。 因此，诸如 "虚拟地址 0x80002000" 或 " **eax** 寄存器" 之类的短语是不明确的。 您必须指定可理解此类短语的 *上下文* 。

调试时，调试程序具有五种不同的上下文：

1.  会话上下文指示默认的用户会话。 

2.  进程上下文确定调试器解释虚拟地址的方式。

3.  *用户模式地址上下文* 几乎不会直接设置。 更改进程上下文时，会自动设置此上下文。

4.  注册上下文确定调试器如何解释寄存器，并控制堆栈跟踪的结果。 虽然这种情况并不完全准确，但此上下文也称为 *线程上下文*。 *显式上下文* 也是寄存器上下文的类型。 如果指定显式上下文，则使用该上下文而不是当前的注册上下文。

5.  本地上下文确定调试器如何解释局部变量。 此上下文也称为 " *作用域*"。

### <a name="span-idsession-contextspanspan-idsession_contextspansession-context"></a><span id="session-context"></span><span id="SESSION_CONTEXT"></span>会话上下文

可同时运行多个登录会话。 每个登录会话都有自己的进程。

[**！会话**](-session.md)扩展显示所有登录会话或更改当前会话上下文。

当会话号码输入为 "-2" 时，将由 [**！ sprocess**](-sprocess.md) 和 [**！ spoolused**](kernel-mode-extensions.md) 扩展使用会话上下文。

更改会话上下文时，进程上下文会自动更改为该会话的活动进程。

### <a name="span-idprocess-contextspanspan-idprocess_contextspanprocess-context"></a><span id="process-context"></span><span id="PROCESS_CONTEXT"></span>处理上下文

每个进程都有其自己的页面目录，用于记录虚拟地址如何映射到物理地址。 当执行进程中的任何线程时，Windows 操作系统将使用此页面目录来解释虚拟地址。

在用户模式调试期间，当前进程将确定进程上下文。 调试程序命令、扩展和调试信息窗口中使用的虚拟地址通过使用当前进程的页目录进行解释。

在内核模式调试过程中，你可以通过使用 [**. process (设置进程上下文)**](-process--set-process-context-.md) 命令来设置过程上下文。 使用此命令可选择用于解释虚拟地址的进程的页面目录。 设置进程上下文后，可以在任何采用地址的命令中使用此上下文。 甚至可以在此地址设置断点。 通过在 **. process** 命令中包含一个 **/i** 选项来指定侵害性调试，还可以使用内核调试器在用户空间中设置断点。

还可以通过在内核空间函数上使用特定于进程的断点，在内核调试器中设置用户模式断点。 设置战略断点并等待适当的上下文启动。

*用户模式地址上下文* 是进程上下文的一部分。 通常，您不必直接设置用户模式地址上下文。 如果设置了过程上下文，则用户模式地址上下文会自动更改为进程的相关页表的目录基。 

当你在内核模式调试过程中设置进程上下文时，该进程上下文会一直保留，直到另一个 **。 process** 命令更改上下文。 用户模式地址上下文还会保留，直到 **处理** 或 **上下文** 命令更改。 当目标计算机执行时，这些上下文不会更改，并且它们不受对寄存器上下文或本地上下文的更改的影响。

### <a name="span-idregister-contextspanspan-idregister_contextspanregister-context"></a><span id="register-context"></span><span id="REGISTER_CONTEXT"></span>注册上下文

每个线程都有自己的寄存器值。 当线程正在执行并在执行另一个线程时将这些值存储在内存中时，这些值将存储在 CPU 寄存器中。

在用户模式调试期间，当前线程通常会确定寄存器上下文。 对调试器命令、扩展和调试信息窗口中的寄存器的任何引用都将根据当前线程的寄存器来解释。

使用以下命令之一执行用户模式调试时，可以将注册上下文更改为当前线程以外的值：

[**.cxr（显示上下文记录）**](-cxr--display-context-record-.md)

[**.ecxr（显示异常上下文记录）**](-ecxr--display-exception-context-record-.md)

在内核模式调试过程中，可以使用各种调试器命令（包括以下命令）控制注册上下文：

[**.thread（设置寄存器上下文）**](-thread--set-register-context-.md)

[**.cxr（显示上下文记录）**](-cxr--display-context-record-.md)

[**.trap（显示陷阱帧）**](-trap--display-trap-frame-.md)

这些命令不会更改 CPU 寄存器的值。 相反，调试器从其在内存中的位置检索指定的寄存器上下文。 实际上，调试器只能检索 *保存* 的寄存器值。 其他值 (会动态设置，并且不会保存。 保存的值足以重新创建堆栈跟踪。

设置注册上下文后，新的寄存器上下文将用于任何使用寄存器值的命令，如 [**k (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 和 [**r (寄存器)**](r--registers-.md)。

但是，在调试多处理器计算机时，某些命令使你能够指定处理器。  (有关此类命令的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。 ) 如果为命令指定处理器，则该命令将使用指定处理器上的活动线程的注册上下文而不是当前的注册上下文，即使指定的处理器是当前活动的处理器。

此外，如果寄存器上下文与当前处理器模式设置不匹配，则这些命令会产生不正确或无意义的输出。 若要避免输出错误，依赖于注册状态的命令将失败，直到您更改处理器模式以匹配注册上下文为止。 若要更改处理器模式，请使用 [**effmach (有效的计算机)**](-effmach--effective-machine-.md) 命令，

更改注册上下文还可以更改本地上下文。 通过这种方式，注册上下文可能会影响本地变量的显示。

如果发生了任何应用程序执行、单步执行或跟踪，则会立即重置注册上下文以匹配程序计数器的位置。 在用户模式下，如果当前进程或线程发生了更改，则寄存器上下文也会重置。

注册上下文会影响堆栈跟踪，因为堆栈跟踪在基于 x86 的处理器上的堆栈指针注册 (**esp**) 指向的位置开始。 如果将注册上下文设置为无效或无法访问的值，则无法获取堆栈跟踪。

通过使用，可以将处理器断点 (数据断点) 应用到特定的寄存器上下文 [**。应用 \_ .Dbp (将数据断点应用于上下文)**](-apply-dbp--apply-data-breakpoint-to-context-.md) 命令。

### <a name="span-idlocal-contextspanspan-idlocal_contextspanlocal-context"></a><span id="local-context"></span><span id="LOCAL_CONTEXT"></span>本地上下文

当程序正在执行时，本地变量的意义取决于程序计数器的位置，因为此类变量的作用域只扩展到在其中定义的函数。

执行用户模式或内核模式调试时，调试器使用当前函数的作用域 (堆栈上的当前帧) 作为本地上下文。 若要更改此上下文，请使用 [**. frame (设置本地上下文)**](-frame--set-local-context-.md) 命令，或在 [调用窗口](calls-window.md)中双击所需的帧。

在用户模式调试中，本地上下文始终是当前线程的堆栈跟踪内的帧。 在内核模式调试中，本地上下文始终是当前寄存器上下文的线程的堆栈跟踪内的帧。

对于本地上下文，一次只能使用一个堆栈帧。 无法访问其他帧中的局部变量。

如果发生以下任何事件，则会重置本地上下文：

-   任何程序执行、单步执行或跟踪

-   在任何命令中使用线程分隔符 (~) 

-   对寄存器上下文所做的任何更改

[**！对于 \_ 每个 \_ 帧**](-for-each-frame.md)扩展，可以重复执行单个命令，为堆栈中的每个帧执行一次。 此命令更改每个帧的本地上下文，执行指定的命令，然后将本地上下文返回到其原始值。

 

 





