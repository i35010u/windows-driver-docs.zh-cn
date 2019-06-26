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
ms.openlocfilehash: 08267523e06fc78e4384c38fc5b4747dcee5bfdf
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392119"
---
# <a name="ndisfiltertimeddatareceive-rule-ndis"></a>NdisFilterTimedDataReceive 规则 (ndis)


**NdisFilterTimedDataReceive**规则验证 NDIS 筛选器驱动程序完成的接收请求[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)之前函数否则将会超时。

内核调试程序可用于帮助确定问题的原因。 检查规则\_PendingNbl，指向最早的状态挂起[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)。 使用[ **！ ndiskd.nbl** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)调试器扩展。 有关使用调试程序的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00092012) |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a> ，然后选择<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 验证</a>选项。 此规则还经<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

 

 





