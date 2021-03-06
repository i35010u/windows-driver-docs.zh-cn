---
title: 'NdisFilterTimedDataReceive 规则 (ndis) '
description: NdisFilterTimedDataReceive 规则验证 NDIS 筛选器驱动程序在超时前是否通过 FilterReceiveNetBufferLists 函数完成了接收请求。
ms.date: 05/21/2018
keywords:
- 'NdisFilterTimedDataReceive 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisFilterTimedDataReceive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 46e7f2a6d9464abb0c9d179bf368eec418f4e413
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248481"
---
# <a name="ndisfiltertimeddatareceive-rule-ndis"></a>NdisFilterTimedDataReceive 规则 (ndis) 


**NdisFilterTimedDataReceive** 规则验证 NDIS 筛选器驱动程序在超时前是否通过 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)函数完成了接收请求。

您可以使用内核调试器来帮助确定问题的原因。 检查 PendingNbl 的规则 \_ 状态，该状态指向最早的挂起 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)。 使用 [**！ ndiskd**](../debugger/-ndiskd-nbl.md) 调试程序扩展。 有关使用调试器的信息，请参阅 [Windows 调试](../debugger/index.md)。

**驱动程序模型： NDIS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) ( 0x00092012) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 <a href="/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](./ndis-wifi-verification.md)">NDIS/WIFI 验证</a> 选项。 此规则也会用 <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> 选项进行测试。</p></td>
</tr>
</tbody>
</table>

 

