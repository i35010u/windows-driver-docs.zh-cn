---
title: NdisFilterTimedDataReceive 规则 (ndis)
description: NdisFilterTimedDataReceive 规则验证 NDIS 筛选器驱动程序通过在超时之前的 FilterReceiveNetBufferLists 函数来完成接收请求。
ms.assetid: B7B557F5-2D41-4F1F-9DE6-6BE23860A39E
ms.date: 05/21/2018
keywords:
- NdisFilterTimedDataReceive 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisFilterTimedDataReceive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6a682de2c757af9e5c6fe2b340433c609d7f49a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555697"
---
# <a name="ndisfiltertimeddatareceive-rule-ndis"></a>NdisFilterTimedDataReceive 规则 (ndis)


**NdisFilterTimedDataReceive**规则验证 NDIS 筛选器驱动程序完成的接收请求[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)之前函数否则将会超时。

内核调试程序可用于帮助确定问题的原因。 检查规则\_PendingNbl，指向最早的状态挂起[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)。 使用[ **！ ndiskd.nbl** ](https://msdn.microsoft.com/library/windows/hardware/ff564156)调试器扩展。 有关使用调试程序的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00092012) |

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

 

 

 





