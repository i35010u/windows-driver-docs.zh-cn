---
title: ruleinfo
description: Ruleinfo 命令显示有关驱动程序验证程序规则的信息。
ms.assetid: 025FAAFA-7A5C-462C-9CC2-AA55530CD371
keywords:
- ruleinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ruleinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 04c852ebeca9cf09f0303a60cb957c76d8137391
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534708"
---
# <a name="ruleinfo"></a>!ruleinfo


**！ Ruleinfo**命令显示有关驱动程序验证程序规则的信息。

```dbgcmd
!ruleinfo RuleId [RuleState [SubState]]
```

## <a name="span-idddk__ptov_dbgspanspan-idddk__ptov_dbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>参数


<span id="_______RuleId______"></span><span id="_______ruleid______"></span><span id="_______RULEID______"></span>*RuleId*   
验证程序规则的 ID。 这是[**驱动程序 \_ 验证程序 \_ 检测到 \_ 违反**](bug-check-0xc4--driver-verifier-detected-violation.md)bug 检查的第一个参数。

<span id="_______RuleState______"></span><span id="_______rulestate______"></span><span id="_______RULESTATE______"></span>*RuleState*   
有关冲突的其他状态信息。 这是**驱动程序 \_ 验证程序 \_ 检测到 \_ 违反**bug 检查的第三个参数。

<span id="_______SubState______"></span><span id="_______substate______"></span><span id="_______SUBSTATE______"></span>*SubState*子情况   
有关冲突的子状态信息。 这是**驱动程序 \_ 验证程序 \_ 检测到的 \_ 冲突**bug 检查的第四个参数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

ext .dll

<a name="remarks"></a>注解
-------

此命令仅适用于驱动程序验证程序扩展中的规则;也就是说，ID 大于或等于0x10000 的规则。

以下示例显示了[**驱动程序 \_ 验证程序 \_ 检测到 \_ 违反**](bug-check-0xc4--driver-verifier-detected-violation.md)bug 检查的四个参数。

```dbgcmd
DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
...
Arguments:
Arg1: 0000000000091001, ID of the 'NdisOidComplete' rule that was violated.
Arg2: fffff800002d49d0, A pointer to the string describing the violated rule condition.
Arg3: ffffe000027b8370, Address of internal rule state (second argument to !ruleinfo).
Arg4: ffffe000027b83f8, Address of supplemental states (third argument to !ruleinfo).

## Debugging Details:


DV_VIOLATED_CONDITION:  This OID should only be completed with NDIS_STATUS_NOT_ACCEPTED, 
                        NDIS_STATUS_SUCCESS, or NDIS_STATUS_PENDING.

DV_MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278802

DRIVER_OBJECT: ffffe0000277a2b0
...

STACK_TEXT:  
ffffd000`2118ff58 fffff803`4c83afa2 : 00000000`000000c4 00000000`00000001 ...
ffffd000`2118ff60 fffff803`4c83a8c0 : 00000000`00000003 00000000`00091001 ...
...

STACK_COMMAND:  kb

FOLLOWUP_NAME:  Xxxx

FAILURE_BUCKET_ID:  Xxxx
...
```

在上面的输出中，规则 ID （0x91001）显示为 Arg1。 Arg3 和 Arg4 是规则状态和子状态信息的地址。 您可以将规则 ID、规则状态和子状态传递到 **！ ruleinfo** ，以获取规则的说明以及指向规则的详细文档的链接。

```dbgcmd
3: kd> !ruleinfo 0x91001 0xffffe000027b8370 0xffffe000027b83f8

RULE_ID: 0x91001

RULE_NAME: NdisOidComplete

RULE_DESCRIPTION:
This rule verifies if an NDIS miniport driver completes an OID correctly.
Check RULE_STATE for Oid ( use !ndiskd.oid ), which can be one of the following:
1) NULL,
2) Pending OID, or
3) Previous OID if no OID is pending.

MSDN_LINK: https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete

CONTEXT: Miniport 0xFFFFE0000283F1A0

CURRENT_TIME (Timed Rules): 142 seconds

RULE_STATE: 0xFFFFE000027B83F8
```

 

 





