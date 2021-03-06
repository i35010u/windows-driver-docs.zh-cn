---
title: 'Irql \_ NetBuffer \_ 函数规则 (ndis) '
description: Irql \_ NetBuffer \_ 函数规则指定 \_ 必须在正确的 Irql 级别调用与网络缓冲区相关的函数。
ms.date: 05/21/2018
keywords:
- 'Irql_NetBuffer_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_NetBuffer_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1405d65d15a58d589939af5ceeb56aa17debc219
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248259"
---
# <a name="irql_netbuffer_function-rule-ndis"></a>Irql \_ NetBuffer \_ 函数规则 (ndis) 


Irql \_ NetBuffer \_ 函数规则指定 \_ 必须在正确的 Irql 级别调用与网络缓冲区相关的函数。

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

**驱动程序模型： NDIS**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_NetBuffer_Function</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisAdvanceNetBufferDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisadvancenetbufferdatastart) 
[**NdisAdvanceNetBufferListDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisadvancenetbufferlistdatastart) 
[**NdisAllocateCloneNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocateclonenetbufferlist) 
[**NdisAllocateFragmentNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatefragmentnetbufferlist) 
[**NdisAllocateMdl**](/windows-hardware/drivers/ddi/mdlapi/nf-mdlapi-ndisallocatemdl) 
[**NdisAllocateNetBuffer**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbuffer) 
[**NdisAllocateNetBufferAndNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferandnetbufferlist) 
[**NdisAllocateNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferlist) 
[**NdisAllocateNetBufferListContext**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferlistcontext) 
[**NdisAllocateNetBufferListPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferlistpool) 
[**NdisAllocateNetBufferMdlAndData**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbuffermdlanddata) 
[**NdisAllocateNetBufferPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferpool) 
[**NdisAllocateReassembledNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatereassemblednetbufferlist) 
[**NdisCopyFromNetBufferToNetBuffer**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndiscopyfromnetbuffertonetbuffer) 
[**NdisCopyReceiveNetBufferListInfo**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndiscopyreceivenetbufferlistinfo) 
[**NdisCopySendNetBufferListInfo**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndiscopysendnetbufferlistinfo) 
[**NdisFreeCloneNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreeclonenetbufferlist) 
[**NdisFreeFragmentNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreefragmentnetbufferlist) 
[**NdisFreeMdl**](/windows-hardware/drivers/ddi/mdlapi/nf-mdlapi-ndisfreemdl) 
[**NdisFreeNetBuffer**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbuffer) 
[**NdisFreeNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbufferlist) 
[**NdisFreeNetBufferListContext**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbufferlistcontext) 
[**NdisFreeNetBufferListPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbufferlistpool) 
[**NdisFreeNetBufferPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbufferpool) 
[**NdisFreeReassembledNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreereassemblednetbufferlist) 
[**NdisGetDataBuffer**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisgetdatabuffer) 
[**NdisGetMdlPhysicalArraySize**](../network/ndisgetmdlphysicalarraysize.md) 
[**NdisGetPoolFromNetBuffer**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisgetpoolfromnetbuffer) 
[**NdisGetPoolFromNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisgetpoolfromnetbufferlist) 
[**NdisQueryMdl**](../network/ndisquerymdl.md) 
[**NdisQueryMdlOffset**](../network/ndisquerymdloffset.md) 
[**NdisQueryNetBufferPhysicalCount**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisquerynetbufferphysicalcount) 
[**NdisRetreatNetBufferDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisretreatnetbufferdatastart) 
[**NdisRetreatNetBufferListDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisretreatnetbufferlistdatastart)
