---
title: KsIrqlPinCallbacks 规则 （)
description: KsIrqlPinCallbacks 规则指定内核流 (KS) 微型端口驱动程序返回从它必须在调用同一 IRQL KS Pin 回调函数。
ms.assetid: B2C1413A-9B94-499A-A15C-A943065F7CA1
ms.date: 05/21/2018
keywords:
- KsIrqlPinCallbacks 规则 （)
topic_type:
- apiref
api_name:
- KsIrqlPinCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6fe7185b93503fa00971a47321a423416536267d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392747"
---
# <a name="ksirqlpincallbacks-rule-"></a>KsIrqlPinCallbacks 规则 （)


KsIrqlPinCallbacks 规则指定内核流 (KS) 微型端口驱动程序返回从它必须在调用同一 IRQL KS Pin 回调函数。

**调试的提示**

当驱动程序验证程序检测到违反此规则时，它将触发[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)，与*arg1* 0x00081008 的值。 *Arg3* (RuleState) 和*了 arg4* （子状态） 的 bug 检查提供了指向有关的规则冲突的其他信息。

使用[ **！ ruleinfo** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)调试器扩展，以找出 IRQL 值已在函数入口和出口。

使用命令：

**!ruleinfo 0x81008** *RuleState* *SubState*.

在规则状态数据中， *OldIrql*是 IRQL 输入回调时。 *NewIrql*是 IRQL 回调函数退出时。

不要使用[ **！ irql** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-irql)以确定当前 IRQL，因为驱动程序验证程序可能具有的 IRQL 前引发 bug 检查。 请改用 **！ verifier 0x008**查看 IRQL 日志。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00081008) |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开命令提示符窗口。 输入驱动程序验证程序命令，并指定<strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





