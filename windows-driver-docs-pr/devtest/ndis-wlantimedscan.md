---
title: WlanTimedScan 规则（ndis）
description: WlanTimedScan 规则验证 WLAN 扫描操作是否在15秒内完成。
ms.assetid: 6BFA0DAD-00A4-43EB-A226-40E1B0892E91
ms.date: 05/21/2018
keywords:
- WlanTimedScan 规则（ndis）
topic_type:
- apiref
api_name:
- WlanTimedScan
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e3967b72625acc6e23cdcb9a04101ebdb6bb91e4
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916205"
---
# <a name="wlantimedscan-rule-ndis"></a>WlanTimedScan 规则（ndis）


**WlanTimedScan**规则验证 WLAN 扫描操作是否在15秒内完成。

**驱动程序模型： NDIS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x0009400C） |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">驱动程序验证程序</a>，并选择<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**MiniportHaltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 
[**MiniportOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)另请参阅
--------

[常规连接操作指导原则](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines) 
[OID \_DOT11 \_ 连接 \_ 请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-connect-request) 
 [NDIS \_ 状态 \_ DOT11 \_ 连接 \_ 启动](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-connection-start)
 

 





