---
title: NdisTimedDataHang 规则 (ndis)
description: NdisTimedDataHang 规则验证 NDIS 微型端口驱动程序为 NET 处理任何挂起的发送请求\_缓冲区\_22 秒内的列表结构。
ms.assetid: CDFC9C23-B065-4916-BF1C-5429B6B57A23
ms.date: 05/21/2018
keywords:
- NdisTimedDataHang 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisTimedDataHang
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 960fa64c4f64193f69eddf09c9f69e3eae97dd9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382974"
---
# <a name="ndistimeddatahang-rule-ndis"></a>NdisTimedDataHang 规则 (ndis)


**NdisTimedDataHang**规则验证 NDIS 微型端口驱动程序处理的任何挂起的发送请求[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)22 秒内的结构。

微型端口驱动程序必须调用[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数来完成所有挂起的发送请求[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 如果有挂起的发送请求，NDIS 微型端口驱动程序必须继续完成它们。 至少一个挂起的发送请求时违反此规则**NET\_缓冲区\_列表**结构和任何此类发送已在过去的 22 数秒内完成的请求。

内核调试程序可用于帮助确定问题的原因。 检查规则\_PendingNbl，指向最早的状态挂起[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)。 使用[ **！ ndiskd.nbl** ](https://msdn.microsoft.com/library/windows/hardware/ff564156)调试器扩展。 有关使用调试程序的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0x0009200F) |

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

[**MiniportSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff559440)
[**NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)
 

 





