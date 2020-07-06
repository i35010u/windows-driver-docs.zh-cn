---
title: PcIrqlDDIs 规则（音频）
description: PcIrqlDDIs 规则指定 PortCls 微型端口驱动程序必须在正确的 IRQL 级别调用 PortCls DDIs。
ms.assetid: 7CBC8407-FE46-449F-B921-883BCDA0436B
ms.date: 05/21/2018
keywords:
- PcIrqlDDIs 规则（音频）
topic_type:
- apiref
api_name:
- PcIrqlDDIs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b275bd654b0c71de58e1e135d0eb16ef198d7cde
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968416"
---
# <a name="pcirqlddis-rule-audio"></a>PcIrqlDDIs 规则（音频）


PcIrqlDDIs 规则指定 PortCls 微型端口驱动程序必须在正确的 IRQL 级别调用 PortCls DDIs。

**驱动程序模型：音频**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00071001）


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定<strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em> &lt; yourdriver &gt; </em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





