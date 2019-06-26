---
title: KsIrqlDeviceCallbacks 规则 （)
description: KsIrqlDeviceCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 KS 设备回调函数具有相同的 IRQL 时调用。
ms.assetid: 8C73EE2F-AA5B-478B-925A-C7DC4F6EFF6A
ms.date: 05/21/2018
keywords:
- KsIrqlDeviceCallbacks 规则 （)
topic_type:
- apiref
api_name:
- KsIrqlDeviceCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: df29778d132bde2e1cd6b4ec24d8759787e289da
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392762"
---
# <a name="ksirqldevicecallbacks-rule-"></a>KsIrqlDeviceCallbacks 规则 （)


KsIrqlDeviceCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 KS 设备回调函数具有相同的 IRQL 时调用。

**调试的提示**

当驱动程序验证程序检测到违反此规则时，它将触发[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)，与*arg1* 0x00081006 的值。 *Arg3* (RuleState) 和*了 arg4* （子状态） 的 bug 检查提供了指向有关的规则冲突的其他信息。

使用[ **！ ruleinfo** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)调试器扩展，以找出 IRQL 值已在函数入口和出口。

使用命令：

**!ruleinfo 0x81006** *RuleState* *SubState*.

在规则状态数据中， *OldIrql*是 IRQL 输入回调时。 *NewIrql*是 IRQL 回调函数退出时。

不要使用[ **！ irql** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-irql)以确定当前 IRQL，因为驱动程序验证程序可能具有的 IRQL 前引发 bug 检查。 请改用 **！ verifier 0x008**查看 IRQL 日志。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00081006) |

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

 

 

 





