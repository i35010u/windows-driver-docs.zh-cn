---
title: NdisTimedDataHang 规则（ndis）
description: NdisTimedDataHang 规则验证 NDIS 微型端口驱动程序是否 \_ \_ 在22秒内处理网络缓冲区列表结构的任何挂起发送请求。
ms.assetid: CDFC9C23-B065-4916-BF1C-5429B6B57A23
ms.date: 05/21/2018
keywords:
- NdisTimedDataHang 规则（ndis）
topic_type:
- apiref
api_name:
- NdisTimedDataHang
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76e3042bf237772c2473acd17c3fbb7b4ef2e68d
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967928"
---
# <a name="ndistimeddatahang-rule-ndis"></a>NdisTimedDataHang 规则（ndis）


**NdisTimedDataHang**规则验证 NDIS 微型端口驱动程序是否在22秒内处理[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的任何挂起发送请求。

微型端口驱动程序必须调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数来完成所有[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的挂起发送请求。 如果有挂起的发送请求，NDIS 微型端口驱动程序必须继续完成这些请求。 如果**网络 \_ 缓冲区 \_ 列表**结构至少有一个挂起的发送请求，但在过去22秒内没有完成此类发送请求，则将违反此规则。

您可以使用内核调试器来帮助确定问题的原因。 检查 PendingNbl 的规则 \_ 状态，该状态指向最早的挂起[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)。 使用[**！ ndiskd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)调试程序扩展。 有关使用调试器的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

**驱动程序模型： NDIS**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x0x0009200F）


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
 

 





