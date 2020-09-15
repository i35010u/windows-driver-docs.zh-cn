---
title: 'NdisOidDoubleRequest 规则 (ndis) '
description: 此 NdisOidDoubleRequest 规则验证 Minport 驱动程序必须完成 \_ 当前挂起的 NDIS OID \_ 请求。
ms.assetid: 67B179ED-EEAF-4717-B714-9601BE806269
ms.date: 05/21/2018
keywords:
- 'NdisOidDoubleRequest 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisOidDoubleRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 21137c12d0ecd16c9e2404cdc73862ae883023ec
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102872"
---
# <a name="ndisoiddoublerequest-rule-ndis"></a>NdisOidDoubleRequest 规则 (ndis) 


此 **NdisOidDoubleRequest** 规则验证：

-   Minport 驱动程序必须完成当前挂起的 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x0009100E) 


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
