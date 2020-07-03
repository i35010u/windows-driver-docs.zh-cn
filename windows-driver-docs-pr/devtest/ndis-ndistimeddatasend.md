---
title: NdisTimedDataSend 规则（ndis）
description: NdisTimedDataSend 规则验证当 NDIS 驱动程序调用 MiniportSendNetBufferLists 时，微型端口驱动程序在30秒内完成了发送请求。
ms.assetid: 2240254E-4381-4009-ACF2-DA481CB065FE
ms.date: 05/21/2018
keywords:
- NdisTimedDataSend 规则（ndis）
topic_type:
- apiref
api_name:
- NdisTimedDataSend
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 045e68b583588c8db723eddbe91d6e5fa043cc70
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916319"
---
# <a name="ndistimeddatasend-rule-ndis"></a>NdisTimedDataSend 规则（ndis）


**NdisTimedDataSend**规则验证当 NDIS 驱动程序调用[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)时，微型端口驱动程序在30秒内完成了发送请求。

您可以使用内核调试器来帮助确定问题的原因。 检查 PendingNbl 的规则 \_ 状态，它指向导致超时的挂起缓冲区列表。 使用[**！ ndiskd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)调试程序扩展来检查[**NET \_ BUFFER \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)。 有关使用调试器的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

**驱动程序模型： NDIS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x0009200D） |

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

[**MiniportSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 
[ **NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)
 

 





