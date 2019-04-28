---
title: 在启用驱动程序验证程序的情况下处理 Bug 检查
description: 驱动程序验证程序在运行时检测到驱动程序错误。 可以使用驱动程序验证程序以及分析调试器命令，来检测和驱动程序中显示有关错误的信息。
ms.assetid: 4226B62B-0AA5-4D04-A32D-7DD22FD694E3
keywords:
- 驱动程序验证程序
- 验证程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07a835eb71d0a959575ae04a7f55970b02d68a89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342079"
---
# <a name="handling-a-bug-check-when-driver-verifier-is-enabled"></a>在启用驱动程序验证程序的情况下处理 Bug 检查


[驱动程序验证程序](https://go.microsoft.com/fwlink/p?LinkID=268663)在运行时检测到驱动程序错误。 可以使用与 Driver Verifier [ **！ 分析**](-analyze.md)调试器命令，以检测和驱动程序中显示有关错误的信息。

在 Windows 8 中， [Driver Verifier](https://go.microsoft.com/fwlink/p?LinkID=268663)新功能，包括已得到增强[DDI 符合性检查](https://go.microsoft.com/fwlink/p?LinkID=268676)。 此处我们提供的示例，演示 DDI 符合性检查。

使用以下过程来进行设置。

1.  建立主机和目标计算机之间的内核模式调试会话。
2.  在目标计算机上安装您的驱动程序。
3.  在目标计算机上，打开命令提示符窗口并输入命令**verifier**。 使用[驱动程序验证程序管理器](https://go.microsoft.com/fwlink/p?LinkID=268659)为您的驱动程序启用驱动程序验证程序。
4.  重新启动目标计算机。

当驱动程序验证程序检测到错误时，它将生成的 bug 检查。 然后 Windows 进入调试器并显示错误的简短说明。 下面是一个示例驱动程序验证程序生成错误检查[**驱动程序\_VERIFIER\_已检测\_冲突 (C4)**](bug-check-0xc4--driver-verifier-detected-violation.md)。

```dbgcmd
Driver Verifier: Extension abort with Error Code 0x20005
Error String ExAcquireFastMutex should only be called at IRQL <= APC_LEVEL.

*** Fatal System Error: 0x000000c4
                       (0x0000000000020005,0xFFFFF88000E16F50,0x0000000000000000,0x0000000000000000)

Break instruction exception - code 80000003 (first chance)

A fatal system error has occurred.
Debugger entered on first try; Bugcheck callbacks have not been invoked.

A fatal system error has occurred.

nt!DbgBreakPointWithStatus:
fffff802`a40ef930 cc              int     3
```

在调试器中，输入[ **！ 分析-v** ](-analyze.md)获取错误的详细的说明。

```dbgcmd
0: kd> !analyze -v
Connected to Windows 8 9200 x64 target at (Thu Oct 11 13:48:31.270 2012 (UTC - 7:00)), ptr64 TRUE
Loading Kernel Symbols
...............................................................
................................................................
...................
Loading User Symbols
..................................................
Loading unloaded module list
............
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
A device driver attempting to corrupt the system has been caught.  This is
because the driver was specified in the registry as being suspect (by the
administrator) and the kernel has enabled substantial checking of this driver.
If the driver attempts to corrupt the system, bugchecks 0xC4, 0xC1 and 0xA will
be among the most commonly seen crashes.
Arguments:
Arg1: 0000000000020005, ID of the 'IrqlExApcLte1' rule that was violated.
Arg2: fffff88000e16f50, A pointer to the string describing the violated rule condition.
Arg3: 0000000000000000, An optional pointer to the rule state variable(s).
Arg4: 0000000000000000, Reserved (unused)

## Debugging Details:

...

DV_VIOLATED_CONDITION:  ExAcquireFastMutex should only be called at IRQL <= APC_LEVEL.

DV_MSDN_LINK: !url https://go.microsoft.com/fwlink/p/?linkid=216022

DV_RULE_INFO: !ruleinfo 0x20005

BUGCHECK_STR:  0xc4_IrqlExApcLte1_XDV

DEFAULT_BUCKET_ID:  WIN8_DRIVER_FAULT

PROCESS_NAME:  TiWorker.exe

CURRENT_IRQL:  9
```

在上面的输出中可以看到的名称和规则的说明**IrqlExApcLte1**、 违反了的并且你可以单击指向描述规则的参考页的链接： <https://go.microsoft.com/fwlink/p/?linkid=216022>。 此外可以单击调试器 command link **！ ruleinfo 0x20005**，以获取有关规则的信息。 在这种情况下，规则规定，不能调用[ExAcquireFastMutex](https://go.microsoft.com/fwlink/p?LinkID=268628)中断请求级别 (IRQL) 是否大于 APC\_级别。 该输出显示当前 IRQL 是 9，并在 wdm.h 中可以看到该 APC\_级别的值为 1。 有关于 Irql 详细信息，请参阅[管理硬件优先级](https://go.microsoft.com/fwlink/p?LinkID=268625)。

输出[ **！ 分析-v** ](-analyze.md)将继续执行堆栈跟踪和有关代码导致了错误的信息。 在下面的输出，可以看到**OnInterrupt**例程中名为 MyDriver.sys [ExAcquireFastMutex](https://go.microsoft.com/fwlink/p?LinkID=268628)。 **OnInterrupt**大于 APC 的 IRQL 在运行一个中断服务例程\_级别，因此，若要调用该例程的冲突[ExAcquireFastMutex](https://go.microsoft.com/fwlink/p?LinkID=268628)。

```dbgcmd
LAST_CONTROL_TRANSFER:  from fffff802a41f00ea to fffff802a40ef930

STACK_TEXT:  
... : nt!DbgBreakPointWithStatus ...
... : nt!KiBugCheckDebugBreak+0x12 ...
... : nt!KeBugCheck2+0x79f ...
... : nt!KeBugCheckEx+0x104 ...
... : VerifierExt!SLIC_abort+0x47 ...
... : VerifierExt!SLIC_ExAcquireFastMutex_entry_irqlexapclte1+0x25 ...
... : VerifierExt!ExAcquireFastMutex_wrapper+0x1a ...
... : nt!ViExAcquireFastMutexCommon+0x1d ...
... : nt!VerifierExAcquireFastMutex+0x1a ...
... : MyDriver!OnInterrupt+0x69 ...
... : nt!KiScanInterruptObjectList+0x6f ...
... : nt!KiChainedDispatch+0x19a ...
...

STACK_COMMAND:  kb

FOLLOWUP_IP: 
MyDriver!OnInterrupt+69 ...
fffff880`16306649 4c8d0510040000  lea     r8,[MyDriver! ?? ::FNODOBFM::`string' (fffff880`16306a60)]

FAULTING_SOURCE_LINE:  c:\MyDriverwdm03\cpp\MyDriver\pnp.c

FAULTING_SOURCE_FILE:  c:\MyDriverwdm03\cpp\MyDriver\pnp.c

FAULTING_SOURCE_LINE_NUMBER:  26

FAULTING_SOURCE_CODE:  
    22:    if(1 == interruptStatus)
    23:    {
    24:       ...
    25:       ExAcquireFastMutex( &(fdoExt->fastMutex) );
>   26:       ...
    27:       ExReleaseFastMutex( &(fdoExt->fastMutex) );
    28:       ...
    29:       return TRUE;
    30:    }
    31:    else


SYMBOL_STACK_INDEX:  9

SYMBOL_NAME:  MyDriver!OnInterrupt+69

FOLLOWUP_NAME:  ...

MODULE_NAME: MyDriver

IMAGE_NAME:  MyDriver.sys

DEBUG_FLR_IMAGE_TIMESTAMP:  50772f37

BUCKET_ID_FUNC_OFFSET:  69

FAILURE_BUCKET_ID:  0xc4_IrqlExApcLte1_XDV_VRF_MyDriver!OnInterrupt

BUCKET_ID:  0xc4_IrqlExApcLte1_XDV_VRF_MyDriver!OnInterrupt
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[静态驱动程序验证程序](https://go.microsoft.com/fwlink/p?LinkID=268668)

 

 






