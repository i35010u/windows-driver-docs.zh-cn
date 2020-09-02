---
title: 'WlanDisassociation 规则 (ndis) '
description: WlanDisassociation 规则验证微型端口驱动程序是否正确遵循了本机802.11 无线局域网 (WLAN) 解除相应的序列。
ms.assetid: E9C115D5-8522-4275-B874-1DB673AE23F2
ms.date: 05/21/2018
keywords:
- 'WlanDisassociation 规则 (ndis) '
topic_type:
- apiref
api_name:
- WlanDisassociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: addca1d33c81547625224b63212756a8696bd613
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381577"
---
# <a name="wlandisassociation-rule-ndis"></a>WlanDisassociation 规则 (ndis) 


**WlanDisassociation**规则验证微型端口驱动程序是否正确遵循了本机802.11 无线局域网 (WLAN) 解除相应的序列。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x00093006) 


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
 [ndis \_ 状态 \_ DOT11 \_ ](/previous-versions/windows/hardware/wireless/ndis-status-dot11-disassociation)解除 
 [ndis \_ 状态 \_ DOT11 \_ 关联 \_ 启动](/previous-versions/windows/hardware/wireless/ndis-status-dot11-association-start)
 

