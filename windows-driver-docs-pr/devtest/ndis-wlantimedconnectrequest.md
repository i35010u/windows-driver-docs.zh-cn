---
title: 'WlanTimedConnectRequest 规则 (ndis) '
description: WlanTimedConnectRequest 规则验证 OID \_ DOT11 \_ CONNECT \_ 请求后跟 NDIS \_ STATUS \_ DOT11 \_ 连接是否 \_ 在10秒内启动。
ms.assetid: F40D92B1-CA48-4060-B9E2-A965900EAF7B
ms.date: 05/21/2018
keywords:
- 'WlanTimedConnectRequest 规则 (ndis) '
topic_type:
- apiref
api_name:
- WlanTimedConnectRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e2722440b652c0f4cac6501021b1335f38215bdc
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381565"
---
# <a name="wlantimedconnectrequest-rule-ndis"></a>WlanTimedConnectRequest 规则 (ndis) 


**WlanTimedConnectRequest**规则验证 OID \_ DOT11 \_ CONNECT \_ 请求后跟 NDIS \_ STATUS \_ DOT11 \_ 连接是否 \_ 在10秒内启动。

此外， \_ \_ \_ \_ 仅当 OID \_ DOT11 \_ 连接 \_ 请求在 ndis \_ 状态 \_ 成功完成时，才会指示 ndis 状态 DOT11 连接开始。 此规则仅适用于 (端口 0) 的可扩展工作站端口。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00094009) 


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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](./ndis-wifi-verification.md)">NDIS/WIFI 验证</a> 选项。</p></td>
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

[常规连接操作指导原则](/previous-versions/windows/hardware/wireless/general-connection-operation-guidelines)
 

