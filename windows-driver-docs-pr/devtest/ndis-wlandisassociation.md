---
title: WlanDisassociation 规则（ndis）
description: WlanDisassociation 规则验证微型端口驱动程序是否正确遵循了本机802.11 无线 LAN （WLAN）解除相应顺序。
ms.assetid: E9C115D5-8522-4275-B874-1DB673AE23F2
ms.date: 05/21/2018
keywords:
- WlanDisassociation 规则（ndis）
topic_type:
- apiref
api_name:
- WlanDisassociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa2323c7e756887fbfb8a9d3d4cf55428049e8e7
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916929"
---
# <a name="wlandisassociation-rule-ndis"></a>WlanDisassociation 规则（ndis）


**WlanDisassociation**规则验证微型端口驱动程序是否正确遵循了本机802.11 无线 LAN （WLAN）解除相应顺序。

**驱动程序模型： NDIS**

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00093006） |

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
[OID \_DOT11 \_ 重置 \_ 请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request) 
 [ndis \_ 状态 \_ DOT11 \_ ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-disassociation)解除 
 [ndis \_ 状态 \_ DOT11 \_ 关联 \_ 启动](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-start)
 

 





