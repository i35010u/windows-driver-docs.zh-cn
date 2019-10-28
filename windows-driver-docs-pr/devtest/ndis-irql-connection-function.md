---
title: Irql\_连接\_函数规则（ndis）
description: Irql\_连接\_函数规则指定必须在正确的 IRQL 级别调用协议驱动程序的 NDIS 连接函数。
ms.assetid: 9721cb8a-ac70-4f2b-8bbd-809dc06548dc
ms.date: 05/21/2018
keywords:
- Irql_Connection_Function 规则（ndis）
topic_type:
- apiref
api_name:
- Irql_Connection_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4e47b88319e890892c262e616a3d0c5a36f9a018
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840118"
---
# <a name="irql_connection_function-rule-ndis"></a>Irql\_连接\_函数规则（ndis）


**Irql\_连接\_函数**规则指定必须在正确的 Irql 级别调用协议驱动程序的 NDIS 连接函数。

此规则验证以下 NDIS 函数：

**NdisCoAssignInstanceNam**
**NdisCoCreateVc**
**NdisCoDeleteVc**
**NdisCoGetTapiCallId**
**NdisCoOidRequest**
**NdisCoOidRequestComplete**
**NdisCoSendNetBufferLists**

|              |      |
|--------------|------|
| 驱动程序型号 | 以此 |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Irql_Connection_Function</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisCoAssignInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename)
[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)
[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)
[**NdisCoGetTapiCallId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscogettapicallid)
[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)
[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)
[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)








