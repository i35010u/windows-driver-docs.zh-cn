---
title: 'NdisFilterTimedPauseComplete 规则 (ndis) '
description: NdisFilterTimedPauseComplete 验证三项 FilterPause 函数将在10秒或更短时间内完成。FilterPause 函数不能失败。FilterPause 函数不得完成两次。
ms.date: 05/21/2018
keywords:
- 'NdisFilterTimedPauseComplete 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisFilterTimedPauseComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c907c0ecd1e7d52e93ca5b15da47e6c0b88dd26b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838997"
---
# <a name="ndisfiltertimedpausecomplete-rule-ndis"></a>NdisFilterTimedPauseComplete 规则 (ndis) 


**NdisFilterTimedPauseComplete** 验证三个方面：

-   [*FilterPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)函数将在10秒或更短时间内完成。

-   [*FilterPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)函数不能失败。

-   [*FilterPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)函数不得完成两次。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x00092010) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 <a href="/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](./ndis-wifi-verification.md)">NDIS/WIFI 验证</a> 选项。 此规则也会用 <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> 选项进行测试。</p></td>
</tr>
</tbody>
</table>

 

