---
title: 'WlanTimedLinkQuality 规则 (ndis) '
description: WlanTimedLinkQuality 规则指定 \_ \_ \_ \_ 在成功 ndis \_ 状态 \_ DOT11 \_ 关联完成后15秒内发生的 NDIS 状态 DOT11 链接质量指示 \_ 。
ms.date: 05/21/2018
keywords:
- 'WlanTimedLinkQuality 规则 (ndis) '
topic_type:
- apiref
api_name:
- WlanTimedLinkQuality
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6a5047c9bedda81c1e1db767a245fee0348f99e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791931"
---
# <a name="wlantimedlinkquality-rule-ndis"></a>WlanTimedLinkQuality 规则 (ndis) 


**WlanTimedLinkQuality** 规则指定 \_ \_ \_ \_ 在成功 ndis \_ 状态 \_ DOT11 \_ 关联完成后15秒内发生的 NDIS 状态 DOT11 链接质量指示 \_ 。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x0009400B) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[NDIS/WIFI verification](./ddi-compliance-checking.md)">NDIS/WIFI 验证</a> 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**MiniportHaltEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 
[**MiniportOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 
[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 
[**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)另请参阅
--------

[NDIS \_ 状态 \_ DOT11 \_ 链接 \_ 质量](/previous-versions/windows/hardware/wireless/ndis-status-dot11-link-quality)
