---
title: 'PcPropertyRequest 规则 (音频) '
description: PcPropertyRequest 规则指定 PortCls 微型端口驱动程序绝不应使用处于 "挂起" 状态的 NtStatus 值调用 PcCompletePendingPropertyRequest \_ 。
ms.assetid: 7D06F924-512F-4D21-98CD-B9E60CC8A6AB
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
ms.openlocfilehash: c388f93d3d2bac86445ca3b6311f42dd4a24b09f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103982"
---
# <a name="pcpropertyrequest-rule-audio"></a>PcPropertyRequest 规则 (音频) 


PcPropertyRequest 规则指定 PortCls 微型端口驱动程序绝不应使用处于 "挂起" 状态的*NtStatus*值调用[**PcCompletePendingPropertyRequest**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest) \_ 。

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

 

