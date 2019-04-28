---
title: 调试 DRIVER_VERIFIER_DETECTED_VIOLATION (C4)
description: 驱动程序验证程序检测到驱动程序违反了某个 NDIS/WiFi 超时规则。
ms.assetid: 73D4B6DF-E667-4C71-B985-FCDC05837908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 556d04d6c369ab9c5efb8600eac68345845463a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344865"
---
# <a name="debugging-ndiswifi-time-out-errors---driververifierdetectedviolation-c4"></a>调试 NDIS/WiFi 超时错误的驱动程序\_VERIFIER\_检测到\_冲突 (C4)


当你具有[NDIS/WIFI 验证](ndis-wifi-verification.md)选择选项，并且驱动程序验证程序检测到驱动程序违反了某个 NDIS/WiFi 超时规则[Driver Verifier](driver-verifier.md)生成[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) （参数 1 等于为特定的 NDIS/WiFi 超时规则的标识符）。

Driver Verifier 测试时 NDIS/WIFI 超时规则，如[ **NdisTimedOidComplete**](https://msdn.microsoft.com/library/windows/hardware/dn305120)，驱动程序验证程序的轮询机制需要在一定数目的周期内的微型端口驱动程序的响应。 每个定时的规则定义了其自己允许的最大周期。 当超过最大值时，驱动程序验证程序生成的 bug 检查。 本部分介绍调试这些冲突的一些示例策略。

## <a name="debugging-ndiswifi-timeout-errors"></a>调试 NDIS/WIFI 超时错误


-   [使用 ！ 分析以显示 bug 检查有关的信息](#use-analyze-to-display-information-about-the-bug-check)
-   [使用 ！ ruleinfo 扩展命令](#use-the-ruleinfo-extension-command)
-   [单击最后一个\_调用\_堆栈链接，来识别冲突的位置](#identify-the-location-of-the-violation)
-   [修复 NDIS/WIFI 超时冲突的原因](#fixing-the-cause-of-the-ndis-wifi-timeout-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用 ！ 分析以显示 bug 检查有关的信息

最佳的第一步是运行后可以控制在调试器中出现任何错误检查，与一样[ **！ 分析-v** ](https://msdn.microsoft.com/library/windows/hardware/ff562112)命令。

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

下一节中 **！ 分析-v**输出，原因违反这一规则下的原因显示下 DV\_VIOLATED\_条件字段。 DV\_MSDN\_链接部分也是很有用的链接提取到有关此规则的文档。

```
## Debugging Details:


*** ERROR: Module load completed but symbols could not be loaded for NdisTimedOidComplete.sys

DV_VIOLATED_CONDITION:  Timeout on completing an NDIS OID request.

DV_MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278804

DRIVER_OBJECT: 98a87980

IMAGE_NAME:  NdisTimedOidComplete.sys

DEBUG_FLR_IMAGE_TIMESTAMP:  5229c857

MODULE_NAME: NdisTimedOidComplete

FAULTING_MODULE: 9fee1000 NdisTimedOidComplete
```

进一步下此分析输出，您可以单击链接下 dv 摄\_规则\_信息部分，了解其他规则的说明。 对于超时类型的规则，当前堆栈可能不包含相关信息。

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

### <a name="use-the-ruleinfo-extension-command"></a>使用 ！ ruleinfo 扩展命令

**DV\_规则\_信息：** 字段 **！ 分析**输出显示到命令可用于查找有关此规则冲突的详细信息的链接。 对于此示例中，如果单击该链接，它将运行[ **！ ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374)命令与规则\_ID (0x92003) Arg3 和 Arg 4 bug 检查值。

```
kd> !ruleinfo 0x92003 0xffffffff9c17b860 0xffffffff9c1f3480

RULE_ID: 0x92003

RULE_NAME: NdisTimedOidComplete

RULE_DESCRIPTION:
This rule verifies if an NDIS miniport driver completes an OID in time.
The OID is tracked (a.k.a., TRACKED_OBJECT). Use !ndiskd.oid .

MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278804

CONTEXT: Miniport 0x86BD10E8

CURRENT_TIME (Timed Rules): 168 seconds

TRACKED_OBJECT: 0x86633804

LAST_CALL_STACK: 0x9C1F3480 + 0x10

RULE_STATE: 0x9C1F3480
```

### <a name="identify-the-location-of-the-violation"></a>标识冲突的位置

在示例中我们将在这里，微型端口驱动程序，NdisTimedOidComplete.sys，具有睡眠周期注入到其*MPOidRequest*函数。 我们可以通过单击的最后一个检查\_调用\_堆栈中的链接[ **！ ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374)输出。 这是最后一个调用堆栈看到的驱动程序验证程序，我们看到，调用 NDIS *ndisMInvokeOidRequest*发生超时之前。

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

### <a name="fixing-the-cause-of-the-ndis-wifi-timeout-violation"></a>修复超时冲突的 NDIS WIFI 的原因

当已为计时规则生成故障转储时，则可能可以在故障转储的时间找到根本原因的。 若要进一步调试，请考虑从开始 NdisKd 调试器扩展命令，请参阅[NDIS 扩展 (Ndiskd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff552270)并[入门 NDISKD](https://go.microsoft.com/fwlink/p/?linkid=327569)。 您可能还需要看一下[事件跟踪 Windows (ETW)](event-tracing-for-windows--etw-.md)日志，如果您的驱动程序已实现 ETW。 如果未启用此规则，此错误将表现为用户应用程序挂起，或者[ **Bug 检查 0x9F:驱动程序\_电源\_状态\_失败**](https://msdn.microsoft.com/library/windows/hardware/ff559329)在最差。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[NDIS 扩展 (Ndiskd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff552270)

[开始使用 NDISKD （第 1 部分）](https://go.microsoft.com/fwlink/p/?linkid=327569)

[NDISKD 和 ！ 微型端口 （第 2 部分）]( https://go.microsoft.com/fwlink/p/?linkid=327570)

[使用 NDISKD （第 3 部分） 进行调试](https://go.microsoft.com/fwlink/p/?linkid=327571)










