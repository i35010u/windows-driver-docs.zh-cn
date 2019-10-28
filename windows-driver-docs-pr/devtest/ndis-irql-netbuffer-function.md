---
title: Irql\_NetBuffer\_函数规则（ndis）
description: Irql\_NetBuffer\_函数规则指定必须在正确的 IRQL 级别调用 NET\_与缓冲区相关的函数。
ms.assetid: e3b43ba1-3b58-4bc8-9d90-7be31c9e0a09
ms.date: 05/21/2018
keywords:
- Irql_NetBuffer_Function 规则（ndis）
topic_type:
- apiref
api_name:
- Irql_NetBuffer_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53bb96318d64e6b58767eadf93299938b68ff839
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839385"
---
# <a name="irql_netbuffer_function-rule-ndis"></a>Irql\_NetBuffer\_函数规则（ndis）


Irql\_NetBuffer\_函数规则指定必须在正确的 IRQL 级别调用 NET\_与缓冲区相关的函数。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Irql_NetBuffer_Function</strong>规则。</p>
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

[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart)
[**NdisAdvanceNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferlistdatastart)
[**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateclonenetbufferlist)
[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)
[**NdisAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatemdl)
[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)
[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)
[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)
[**NdisAllocateNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistcontext)
[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)
[**NdisAllocateNetBufferMdlAndData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffermdlanddata)
[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool)
[**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)
[**NdisCopyFromNetBufferToNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscopyfromnetbuffertonetbuffer)
[**NdisCopyReceiveNetBufferListInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscopyreceivenetbufferlistinfo)
[**NdisCopySendNetBufferListInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscopysendnetbufferlistinfo)
[**NdisFreeCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeclonenetbufferlist)
[**NdisFreeFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreefragmentnetbufferlist)
[**NdisFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreemdl)
[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)
[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)
[**NdisFreeNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistcontext)
[**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool)
[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool)
[**NdisFreeReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreereassemblednetbufferlist)
[**NdisGetDataBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetdatabuffer)
[**NdisGetMdlPhysicalArraySize**](https://docs.microsoft.com/windows-hardware/drivers/network/ndisgetmdlphysicalarraysize)
[**NdisGetPoolFromNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetpoolfromnetbuffer)
[**NdisGetPoolFromNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetpoolfromnetbufferlist)
[**NdisQueryMdl**](https://docs.microsoft.com/windows-hardware/drivers/network/ndisquerymdl)
[**NdisQueryMdlOffset**](https://docs.microsoft.com/windows-hardware/drivers/network/ndisquerymdloffset)
[**NdisQueryNetBufferPhysicalCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerynetbufferphysicalcount)
[**NdisRetreatNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart)
[**NdisRetreatNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferlistdatastart)








