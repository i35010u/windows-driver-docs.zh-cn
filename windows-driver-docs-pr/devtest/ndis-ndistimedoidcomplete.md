---
title: NdisTimedOidComplete 规则（ndis）
description: NdisTimedOidComplete 规则指定 NDIS 微型端口驱动程序在12秒内完成 OID 请求。
ms.assetid: 8C395BCA-4B9E-4302-BF6D-FD79809EB187
ms.date: 05/21/2018
keywords:
- NdisTimedOidComplete 规则（ndis）
topic_type:
- apiref
api_name:
- NdisTimedOidComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfd7b356bf3336dc288b4573eec78562d7fc1b20
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839358"
---
# <a name="ndistimedoidcomplete-rule-ndis"></a>NdisTimedOidComplete 规则（ndis）


**NdisTimedOidComplete**规则指定 NDIS 微型端口驱动程序在12秒内完成 OID 请求。

|              |      |
|--------------|------|
| 驱动程序型号 | 以此 |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：检测到\_冲突的驱动程序\_验证程序\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) （0x00092003） |

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

[**MiniportOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)
[ **NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)
 

 





