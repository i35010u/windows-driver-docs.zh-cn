---
title: Irql\_网络缓冲区\_函数规则 (ndis)
description: Irql\_网络缓冲区\_函数规则指定 NET\_缓冲区相关函数的调用必须在正确的 IRQL 级别。
ms.assetid: e3b43ba1-3b58-4bc8-9d90-7be31c9e0a09
ms.date: 05/21/2018
keywords:
- Irql_NetBuffer_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_NetBuffer_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97bdde0cf34405cac21736725d3355d24e896a9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523003"
---
# <a name="irqlnetbufferfunction-rule-ndis"></a>Irql\_网络缓冲区\_函数规则 (ndis)


Irql\_网络缓冲区\_函数规则指定 NET\_缓冲区相关函数的调用必须在正确的 IRQL 级别。

此规则验证以下 NDIS 函数：

**NdisAdvanceNetBufferDataStart**
**disAdvanceNetBufferListDataStart**
**NdisAllocateCloneNetBufferList** 
 **NdisAllocateFragmentNetBufferList**
**NdisAllocateMdl**
**NdisAllocateNetBuffer** 
 **NdisAllocateNetBufferAndNetBufferList**
**NdisAllocateNetBufferList**
**NdisAllocateNetBufferListContext** 
**NdisAllocateNetBufferListPool**
**NdisAllocateNetBufferMdlAndData**
**NdisAllocateNetBufferPool**
 **NdisAllocateReassembledNetBufferList**
**NdisCopyFromNetBufferToNetBuffer** 
 **NdisCopyReceiveNetBufferListInfo**
**NdisCopySendNetBufferListInfo**
**NdisFreeCloneNetBufferList** 
**NdisFreeFragmentNetBufferList**
**NdisFreeMdl**
**NdisFreeNetBuffer** 
**NdisFreeNetBufferList**
**NdisFreeNetBufferListContext**
**NdisFreeNetBufferListPool**
 **NdisFreeNetBufferPool**
**NdisFreeReassembledNetBufferList** 
 **NdisGetDataBuffer**
**NdisGetMdlPhysicalArraySize**
**NdisGetPoolFromNetBuffer** 
 **NdisGetPoolFromNetBufferList**
**NdisQueryMdl**
**NdisQueryMdlOffset**
 **NdisQueryNetBufferPhysicalCount**
**NdisRetreatNetBufferDataStart** 
 **NdisRetreatNetBufferListDataStart**

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_NetBuffer_Function</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisAdvanceNetBufferDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff560703)
[**NdisAdvanceNetBufferListDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff560704)
[**NdisAllocateCloneNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560705)
[**NdisAllocateFragmentNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560707)
[**NdisAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff561605)
[**NdisAllocateNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561607)
[**NdisAllocateNetBufferAndNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561608)
[**NdisAllocateNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561609)
[**NdisAllocateNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff561610)
[**NdisAllocateNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)
[**NdisAllocateNetBufferMdlAndData**](https://msdn.microsoft.com/library/windows/hardware/ff561612)
[**NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561613)
[**NdisAllocateReassembledNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561614)
[**NdisCopyFromNetBufferToNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561718)
[**NdisCopyReceiveNetBufferListInfo**](https://msdn.microsoft.com/library/windows/hardware/ff561722)
[**NdisCopySendNetBufferListInfo**](https://msdn.microsoft.com/library/windows/hardware/ff561724)
[**NdisFreeCloneNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561841)
[**NdisFreeFragmentNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561847)
[**NdisFreeMdl**](https://msdn.microsoft.com/library/windows/hardware/ff562575)
[**NdisFreeNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562582)
[**NdisFreeNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562583)
[**NdisFreeNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff562587)
[**NdisFreeNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff562590)
[**NdisFreeNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff562592)
[**NdisFreeReassembledNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562594)
[**NdisGetDataBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562631)
[**NdisGetMdlPhysicalArraySize**](https://msdn.microsoft.com/library/windows/hardware/ff562639)
[**NdisGetPoolFromNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562657)
[**NdisGetPoolFromNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562659)
[**NdisQueryMdl**](https://msdn.microsoft.com/library/windows/hardware/ff563757)
[**NdisQueryMdlOffset**](https://msdn.microsoft.com/library/windows/hardware/ff563761)
[**NdisQueryNetBufferPhysicalCount**](https://msdn.microsoft.com/library/windows/hardware/ff563766)
[**NdisRetreatNetBufferDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564527)
[**NdisRetreatNetBufferListDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564529)








