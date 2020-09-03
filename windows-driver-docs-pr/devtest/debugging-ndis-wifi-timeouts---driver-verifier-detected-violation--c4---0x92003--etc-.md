---
title: '调试 DRIVER_VERIFIER_DETECTED_VIOLATION (C4) '
description: 驱动程序验证程序检测到驱动程序违反了 NDIS/WiFi 超时规则之一。
ms.assetid: 73D4B6DF-E667-4C71-B985-FCDC05837908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2a231b6228a76ad6c589adcda999f549dfba72a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383967"
---
# <a name="debugging-ndiswifi-time-out-errors---driver_verifier_detected_violation-c4"></a>调试 NDIS/WiFi 超时错误-驱动程序 \_ 验证器 \_ 检测到 \_ 违反 (C4) 


如果选择了 [ndis/wifi 验证](ndis-wifi-verification.md) 选项，并且驱动程序验证器检测到驱动程序违反了某个 NDIS/wifi 超时规则，则 [驱动程序验证](driver-verifier.md) 器将生成 [**BUG 检查0xC4：驱动程序验证器 \_ \_ 检测到 \_ **](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) 与参数1等于特定 NDIS/wifi 超时规则的标识符) 的冲突 (。

当驱动程序验证器测试 NDIS/WIFI 超时规则（如 [**NdisTimedOidComplete**](./ndis-ndistimedoidcomplete.md)）时，驱动程序验证程序的轮询机制需要在多个循环中通过微型端口驱动程序的响应。 每个定时规则定义了其自己的最大周期。 超过最大值时，驱动程序验证器会生成 bug 检查。 本部分介绍用于调试这些冲突的一些示例策略。

## <a name="debugging-ndiswifi-timeout-errors"></a>调试 NDIS/WIFI 超时错误


-   [使用！分析显示 bug 检查的相关信息](#use-analyze-to-display-information-about-the-bug-check)
-   [使用！ ruleinfo extension 命令](#use-the-ruleinfo-extension-command)
-   [单击 "最后一个 \_ 调用 \_ 堆栈" 链接以标识冲突的位置。](#identify-the-location-of-the-violation)
-   [修复 NDIS/WIFI 超时冲突的原因](#fixing-the-cause-of-the-ndis-wifi-timeout-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用！分析显示 bug 检查的相关信息

与发生的任何 bug 检查一样，在控制调试器后，最好的第一步是运行 [**！分析-v**](../debugger/-analyze.md) 命令。

```
DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
A device driver attempting to corrupt the system has been caught.  This is
because the driver was specified in the registry as being suspect (by the
administrator) and the kernel has enabled substantial checking of this driver.
If the driver attempts to corrupt the system, bugchecks 0xC4, 0xC1 and 0xA will
be among the most commonly seen crashes.
Arguments:
Arg1: 00092003, ID of the 'NdisTimedOidComplete' rule that was violated.
Arg2: 8521dd34, A pointer to the string describing the violated rule condition.
Arg3: 9c17b860, Address of internal rule state (second argument to !ruleinfo).
Arg4: 9c1f3480, Address of supplemental states (third argument to !ruleinfo).
```

在 **！分析-v** 输出的以下部分中，违反此规则的原因显示在 "DV \_ 违反 \_ 条件" 字段下。 "DV \_ MSDN \_ 链接" 部分也有助于获取有关此规则的文档的链接。

```
## Debugging Details:


*** ERROR: Module load completed but symbols could not be loaded for NdisTimedOidComplete.sys

DV_VIOLATED_CONDITION:  Timeout on completing an NDIS OID request.

DV_MSDN_LINK: https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete

DRIVER_OBJECT: 98a87980

IMAGE_NAME:  NdisTimedOidComplete.sys

DEBUG_FLR_IMAGE_TIMESTAMP:  5229c857

MODULE_NAME: NdisTimedOidComplete

FAULTING_MODULE: 9fee1000 NdisTimedOidComplete
```

在此分析输出的后面，你可以单击 "DV 规则信息" 部分下的链接 \_ \_ 以获取其他规则说明。 对于超时类型的规则，当前堆栈可能不包含相关信息。

```
DV_RULE_INFO: 0x92003

BUGCHECK_STR:  0xc4_NdisTimedOidComplete_XDV

DEFAULT_BUCKET_ID:  WIN8_DRIVER_FAULT

PROCESS_NAME:  System

CURRENT_IRQL:  2

ANALYSIS_VERSION: 6.13.0016.1929 (debuggers(dbg).130725-1857) amd64fre

LAST_CONTROL_TRANSFER:  from 80f87fd3 to 80f0ed14

STACK_TEXT:  
8912380c 80f87fd3 00000003 e6c3476e 00000065 nt!RtlpBreakWithStatusInstruction
89123860 80f87aed 825a6138 89123c5c 89123cac nt!KiBugCheckDebugBreak+0x1f
89123c30 80f0d8d6 000000c4 00092003 8521dd34 nt!KeBugCheck2+0x676
89123c54 80f0d80d 000000c4 00092003 8521dd34 nt!KiBugCheck2+0xc6
89123c74 85211584 000000c4 00092003 8521dd34 nt!KeBugCheckEx+0x19
89123cac 85216d54 9c17b860 9c1f3480 9c17b8dc VerifierExt!SLIC_StatefulAbort+0x1a4
89123cd0 85216ffe 85220000 85215f5b 00000000 VerifierExt!Ndis_OnTimerExpire+0x234
89123cd8 85215f5b 00000000 80ecd56a 843d0c38 VerifierExt!CheckOnTimerExpire+0x26
89123ce0 80ecd56a 843d0c38 00000000 80ecd502 VerifierExt!XdvPassiveTimerRoutine+0x1d
89123d24 80eec133 882befd0 00000000 887debc0 nt!IopProcessWorkItem+0x68
89123d70 80ec1162 00000000 e6c342be 00000000 nt!ExpWorkerThread+0x14f
89123db0 80f23201 80eebfe4 00000000 00000000 nt!PspSystemThreadStartup+0x58
89123dbc 00000000 00000000 00000000 00000000 nt!KiThreadStartup+0x15
```

### <a name="use-the-ruleinfo-extension-command"></a>使用！ ruleinfo extension 命令

" **！分析**" 输出的 " **DV \_ 规则 \_ 信息：** " 字段显示一个指向命令的链接，你可以使用该命令查找有关此规则冲突的详细信息。 在此示例中，如果单击该链接，它将运行[**!ruleinfo**](../debugger/-ruleinfo.md)带规则 \_ ID (0x92003) Arg3 和 Arg 4 bug 检查值的！ ruleinfo 命令。

```
kd> !ruleinfo 0x92003 0xffffffff9c17b860 0xffffffff9c1f3480

RULE_ID: 0x92003

RULE_NAME: NdisTimedOidComplete

RULE_DESCRIPTION:
This rule verifies if an NDIS miniport driver completes an OID in time.
The OID is tracked (a.k.a., TRACKED_OBJECT). Use !ndiskd.oid .

MSDN_LINK: https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete

CONTEXT: Miniport 0x86BD10E8

CURRENT_TIME (Timed Rules): 168 seconds

TRACKED_OBJECT: 0x86633804

LAST_CALL_STACK: 0x9C1F3480 + 0x10

RULE_STATE: 0x9C1F3480
```

### <a name="identify-the-location-of-the-violation"></a>确定冲突的位置

在此处使用的示例中，微型端口驱动程序 NdisTimedOidComplete.sys，它将一个睡眠周期注入到其 *MPOidRequest* 函数中。 可以通过单击 \_ \_ [**！ ruleinfo**](../debugger/-ruleinfo.md) 输出中的最后一个调用堆栈链接进行检查。 这是驱动程序验证程序看到的最后一个调用堆栈，在此，我们看到在超时发生之前 NDIS 调用了 *ndisMInvokeOidRequest* 。

```
kd> dps 0x9C1F3480 + 0x10
9c1f3490  850e1e37 ndis!ndisMInvokeOidRequest+0x16641
9c1f3494  850765c8 ndis!ndisMDoOidRequest+0x24a
9c1f3498  8507552a ndis!ndisQueueOidRequest+0x2fa
9c1f349c  8507372b ndis!ndisQuerySetMiniportEx+0xd9
9c1f34a0  85073646 ndis!ndisQuerySetMiniport+0x18
9c1f34a4  850dd9c8 ndis!ndisMDoMiniportOp+0x8c
9c1f34a8  850dd916 ndis!ndisMNotifyMachineName+0xe4
9c1f34ac  85104005 ndis!ndisMInitializeAdapter+0xad7
```

### <a name="fixing-the-cause-of-the-ndis-wifi-timeout-violation"></a>修复 NDIS WIFI 超时冲突的原因

为定时规则生成崩溃转储时，可能会在出现故障转储时找到根本原因的原因。 若要进一步调试，请考虑从 NdisKd 调试器扩展命令开始，请参阅 [NDIS 扩展 ( # A0) ](../debugger/ndis-extensions--ndiskd-dll-.md) 和 [NdisKd](/archive/blogs/ndis/getting-started-with-ndiskd)入门。 如果驱动程序实现了 ETW，还可能需要查看 [Windows (etw) 日志的事件跟踪 ](event-tracing-for-windows--etw-.md) 。 如果未启用此规则，则此错误将表现为用户应用程序挂起，或者 [**Bug 检查0x9F：驱动程序 \_ 电源 \_ 状态 \_ 故障**](../debugger/bug-check-0x9f--driver-power-state-failure.md) 。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[NDIS 扩展 (Ndiskd.dll)](../debugger/ndis-extensions--ndiskd-dll-.md)

[NDISKD 入门 (第1部分) ](/archive/blogs/ndis/getting-started-with-ndiskd)

[NDISKD 和！微型 (第2部分) ](/archive/blogs/ndis/ndiskd-and-miniport)

[用 NDISKD 调试 (第3部分) ](/archive/blogs/ndis/debugging-with-ndiskd)