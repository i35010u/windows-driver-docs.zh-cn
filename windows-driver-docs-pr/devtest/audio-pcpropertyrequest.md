---
title: 'PcPropertyRequest 规则 (音频) '
description: PcPropertyRequest 规则指定 PortCls 微型端口驱动程序绝不应使用处于 "挂起" 状态的 NtStatus 值调用 PcCompletePendingPropertyRequest \_ 。
ms.date: 05/21/2018
keywords:
- 'PcPropertyRequest 规则 (音频) '
topic_type:
- apiref
api_name:
- PcPropertyRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1162f299cf655103a341e239e011829d0148e44b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790681"
---
# <a name="pcpropertyrequest-rule-audio"></a>PcPropertyRequest 规则 (音频) 


PcPropertyRequest 规则指定 PortCls 微型端口驱动程序绝不应使用处于 "挂起" 状态的 *NtStatus* 值调用 [**PcCompletePendingPropertyRequest**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest) \_ 。

**驱动程序模型：音频**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00071008) 


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em> &lt; yourdriver &gt; </em></p>
<p>有关详细信息，请参阅<a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

