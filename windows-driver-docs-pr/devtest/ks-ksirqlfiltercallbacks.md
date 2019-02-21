---
title: KsIrqlFilterCallbacks rule ()
description: KsIrqlFilterCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 KS 筛选器回调函数具有相同的 IRQL 时调用回调函数。
ms.assetid: AC27FF93-DC7C-4287-B3D6-2579FAA65A77
ms.date: 05/21/2018
keywords:
- KsIrqlFilterCallbacks rule ()
topic_type:
- apiref
api_name:
- KsIrqlFilterCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69e38d2c95535a9f8fa934b8526a470798319d6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533443"
---
# <a name="ksirqlfiltercallbacks-rule-"></a>KsIrqlFilterCallbacks rule ()


KsIrqlFilterCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 KS 筛选器回调函数具有相同的 IRQL 时调用回调函数。

**调试的提示**

当驱动程序验证程序检测到违反此规则时，它将触发[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187)，与*arg1* 0x00081007 的值。 *Arg3* (RuleState) 和*了 arg4* （子状态） 的 bug 检查提供了指向有关的规则冲突的其他信息。

使用[ **！ ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374)调试器扩展，以找出 IRQL 值已在函数入口和出口。

使用命令：

**!ruleinfo 0x81007** *RuleState* *SubState*.

在规则状态数据中， *OldIrql*是 IRQL 输入回调时。 *NewIrql*是 IRQL 回调函数退出时。

不要使用[ **！ irql** ](https://msdn.microsoft.com/library/windows/hardware/ff563825)以确定当前 IRQL，因为驱动程序验证程序可能具有的 IRQL 前引发 bug 检查。 请改用 **！ verifier 0x008**查看 IRQL 日志。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081007) |

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
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





