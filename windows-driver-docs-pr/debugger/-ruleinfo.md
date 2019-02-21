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
ms.openlocfilehash: 3c4b75b692992085c20b7988766b4d46b4b49eef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547431"
---
# <a name="ruleinfo"></a>！ ruleinfo


**！ Ruleinfo**命令显示有关驱动程序验证程序规则的信息。

```dbgcmd
!ruleinfo RuleId [RuleState [SubState]]
```

## <a name="span-idddkptovdbgspanspan-idddkptovdbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>参数


<span id="_______RuleId______"></span><span id="_______ruleid______"></span><span id="_______RULEID______"></span> *RuleId*   
验证程序规则的 ID。 这是第一个参数的[**驱动程序\_VERIFIER\_已检测\_冲突**](bug-check-0xc4--driver-verifier-detected-violation.md) bug 检查。

<span id="_______RuleState______"></span><span id="_______rulestate______"></span><span id="_______RULESTATE______"></span> *RuleState*   
有关冲突的其他状态信息。 这是第三个参数**驱动程序\_VERIFIER\_检测到\_冲突**bug 检查。

<span id="_______SubState______"></span><span id="_______substate______"></span><span id="_______SUBSTATE______"></span> *SubState*   
有关冲突的子状态信息。 这是第四个参数的**驱动程序\_VERIFIER\_检测到\_冲突**bug 检查。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ext.dll

<a name="remarks"></a>备注
-------

此命令仅适用于驱动程序验证工具扩展中; 中的规则也就是说，规则，具有一个大于或等于 0x10000 的 ID。

下面的示例演示的四个参数[**驱动程序\_VERIFIER\_已检测\_冲突**](bug-check-0xc4--driver-verifier-detected-violation.md) bug 检查。

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

在上面的输出中 Arg1 显示规则 ID (0x91001)。 Arg3 和了 Arg4 规则状态和 substate 信息的地址。 可以传递规则 ID、 规则状态和到的子状态 **！ ruleinfo**若要获取该规则和规则的详细文档的链接的说明。

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

MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278802

CONTEXT: Miniport 0xFFFFE0000283F1A0

CURRENT_TIME (Timed Rules): 142 seconds

RULE_STATE: 0xFFFFE000027B83F8
```

 

 





