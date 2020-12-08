---
title: 已检验版本如何指出问题
description: 已检验版本如何指出问题
keywords:
- 已检查生成 WDK，问题通知
- 通知 WDK 检查版本
- 断言 WDK 检查生成
- 断点 WDK
- 调试器消息 WDK
- 消息 WDK 检查版本
- 错误 WDK 检查版本
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 878ae74334eb547b8476357ab0971b411ae59b17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830719"
---
# <a name="how-the-checked-build-indicates-a-problem"></a>已检验版本如何指出问题

## <span id="ddk_how_the_checked_build_indicates_a_problem_tools"></span><span id="DDK_HOW_THE_CHECKED_BUILD_INDICATES_A_PROBLEM_TOOLS"></span>

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

操作系统的检查内部版本使用各种方法来通知您发现的问题。 这些方法包括断言错误、断点和调试器消息。 所有这些方法都将导致内核调试器输出。 因此，若要非常有用，您必须使用内核模式调试器运行检查的生成 (如 WinDbg 或 KD) 连接。

有关调试的详细信息，请参阅 [Windows 调试](../debugger/index.md)。

### <a name="span-idassert_failuresspanspan-idassert_failuresspanassert-failures"></a><span id="assert_failures"></span><span id="ASSERT_FAILURES"></span>断言失败

检查生成执行的大部分检查都作为 [**ASSERT**](/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85)) 语句实现。 当断言的表达式的计算结果为 **FALSE** 时，调试器将显示一条消息，其中包含：

-   失败的代码表达式的文本

-   失败的 ASSERT 例程的源代码路径、文件名和行号

下面的示例演示了在 i/o 管理器中断言失败时调试器显示的输出：

```
**_ Assertion failed: Irp->IoStatus.Status != 0xffffffff
_*_   Source File: D:\nt\private\ntos\io\iosubs.c, line 3305

0:Break, Ignore, Terminate Process or Terminate Thread (bipt)? b
0:Execute '!cxr BD94B918' to dump context
Break instruction exception - code 80000003 (first chance)
ntkrnlmp!DbgBreakPoint:
804a3ce4 cc               int     3
```

如调试器输出所示，要求用户 "中断、忽略、终止进程或终止线程"。 用户通过输入 "b" 回答，这会导致调试器停止系统执行并带有断点。 因此，用户现在可以继续调试发现的问题。

失败的断言对系统产生的影响的方式取决于多个因素。 在 Windows Vista 之前的 Windows 版本中，如果在系统启动过程中为操作系统启用了调试，则系统会在连接) 或挂起等待调试器连接的情况下中断调试器 (。 如果未启用调试，系统将崩溃并出现 [*错误检查 0x1E* *](../debugger/bug-check-0x1e--kmode-exception-not-handled.md) (\_ \_ 未 \_ 使用0x80000003 的参数1值) 处理 KMODE 异常。 在 Windows Vista 和更高版本中，只有当调试器连接时，系统才会中断调试器。 如果未启用调试，或启用了调试但未连接调试程序，则将不会报告失败的断言 (但) 仍将执行断言检查。 如果正在开发驱动程序，并且希望在启用调试但未连接调试器的情况下，明确中断调试器，则可以在代码中使用 [**DbgBreakPoint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint) 语句。

某些 [**断言**](/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85)) 失败之前有其他 [**DbgPrint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint) 输出。 此类断言的一个常见示例是下面的 [**分页 \_ 代码**](../kernel/mm-bad-pointer.md) 宏，该宏是在 ntddk 中定义的，并在驱动程序的已检查版本中使用：

```
#define PAGED_CODE() \
    if (KeGetCurrentIrql() > APC_LEVEL) { \
KdPrint(( "EX: Pageable code called at IRQL %d\n", KeGetCurrentIrql() )); \
        ASSERT(FALSE); \
        }
```

此宏经常用于操作系统中，以验证是否仅在适当的 IRQLs 调用了可分页函数。

通常可以检查失败代码表达式的文本，以确定断言的原因，包括发生断言时驱动程序的操作和调用的函数。 **KB (显示堆栈跟踪)** 调试器命令对于此分析至关重要。

有关最常见的断言调用的列表，请参阅 [检查的生成断言](checked-build-asserts.md)。

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>处

选中的生成还可以使用断点指示问题。 断点前面通常带有 [**DbgPrint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint) 语句，这将导致调试器显示有关遇到的问题的信息。 如果在发生断点时调试器未连接到系统，则系统崩溃并所有解释性消息都将丢失。

检查生成中的断点前面的某些最常见消息以及驱动程序编写器遇到的一些最常见消息都列在 " [已检查生成断点和消息](checked-build-breakpoints-and-messages.md)" 中。

下面的示例演示了 **DbgPrint** 调用和断点在调试器中的显示方式：

```
**_ DPC routine > 1 sec --- This is not a break in KeUpdateSystemTime
Break instruction exception - code 80000003 (first chance)
NTOSKRNL!DbgBreakPoint:
804a3ce4 cc               int     3
```

