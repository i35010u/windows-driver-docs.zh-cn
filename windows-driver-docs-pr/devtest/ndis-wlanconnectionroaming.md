---
title: 'WlanConnectionRoaming 规则 (ndis) '
description: WlanConnectionRoaming 规则验证微型端口驱动程序是否正确地遵从了本机802.11 无线局域网 (WLAN) 连接和漫游顺序。
ms.assetid: 7DB1881B-4DD8-4E06-AAF2-C6EAD0EEC5FC
ms.date: 05/21/2018
keywords:
- 'WlanConnectionRoaming 规则 (ndis) '
topic_type:
- apiref
api_name:
- WlanConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 892db026e9a782b899b9327db9c0f13cc080162a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107448"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming 规则 (ndis) 


**WlanConnectionRoaming**规则验证微型端口驱动程序是否正确地遵从了本机802.11 无线局域网 (WLAN) 连接和漫游顺序。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x00093005) 


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
[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)另请参阅
--------

[常规连接操作指导原则](/previous-versions/windows/hardware/wireless/general-connection-operation-guidelines) 
[NDIS \_状态 \_ DOT11 \_ 连接 \_ 开始](/previous-versions/windows/hardware/wireless/ndis-status-dot11-connection-start) 
 [OID \_ DOT11 \_ 重置 \_ 请求](/previous-versions/windows/hardware/wireless/oid-dot11-reset-request) 
 [NDIS \_ 状态 \_ DOT11 \_ 漫游 \_ 启动](/previous-versions/windows/hardware/wireless/ndis-status-dot11-roaming-start)
