---
title: 已检验版本如何指出问题
description: 已检验版本如何指出问题
ms.assetid: 373519e0-bca9-434e-8cc3-e11c2d4b42a4
keywords:
- 检查内部版本号 WDK，问题通知
- 通知 WDK 检查生成
- 断言检查 WDK 版本
- 断点 WDK
- 调试器消息 WDK
- 检查生成邮件 WDK
- 错误 WDK 检查生成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81478c63008e35f60b35159a6e51537d5200b373
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330648"
---
# <a name="how-the-checked-build-indicates-a-problem"></a>已检验版本如何指出问题


## <span id="ddk_how_the_checked_build_indicates_a_problem_tools"></span><span id="DDK_HOW_THE_CHECKED_BUILD_INDICATES_A_PROBLEM_TOOLS"></span>


操作系统已检验的版本使用多种方法来通知你发现的问题。 这些方法包括断言失败、 断点以及调试器消息。 所有这些方法会导致从内核调试程序的输出。 因此，若要很有帮助，必须运行已检验的版本与内核模式调试程序 （如 WinDbg 或 KD） 连接。

有关调试的详细信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

### <a name="span-idassertfailuresspanspan-idassertfailuresspanassert-failures"></a><span id="assert_failures"></span><span id="ASSERT_FAILURES"></span>断言失败

已检验的版本执行的检查的大多数作为实现[ **ASSERT** ](https://msdn.microsoft.com/library/windows/hardware/ff542107)语句。 如果断言的表达式的计算结果为**FALSE**，调试器将显示包含的消息：

-   失败的代码表达式的文本

-   源的代码路径、 文件名和失败的断言例程的行号

下面的示例显示了断言失败 I/O 管理器中时，调试器显示的输出：

```
*** Assertion failed: Irp->IoStatus.Status != 0xffffffff
***   Source File: D:\nt\private\ntos\io\iosubs.c, line 3305

0:Break, Ignore, Terminate Process or Terminate Thread (bipt)? b
0:Execute '!cxr BD94B918' to dump context
Break instruction exception - code 80000003 (first chance)
ntkrnlmp!DbgBreakPoint:
804a3ce4 cc               int     3
```

调试程序输出中所示，为"中断、 忽略、 终止进程或终止线程。"要求用户 用户通过输入"b"，回答导致调试器停止系统执行与断点。 因此，用户现在可以继续调试时发现的问题。

在该失败的断言将影响系统的方式取决于多种因素。 在 Windows Vista 之前的 Windows 版本，如果已启用调试的操作系统在系统启动过程中，系统会进入调试器 （如果已连接） 或挂起正在等待调试程序连接。 如果未启用调试，系统将崩溃， [ **Bug 检查 0x1E** ](https://msdn.microsoft.com/library/windows/hardware/ff557408) (KMODE\_异常\_不\_HANDLED) 0x80000003 参数 1 值。 在 Windows Vista 及更高版本，系统将中断到调试器，仅当连接调试器。 如果未启用调试，或如果启用调试，但调试器未连接，（尽管仍会执行断言检查），将不会报告失败的断言。 如果你正在开发一个驱动程序并想要明确地中断调试器，如果启用调试，但未连接到调试器，可以使用[ **DbgBreakPoint** ](https://msdn.microsoft.com/library/windows/hardware/ff543626)在代码中的语句。

某些[ **ASSERT** ](https://msdn.microsoft.com/library/windows/hardware/ff542107)故障的前面有其他[ **DbgPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff543632)输出。 此类型的断言的一个常见示例是以下[ **PAGED\_代码**](https://msdn.microsoft.com/library/windows/hardware/ff558773) ntddk.h 和 wdm.h 中用于驱动程序的内部版本中定义的宏：

```
#define PAGED_CODE() \
    if (KeGetCurrentIrql() > APC_LEVEL) { \
KdPrint(( "EX: Pageable code called at IRQL %d\n", KeGetCurrentIrql() )); \
        ASSERT(FALSE); \
        }
```

此宏是经常用于在操作系统中验证仅在适用于 Irql 调用可分页的函数。

通常，你可以检查失败的文本的代码表达式以确定声明，包括驱动程序的操作时，出现了断言和被调用的函数的原因。 **KB （显示堆栈跟踪）** 调试器命令对此分析至关重要。

最常见的 ASSERT 调用列表，请参阅[检查生成的 assert 语句](checked-build-asserts.md)。

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>断点

检查内部版本号还可以使用断点表示存在问题。 断点，通常都会骤然[ **DbgPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff543632)语句，这会导致调试器中以显示有关所遇到的问题的信息。 如果调试器未连接到系统断点发生时，系统崩溃，并解释性的所有消息都都将丢失。

中列出了一些最常见的消息已检验版本，在前面的断点和其遇到的驱动程序编写人员[检查生成断点和消息](checked-build-breakpoints-and-messages.md)。

下面的示例演示如何**DbgPrint**调用和断点出现在调试器中：

```
*** DPC routine > 1 sec --- This is not a break in KeUpdateSystemTime
Break instruction exception - code 80000003 (first chance)
NTOSKRNL!DbgBreakPoint:
804a3ce4 cc               int     3
```

此示例演示调试程序条消息，指示单个延缓的过程调用 (DPC) 正在运行的时间超过一秒，并说明了在调试内部版本中实现的检查的类型。 此断点表示驱动程序所用很长时间在 DPC 例程中，这可能表示有严重的驱动程序问题。 但是，如果驱动程序将在其 DPC 例程，从而将扩展 DPC 运行所需的时间长度中生成大量的调试输出，也可能发生此断点。 若要发现问题的根本原因，检查 DPC 例程执行操作，并继续通过断点一次或两次。

在极少数情况下在遇到断点时不显示任何消息，务必要检查的内核堆栈跟踪 (使用**KB**调试器命令) 来确定遇到断点。 通常情况下，这将提供强线索对断点的原因。

下面的示例演示了许多 Windows 驱动程序开发人员，以及堆栈跟踪发生过的常见断点：

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

您可以看到此堆栈跟踪中，为调用的结果执行断点**KfAcquireSpinLock**。 检查 wdm.h 中后，您可以看到这是由驱动程序引用的函数的实际名称[ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)。 即使在断点之前显示了任何消息，可以看到在堆栈的顶部断点的位置 (**ntkrnlmp ！SpinLockSpinningForTooLong**)。 此位置表示该断点的原因：旋转锁具有旋转，等待的时间非常长的购置。

### <a name="span-iddebuggermessagesspanspan-iddebuggermessagesspandebugger-messages"></a><span id="debugger_messages"></span><span id="DEBUGGER_MESSAGES"></span>调试器消息

检查内部版本号还可以使用调试器消息来标识，或提供有关已发生错误的其他信息。 调试器消息的最常见的源是从非内核和非 HAL 组件，或选中 （调试） 用户模式程序产生错误。 输出量因每个操作系统版本而异。

下面的示例显示了完整的调试内部版本的安装可能会显示的输出。 此输出由 Windows XP 的预发布版本生成的因此更加让人望而却步比通常出现在完全调试内部版本。

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

中列出了一些最常见的已检验的版本可以显示在驱动程序调试期间的消息[检查生成断点和消息](checked-build-breakpoints-and-messages.md)。

启用更多跟踪或信息性消息中各种系统组件也会导致调试器没有后续断点或断言失败的消息。

 

 





