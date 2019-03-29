---
title: NdisOidDoubleComplete 规则 (ndis)
description: NdisOidDoubleComplete 规则指定 NDIS 微型端口驱动程序必须为相同的 OID 两次调用 NdisMOidRequestComplete 例程。
ms.assetid: 876A3D3C-554F-4D71-AD1B-F568D0AD6C0D
ms.date: 05/21/2018
keywords:
- NdisOidDoubleComplete 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisOidDoubleComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: affe756a47d4c3dd5d15ed569cbdf806d41f7a29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567225"
---
# <a name="ndisoiddoublecomplete-rule-ndis"></a>NdisOidDoubleComplete 规则 (ndis)


**NdisOidDoubleComplete**规则指定 NDIS 微型端口驱动程序必须调用[ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)例程两次以相同的 OID。

跟踪 OID (跟踪\_对象)。 若要帮助调试使用内核调试程序的此错误，请使用 **！ ndiskd.oid**调试器扩展。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00091002) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 验证</a>选项。 此规则还经<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

.

<a name="applies-to"></a>适用对象
----------

[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 

 





