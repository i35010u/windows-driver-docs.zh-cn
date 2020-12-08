---
title: 调试 DRIVER_VERIFIER_DETECTED_VIOLATION (C4) 0x20002-0x20022
description: 如果选择了 "DDI 相容性检查" 选项，并且驱动程序验证器检测到该驱动程序违反了某个 DDI 符合性规则，则驱动程序验证程序会生成 Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION (，参数1等于特定符合性规则) 的标识符。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 105a18da3122a6ffde363aaaa9d8f168a7b202fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824253"
---
# <a name="debugging-ddi-compliance-bugs---driver_verifier_detected_violation-c4-0x20002---0x20022"></a>调试 DDI 相容性错误-驱动程序 \_ 验证器 \_ 检测到 \_ 违反 (C4) ： 0x20002-0x20022


如果选择了 " [DDI 相容性检查](ddi-compliance-checking.md) " 选项，并且驱动程序验证器检测到该驱动程序违反了某个 DDI 符合性规则，则 [驱动程序验证](driver-verifier.md) 器将生成 [**BUG 检查0xC4：驱动程序验证器 \_ \_ 检测到 \_**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) 与参数1等于特定符合性规则的标识符) 的冲突 (。

DDI 符合性规则确保驱动程序正确与 Windows 操作系统内核交互。 例如，这些规则验证驱动程序是否在函数所需的 IRQL 上进行了函数调用，或驱动程序是否正确获取并释放了自旋锁。 本部分介绍用于调试这些冲突的一些示例策略。

## <a name="debugging-ddi-compliance-checking-violations"></a>调试 DDI 相容性检查冲突


-   [使用！分析显示 bug 检查的相关信息](#use-analyze-to-display-information-about-the-bug-check)
-   [使用！ ruleinfo extension 命令](#use-the-ruleinfo-extension-command)
-   [使用！分析– v 命令在源代码中标识冲突的位置](#use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code)
-   [解决 DDI 遵从性冲突的原因](#fixing-the-cause-of-the-ddi-compliance-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用！分析显示 bug 检查的相关信息

与发生的任何 bug 检查一样，在控制调试器后，最好的第一步是运行 [**！分析-v**](../debugger/-analyze.md) 命令。

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

只要 [驱动程序验证](driver-verifier.md) 器捕获 [DDI 相容性检查](ddi-compliance-checking.md) 冲突，就会在 [**！分析**](../debugger/-analyze.md) 输出中提供有关冲突的信息。

在此示例中， [**Bug 检查0xC4：驱动程序 \_ 验证器 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) 具有参数 1 (Arg1) 值为0x20004，这表示该驱动程序违反了 [**IrqlExAllocatePool**](./wdm-irqlexallocatepool.md) 合规性规则。

[**！分析**](../debugger/-analyze.md)输出包含以下信息：

**DV \_违反 \_ 条件：** 此字段提供了导致规则冲突的原因的说明。 在此示例中，违反的条件是：驱动程序尝试以非常高的 IRQL 级别分配内存，或尝试在调度级别分配页面缓冲池内存 \_ 。 例如，这可能是一个驱动程序，该驱动程序尝试在中断服务例程 (ISR) ，或在持有自旋锁的情况下尝试分配页面缓冲池内存的驱动程序中调用 [**ExAllocatePoolWithTagPriority**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority) 。

**DV \_MSDN \_ 链接：** 在 WinDBG 中，这是一个实时链接，它会使调试器打开 MSDN 页，其中显示了有关 [**IrqlExAllocatePool**](./wdm-irqlexallocatepool.md) 规则的详细信息。

**DV \_规则 \_ 信息：** 在 WinDBG 中，这是一个实时链接，它将从调试器上可用的帮助显示有关此规则的信息。

### <a name="use-the-ruleinfo-extension-command"></a>使用！ ruleinfo extension 命令

" **！分析**" 输出的 " **DV \_ 规则 \_ 信息：** " 字段显示可用于查找有关此规则冲突的详细信息的命令。 在此示例中，可以使用命令： **！ ruleinfo 0x20004**

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

### <a name="use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code"></a>使用！分析-v 命令在源代码中标识冲突的位置

捕获到此冲突时，驱动程序验证程序会立即错误检查系统。 **！分析** 输出将显示当前的 IRQL、当前堆栈、对分配内存进行调用的点，并且如果启用源代码的 **！分析– v** (用于详细) 输出，还会显示发出分配请求的源文件和行号：

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

### <a name="fixing-the-cause-of-the-ddi-compliance-violation"></a>解决 DDI 遵从性冲突的原因

修复这些在0x00020000 到0x00020022 范围内具有 Arg1 值的 bug 检查，通常包括验证驱动程序是否满足相应文档中所述的 API 和 DDI 使用情况。

在此示例中，我们使用了此处 (0x20004) ，则 ISR 中任何排序的内存分配将违反 [**ExAllocatePoolWithTagPriority**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority) 例程的 IRQL 规则集。

一般情况下，应查看有关此例程的文档，以获取有关 IRQL 和正确用法的信息。 查看测试函数的特定 [DDI 符合性规则](/windows-hardware/drivers/ddi/index) 。 在这种情况下，规则为 [**IrqlExAllocatePool**](./wdm-irqlexallocatepool.md)。

使用 [静态驱动程序验证](static-driver-verifier.md) 器分析驱动程序源代码，使用同一规则 () 。 静态驱动程序验证程序是一种工具，它通过模拟各种代码路径的行使来扫描 Windows 驱动程序源代码，并报告可能的问题。 静态驱动程序验证程序是一个出色的开发时实用工具，可帮助确定这些类型的问题。

## <a name="related-topics"></a>相关主题


[DDI 合规性检查](ddi-compliance-checking.md)

[DDI 合规性规则](/windows-hardware/drivers/ddi/index)

[静态驱动程序验证程序](static-driver-verifier.md)

[**Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)

 

