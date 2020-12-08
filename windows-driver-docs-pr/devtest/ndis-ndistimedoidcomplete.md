---
title: 'NdisTimedOidComplete 规则 (ndis) '
description: NdisTimedOidComplete 规则指定 NDIS 微型端口驱动程序在12秒内完成 OID 请求。
ms.date: 05/21/2018
keywords:
- 'NdisTimedOidComplete 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisTimedOidComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e3514dcbbe90ff468a42e532b7518f4a9d20a63e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839749"
---
# <a name="ndistimedoidcomplete-rule-ndis"></a>NdisTimedOidComplete 规则 (ndis) 


**NdisTimedOidComplete** 规则指定 NDIS 微型端口驱动程序在12秒内完成 OID 请求。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x00092003) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 <a href="/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](./ndis-wifi-verification.md)">NDIS/WIFI 验证</a> 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**MiniportOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 
[ **NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)
