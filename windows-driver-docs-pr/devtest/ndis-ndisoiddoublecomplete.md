---
title: 'NdisOidDoubleComplete 规则 (ndis) '
description: NdisOidDoubleComplete 规则指定 NDIS 微型端口驱动程序不得为同一 OID 调用两次 NdisMOidRequestComplete 例程。
ms.assetid: 876A3D3C-554F-4D71-AD1B-F568D0AD6C0D
ms.date: 05/21/2018
keywords:
- 'NdisOidDoubleComplete 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisOidDoubleComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d95276a6f7a91bb2e955745401a313d4c5399f73
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382937"
---
# <a name="ndisoiddoublecomplete-rule-ndis"></a>NdisOidDoubleComplete 规则 (ndis) 


**NdisOidDoubleComplete**规则指定 NDIS 微型端口驱动程序不得为同一 OID 调用两次[**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)例程。

将跟踪 OID ( 跟踪的 \_ 对象) 。 若要使用内核调试器帮助调试此错误，请使用 **！ ndiskd** 调试器扩展。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x00091002) 


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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](./ndis-wifi-verification.md)">NDIS/WIFI 验证</a> 选项。 此规则也会用 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> 选项进行测试。</p></td>
</tr>
</tbody>
</table>

 

.

<a name="applies-to"></a>适用于
----------

[**MiniportOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 
[ **NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)
 

