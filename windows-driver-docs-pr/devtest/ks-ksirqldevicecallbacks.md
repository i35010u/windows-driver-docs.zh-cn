---
title: KsIrqlDeviceCallbacks 规则（）
description: KsIrqlDeviceCallbacks 规则指定内核流式处理（KS）微型端口驱动程序从具有调用时所具有的相同 IRQL 的 KS 设备回调函数返回。
ms.assetid: 8C73EE2F-AA5B-478B-925A-C7DC4F6EFF6A
ms.date: 05/21/2018
keywords:
- KsIrqlDeviceCallbacks 规则（）
topic_type:
- apiref
api_name:
- KsIrqlDeviceCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 33133b0c19f1009b52e5e3041543f571b7f5fd9e
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968164"
---
# <a name="ksirqldevicecallbacks-rule-"></a>KsIrqlDeviceCallbacks 规则（）


KsIrqlDeviceCallbacks 规则指定内核流式处理（KS）微型端口驱动程序从具有调用时所具有的相同 IRQL 的 KS 设备回调函数返回。

**调试提示**

当驱动程序验证器检测到与该规则的冲突时，它将触发[**Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)， *arg1*值为0x00081006。 Bug 检查的*arg3* （RuleState）和*arg4* （子错误）提供指向有关规则冲突的其他信息的指针。

使用[**！ ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)调试器扩展来找出函数进入和退出时的 IRQL 值。

使用命令：

**！ ruleinfo 0x81006** *RuleState*子*情况。*

在规则状态数据中，输入回调时， *OldIrql*是 IRQL。 退出回调函数时， *NewIrql*是 IRQL。

不要使用[**！ irql**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-irql)来确定当前的 irql，因为驱动程序验证程序可能在 bug 检查前引发了 irql。 改为使用 **！ verifier 0x008**查看 IRQL 日志。

**驱动程序模型： KS**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00081006）


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定<strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em> &lt; &gt; yourdriver</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





