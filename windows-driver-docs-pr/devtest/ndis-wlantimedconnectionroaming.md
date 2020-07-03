---
title: WlanTimedConnectionRoaming 规则（ndis）
description: WlanTimedConnectionRoaming 规则指定 NDIS 微型端口驱动程序在10秒内完成无线 LAN （WLAN）连接/漫游操作。
ms.assetid: 0961C34B-FAD8-49ED-A0FD-5D790E973C4D
ms.date: 05/21/2018
keywords:
- WlanTimedConnectionRoaming 规则（ndis）
topic_type:
- apiref
api_name:
- WlanTimedConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e66b2a278e1fd426e996765497c876fdd864ebe5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916919"
---
# <a name="wlantimedconnectionroaming-rule-ndis"></a>WlanTimedConnectionRoaming 规则（ndis）


**WlanTimedConnectionRoaming**规则指定 NDIS 微型端口驱动程序在10秒内完成无线 LAN （WLAN）连接/漫游操作。

**驱动程序模型： NDIS**

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00094008） |

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
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)另请参阅
--------

[常规连接操作指导原则](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)
 

 





