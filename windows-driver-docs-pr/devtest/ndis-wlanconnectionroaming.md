---
title: WlanConnectionRoaming 规则（ndis）
description: WlanConnectionRoaming 规则验证微型端口驱动程序是否正确遵循了本机802.11 无线 LAN （WLAN）连接和漫游顺序。
ms.assetid: 7DB1881B-4DD8-4E06-AAF2-C6EAD0EEC5FC
ms.date: 05/21/2018
keywords:
- WlanConnectionRoaming 规则（ndis）
topic_type:
- apiref
api_name:
- WlanConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb603369a09f83e337075ac8a0cfacbe43b1f593
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968414"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming 规则（ndis）


**WlanConnectionRoaming**规则验证微型端口驱动程序是否正确遵循了本机802.11 无线 LAN （WLAN）连接和漫游顺序。

**驱动程序模型： NDIS**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00093005）


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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">驱动程序验证程序</a>，并选择<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**MiniportHaltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)另请参阅
--------

[常规连接操作指导原则](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines) 
[NDIS \_状态 \_ DOT11 \_ 连接 \_ 开始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-connection-start) 
 [OID \_ DOT11 \_ 重置 \_ 请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request) 
 [NDIS \_ 状态 \_ DOT11 \_ 漫游 \_ 启动](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-roaming-start)
 

 





