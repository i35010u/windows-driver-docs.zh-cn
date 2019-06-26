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
ms.openlocfilehash: 4bff0b526eecb989f8af157405bdc7e115eef4f2
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392196"
---
# <a name="ndistimeddatahang-rule-ndis"></a>NdisTimedDataHang 规则 (ndis)


**NdisTimedDataHang**规则验证 NDIS 微型端口驱动程序处理的任何挂起的发送请求[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)22 秒内的结构。

微型端口驱动程序必须调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数来完成所有挂起的发送请求[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 如果有挂起的发送请求，NDIS 微型端口驱动程序必须继续完成它们。 至少一个挂起的发送请求时违反此规则**NET\_缓冲区\_列表**结构和任何此类发送已在过去的 22 数秒内完成的请求。

内核调试程序可用于帮助确定问题的原因。 检查规则\_PendingNbl，指向最早的状态挂起[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)。 使用[ **！ ndiskd.nbl** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)调试器扩展。 有关使用调试程序的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x0x0009200F) |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a> ，然后选择<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用对象
----------

[**MiniportSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)
[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)
 

 





