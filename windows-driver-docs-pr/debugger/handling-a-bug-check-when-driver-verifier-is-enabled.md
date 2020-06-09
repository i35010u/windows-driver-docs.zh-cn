---
title: 在启用驱动程序验证程序的情况下处理 Bug 检查
description: 驱动程序验证程序在运行时检测驱动程序错误。 可以结合使用驱动程序验证程序和 "分析调试器" 命令来检测和显示有关驱动程序中的错误的信息。
ms.assetid: 4226B62B-0AA5-4D04-A32D-7DD22FD694E3
keywords:
- 驱动程序验证程序
- 符
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f49951abcbd074a30aa1b492fc2aed30b8d8eab4
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534352"
---
# <a name="handling-a-bug-check-when-driver-verifier-is-enabled"></a>在启用驱动程序验证程序的情况下处理 Bug 检查


[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)程序在运行时检测驱动程序错误。 可以结合使用驱动程序验证程序和[**！分析**](-analyze.md)调试器命令来检测和显示有关驱动程序中的错误的信息。

在 Windows 8 中，[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)已通过新功能（包括[DDI 相容性检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)）进行了增强。 这里提供了一个示例，演示了 DDI 相容性检查。

使用以下过程进行设置。

1.  建立主机和目标计算机之间的内核模式调试会话。
2.  在目标计算机上安装驱动程序。
3.  在目标计算机上，打开命令提示符窗口，然后输入命令**验证**程序。 使用[驱动程序验证器管理器](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier-manager--windows-xp-and-later-)为驱动程序启用驱动程序验证程序。
4.  重新启动目标计算机。

当驱动程序验证程序检测到错误时，它将生成 bug 检查。 然后，Windows 将中断调试器并显示错误的简短说明。 下面是一个示例，其中，驱动程序验证程序生成 Bug 检查[**驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突（C4）**](bug-check-0xc4--driver-verifier-detected-violation.md)。

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

在调试器中，输入[**！分析-v**](-analyze.md)以获取错误的详细说明。

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

在上面的输出中，你可以看到违反规则的名称和**描述，你**可以单击描述该规则的参考页的链接： <https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1> 。 还可以单击 "调试器" 命令链接 " **！ ruleinfo 0x20005**" 以获取有关规则的信息。 在这种情况下，该规则指出，如果中断请求级别（IRQL）高于 APC 级别，则不能调用[ExAcquireFastMutex](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85)) \_ 。 输出显示当前 IRQL 为9，在 wdm .h 中，你可以看到 APC 级别的值为 \_ 1。 有关 IRQLs 的详细信息，请参阅[管理硬件优先级](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)。

[**！分析-v**](-analyze.md)的输出将继续执行堆栈跟踪以及导致错误的代码的相关信息。 在下面的输出中，可以看到 MyDriver 中的**OnInterrupt**例程称为[ExAcquireFastMutex](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))。 **OnInterrupt**是以比 APC 级别更高的 IRQL 运行的中断服务例程 \_ ，因此，此例程在调用[ExAcquireFastMutex](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))时会发生冲突。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[静态驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)

 

 