此示例显示了一条调试器消息，该消息指示 (DPC) 运行的时间超过一秒，并说明在检查版本中实现的检查类型。 此断点表示驱动程序在 DPC 例程中花费了很长时间，这可能表示出现了严重的驱动程序问题。 另一方面，如果驱动程序在其 DPC 例程中生成大量调试输出，则也会发生此断点，从而延长了 DPC 运行所需的时间长度。 若要发现此问题的根本原因，请检查 DPC 例程正在执行的操作，并在断点之后的一次或两次继续。

在极少数情况下，当遇到断点但未显示消息时，请务必检查内核堆栈跟踪 (使用 _ *KB** 调试程序命令) 来确定断点的位置。 通常，这将为断点原因提供很强的线索。

下面的示例演示了许多 Windows 驱动程序开发人员检测到的常见断点以及堆栈跟踪：

```
Break instruction exception - code 80000003 (first chance)
ntkrnlmp!SpinLockSpinningForTooLong:
8069aafd cc               int     3
1: kd> kb
ChildEBP RetAddr  Args to Child              
f9f77c4c 80103a6c f9f77c84 00000005 fa20e7df ntkrnlmp!SpinLockSpinningForTooLong
f9f77c58 fa20e7df 81b34930 e1558bd0 00180016 halmps!KfAcquireSpinLock+0x3c
f9f77c7c 80742683 000000ff 81ba6000 00000000 nothing+0x7df
f9f77d54 80742893 0000046c 81ba6000 f9f77d80 ntkrnlmp!IopLoadDriver+0x785
f9f77d78 805f8d2d 00000000 00000000 81fa88b8 ntkrnlmp!IopLoadUnloadDriver+0x75
f9f77dac 807cd14f f7d59ce8 00000000 00000000 ntkrnlmp!ExpWorkerThread+0x129
f9f77ddc 8069bece 805f8c04 00000001 00000000 ntkrnlmp!PspSystemThreadStartup+0x4d
00000000 00000000 00000000 00000000 00000000 ntkrnlmp!KiThreadStartup+0x16
```

从此堆栈跟踪中可以看到，断点作为调用 **KfAcquireSpinLock** 的结果而发生。 检查了 wdm 后，可以看到这是驱动程序所引用的函数的实际名称（ [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)）。 即使断点之前未显示消息，也可以在堆栈顶部看到断点的位置 (**ntkrnlmp！SpinLockSpinningForTooLong**) 。 此位置指示断点的原因：旋转锁已旋转，等待获取的时间过长。

### <a name="span-iddebugger_messagesspanspan-iddebugger_messagesspandebugger-messages"></a><span id="debugger_messages"></span><span id="DEBUGGER_MESSAGES"></span>调试器消息

选中的生成还可以使用调试器消息来标识或提供有关已发生的错误的其他信息。 调试器消息的最常见源是源自非内核和非 HAL 组件的错误，或从已检查 (调试) 用户模式程序发出的错误。 每个操作系统版本的输出量有所不同。

下面的示例显示了安装完整的已选中版本可能显示的输出。 此输出是由 Windows XP 的预发布版本生成的，因此甚至比在完全检查的内部版本上通常会出现更多的 voluminous。

```
0:Attempting to load winsock
0:Checking for presence of ws2_32
0:Looking in ws2_32 for getaddrinfo
0:AudioSrv: 1:CreateSessionUserSid: GetCurrentUserTokenW failed, LastError=1245
1:AudioSrv: RegOpenConsoleUser: no console sid
0:(s: 0 0xc4.d0 winlogon.exe) USRK-[Wrn=170] CloseDesktop: Desktop 0X81CEAF78 still in use by thread 0XE16F3EA0
0:GetWinStationUserToken: Error 1702 getting UserToken LogonId 0
1:AudioSrv: InitializeForNewConsoleUser: User SID S-1-5-21-329068152-1292428093-1547161642-500
1:(s: 0 0x240.3a8 spoolsv.exe) USRK-[Wrn=1400] ValidateHwnd: Invalid hwnd (0X0000FFFF)
0:(s: 0 0x240.3a8 spoolsv.exe) USRK-[Wrn=1400] ValidateHwnd: Invalid hwnd (0X0000FFFF)
0:bReadUserSystemEUDCRegistry():fail NtStatus - c0000000
0:GDI: GDISRV:Fail to read system wide eudc
0:
1:TERMSRV : Not Personal Workstation
0:(s: 0 0x260.3c4 Explorer.EXE) USER-[Wrn=1400] HMValidateHandle: Invalid:00000000 Type:0x1
0:(s: 0 0x260.3c4 Explorer.EXE) USER-[Wrn=1400] HMValidateHandle: Invalid:00000000 Type:0x1
0:(s: 0 0x260.3c4 Explorer.EXE) USER-[Wrn=1400] HMValidateHandle: Invalid:00000000 Type:0x1
```

在驱动程序调试过程中，检查的生成可以显示的一些最常见消息列在 " [已检查生成断点和消息](checked-build-breakpoints-and-messages.md)" 中。

在各种系统组件中启用其他跟踪或信息性消息也可能导致调试器消息，而不会发生后续断点或断言错误。

 

