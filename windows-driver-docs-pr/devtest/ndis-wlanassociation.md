---
title: 'WlanAssociation 规则 (ndis) '
description: WlanAssociation 规则验证微型端口驱动程序是否正确地遵从了本机802.11 无线局域网 (WLAN) 关联序列。
ms.assetid: 3F457C06-29F1-4730-92D5-5B98CD459FD1
ms.date: 05/21/2018
keywords:
- 'WlanAssociation 规则 (ndis) '
topic_type:
- apiref
api_name:
- WlanAssociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b0721020df3e67175cc399d0c994c87a46b6b50d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381587"
---
# <a name="wlanassociation-rule-ndis"></a>WlanAssociation 规则 (ndis) 


**WlanAssociation**规则验证微型端口驱动程序是否正确地遵从了本机802.11 无线局域网 (WLAN) 关联序列。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x00093004) 


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
[OID \_DOT11 \_ 重置 \_ 请求](/previous-versions/windows/hardware/wireless/oid-dot11-reset-request) 
 [NDIS \_ 状态 \_ DOT11 \_ 关联 \_ 启动](/previous-versions/windows/hardware/wireless/ndis-status-dot11-association-start)
 

