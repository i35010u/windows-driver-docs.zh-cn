---
title: 'PcIrqlIport 规则 (音频) '
description: PcIrqlIport 规则指定 PortCls 微型端口驱动程序必须在正确的 IRQL 级别调用 PortCls IPort 接口。
ms.assetid: 59E22F37-3377-4B98-8613-EF5ED0CB63D9
ms.date: 05/21/2018
keywords:
- 'PcIrqlIport 规则 (音频) '
topic_type:
- apiref
api_name:
- PcIrqlIport
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a779b6d7a11983df6b0fd48c989452127ca32e9
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383835"
---
# <a name="pcirqliport-rule-audio"></a>PcIrqlIport 规则 (音频) 


PcIrqlIport 规则指定 PortCls 微型端口驱动程序必须在正确的 IRQL 级别调用 PortCls IPort 接口。

**驱动程序模型：音频**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00071003) 


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
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

 

