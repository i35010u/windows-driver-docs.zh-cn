---
title: NdisOidDoubleRequest 规则 (ndis)
description: 此 NdisOidDoubleRequest 规则验证微型端口驱动程序必须完成 NDIS\_OID\_当前处于挂起状态的请求。
ms.assetid: 67B179ED-EEAF-4717-B714-9601BE806269
ms.date: 05/21/2018
keywords:
- NdisOidDoubleRequest 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisOidDoubleRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07e91bf84ffbe9e8263d0b024caae355db992ae9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566653"
---
# <a name="ndisoiddoublerequest-rule-ndis"></a>NdisOidDoubleRequest 规则 (ndis)


这**NdisOidDoubleRequest**规则验证：

-   微型端口驱动程序必须完成[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)这是当前处于挂起状态。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0009100E) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用对象
----------

[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 

 





