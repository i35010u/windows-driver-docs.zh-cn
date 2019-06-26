---
title: 调试 DRIVER_VERIFIER_DETECTED_VIOLATION (C4) 0x20002-0x20022
description: 当有 DDI 符合性检查选项处于选中状态，并且驱动程序验证程序检测到驱动程序违反了某个 DDI 符合性规则时，驱动程序验证程序将生成错误检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION (参数 1 等于特定符合性规则的标识符）。
ms.assetid: 9817AC4B-2BE8-44AC-8C9B-DED5EF0A7DD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0768eeced30f61df33e77a794776cab31d6ce26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371561"
---
# <a name="debugging-ddi-compliance-bugs---driververifierdetectedviolation-c4-0x20002---0x20022"></a>调试 DDI 符合性错误的驱动程序\_VERIFIER\_检测到\_冲突 (C4):0x20002 - 0x20022


当你具有[DDI 符合性检查](ddi-compliance-checking.md)选择选项，并且驱动程序验证程序检测到驱动程序违反了某个 DDI 符合性规则[Driver Verifier](driver-verifier.md)生成[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) （参数 1 等于为特定的符合性规则的标识符）。

DDI 符合性规则可确保驱动程序正确地与 Windows 操作系统内核交互。 例如，规则将验证您的驱动程序在所需的 IRQL 对函数进行函数调用或驱动程序正确地获取和释放自旋锁。 本部分介绍调试这些冲突的一些示例策略。

## <a name="debugging-ddi-compliance-checking-violations"></a>调试 DDI 符合性检查冲突


-   [使用 ！ 分析以显示 bug 检查有关的信息](#use-analyze-to-display-information-about-the-bug-check)
-   [使用 ！ ruleinfo 扩展命令](#use-the-ruleinfo-extension-command)
-   [使用 ！ 分析 – v 命令，以确定在源代码中的冲突的位置](#use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code)
-   [修复 DDI 符合性冲突的原因](#fixing-the-cause-of-the-ddi-compliance-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用 ！ 分析以显示 bug 检查有关的信息

最佳的第一步是运行后可以控制在调试器中出现任何错误检查，与一样[ **！ 分析-v** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)命令。

```
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
Arg1: 00020004, ID of the 'IrqlExAllocatePool' rule that was violated.
Arg2: 8481c118, A pointer to the string describing the violated rule condition.
Arg3: 00000000, Reserved (unused).
Arg4: 00000000, Reserved (unused).

## Debugging Details:


DV_VIOLATED_CONDITION:  ExAllocatePoolWithTagPriority should only be called at IRQL <= DISPATCH_LEVEL.

DV_MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=216021

DV_RULE_INFO: 0x20004
```

每当[Driver Verifier](driver-verifier.md)捕获[DDI 符合性检查](ddi-compliance-checking.md)冲突，将在提供有关冲突信息[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)输出。

在此示例中， [ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)具有一个参数 1 (Arg1) 0x20004，指示已违反该驱动程序的值[ **IrqlExAllocatePool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)符合性规则。

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)输出包括以下信息：

**DV\_VIOLATED\_条件：** 此字段提供导致规则冲突的原因的说明。 在此示例中，违反的条件时，驱动程序尝试分配内存在非常高的 IRQL 级别，或尝试分配的页面缓冲的池内存在调度\_级别。 例如，这可能已尝试调用的驱动程序[ **ExAllocatePoolWithTagPriority** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtagpriority)中断服务例程 (ISR) 或尝试分配页面缓冲的池内存的驱动程序中同时保留自旋锁。

**DV\_MSDN\_链接：** 在 WinDBG 中，这是导致调试器打开 MSDN 页显示的有关详细信息的活动链接[ **IrqlExAllocatePool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)规则。

**DV\_规则\_信息：** 在 WinDBG 中，这是将显示有关此规则从提供的帮助信息的调试器的活动链接。

### <a name="use-the-ruleinfo-extension-command"></a>使用 ！ ruleinfo 扩展命令

**DV\_规则\_信息：** 字段 **！ 分析**输出显示了可用于查找有关此规则冲突的详细信息的命令。 对于此示例中，可以使用命令： **！ ruleinfo 0x20004**

```
kd> !ruleinfo 0x20004

RULE_ID: 0x20004

RULE_NAME: IrqlExAllocatePool

RULE_DESCRIPTION:
The IrqlExAllocatePool rule specifies that the driver calls:
ExAllocatePool,
ExAllocatePoolWithTag,
ExAllocatePoolWithQuota,
ExAllocatePoolWithQuotaTag and
ExAllocatePoolWithTagPriority
only when it is executing at IRQL <= DISPATCH_LEVEL. A caller
executing at DISPATCH_LEVEL must specify a NonPagedXxx value
for PoolType. A caller executing at IRQL <= APC_LEVEL can
specify any POOL_TYPE value.

MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=216021
```

### <a name="use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code"></a>使用 ！ 分析-v 命令，以确定在源代码中的冲突的位置

当捕获到此冲突时，将 bug 驱动程序验证程序来立即检查系统。 **！ 分析**输出将显示当前 IRQL，当前堆栈，点的位置进行调用来分配内存，以及启用了源代码 **！ 分析 – v** (有关详细) 输出还将显示源在其中生成分配请求的文件和行号：

```
CURRENT_IRQL:  10

ANALYSIS_VERSION: 6.13.0016.1929 (debuggers(dbg).130725-1857) amd64fre

LAST_CONTROL_TRANSFER:  from 80ff159d to 80f751f4

STACK_TEXT:  
82f9eaa4 81dda59d 00000003 86fab4b0 00000065 nt!RtlpBreakWithStatusInstruction
82f9eaf8 81dda0b7 82fa0138 82f9eef8 82f9ef40 nt!KiBugCheckDebugBreak+0x1f
82f9eecc 81d5cdc6 000000c4 00020004 85435118 nt!KeBugCheck2+0x676
82f9eef0 81d5ccfd 000000c4 00020004 85435118 nt!KiBugCheck2+0xc6
82f9ef10 8542cb4e 000000c4 00020004 85435118 nt!KeBugCheckEx+0x19
82f9ef30 85425ded ffffffff 85425e0d 82f9ef60 VerifierExt!SLIC_abort+0x40
82f9ef38 85425e0d 82f9ef60 8210c19e 00000080 VerifierExt!SLIC_ExAllocatePoolWithTagPriority_internal_entry_IrqlExAllocatePool+0x6f
82f9ef40 8210c19e 00000080 00000000 00000000 VerifierExt!ExAllocatePoolWithTagPriority_internal_wrapper+0x19
82f9ef60 826c9e16 00000000 00000000 00000000 nt!VerifierExAllocatePoolWithTag+0x24
82f9efa8 81d0726c 833cba80 8a4b9480 00000000 MyDriver!HandleISR+0x146
82f9efbc 81d071c1 833cba80 8a4b9480 000000b8 nt!KiInterruptMessageDispatch+0x12
82f9efe4 81d71f29 00000001 525b61ea 00000224 nt!KiCallInterruptServiceRoutine+0x6d
82f9efe8 00000000 525b61ea 00000224 00000000 nt!KiInterruptDispatch+0x49

STACK_COMMAND:  kb

FOLLOWUP_IP: 
MyDriver!HandleISR+0x140
826c9e10 ff154440699b    call    dword ptr [IrqlExAllocatePool_ExAllocatePoolWithTag!_imp__ExAllocatePoolWithTag (9b694044)]

FAULTING_SOURCE_LINE:  d:\drvsrc\mydriver\isrhandler.c

FAULTING_SOURCE_FILE:  d:\drvsrc\mydriver\isrhandler.c

FAULTING_SOURCE_LINE_NUMBER:  206
```

### <a name="fixing-the-cause-of-the-ddi-compliance-violation"></a>修复 DDI 符合性冲突的原因

修复这些错误检查的具有在范围内 0x00020000 到 0x00020022 Arg1 值，通常包含验证该驱动程序符合相应的文档中所述的 API 和 DDI 使用条件。

在我们在此处使用 (0x20004) 示例中，在 ISR 中任何排序的内存分配是否会违反为设置的 IRQL 规则[ **ExAllocatePoolWithTagPriority** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtagpriority)例程。

一般情况下，应查看有关该例程的 IRQL 和正确的使用情况信息的文档。 查看特定于[DDI 符合性规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)测试函数。 在这种情况下，该规则是[ **IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)。

使用[Static Driver Verifier](static-driver-verifier.md)分析驱动程序源代码，使用相同的规则。 Static Driver Verifier 是一个工具，扫描 Windows 驱动程序的源代码并通过模拟的各种代码路径执行报告可能存在的问题。 Static Driver Verifier 是一个很好的开发时间实用程序，以帮助识别这些类型的问题。

## <a name="related-topics"></a>相关主题


[DDI 符合性检查](ddi-compliance-checking.md)

[DDI 符合性规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[静态驱动程序验证程序](static-driver-verifier.md)

[**Bug 检查 0xC4:驱动程序\_VERIFIER\_检测到\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)

 

 






