---
title: 'Irql \_ 筛选器 \_ 驱动程序 \_ 函数规则 (ndis) '
description: Irql \_ 筛选器 \_ 驱动程序 \_ 函数规则指定必须在正确的 Irql 级别调用筛选器驱动程序的 NDIS 函数。
ms.assetid: 1dd45962-151b-472c-88a6-6042ecb7491c
ms.date: 05/21/2018
keywords:
- 'Irql_Filter_Driver_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_Filter_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7d2f175b64fc25ebcc8d12f9f5e43779a8f25838
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383779"
---
# <a name="irql_filter_driver_function-rule-ndis"></a>Irql \_ 筛选器 \_ 驱动程序 \_ 函数规则 (ndis) 


Irql \_ 筛选器 \_ 驱动程序 \_ 函数规则指定必须在正确的 Irql 级别调用筛选器驱动程序的 NDIS 函数。

用于筛选器驱动程序的 NDIS 函数包括：

**NdisFRegisterFilterDriver** 
**NdisFDeregisterFilterDriver** 
**NdisFSetAttributes** 
**NdisFRestartFilter** 
**NdisFRestartComplete** 
**NdisFPauseComplete** 
**NdisFSendNetBufferLists** 
**NdisFReturnNetBufferLists** 
**NdisFSendNetBufferListsComplete** 
**NdisFCancelSendNetBufferLists** 
**NdisFIndicateReceiveNetBufferLists** 
**NdisFNetPnPEvent** 
**NdisFDevicePnPEventNotify** 
**NdisEnumerateFilterModules**

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_Filter_Driver_Function</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisEnumerateFilterModules**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisenumeratefiltermodules) 
[**NdisFCancelSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists) 
[**NdisFDeregisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver) 
[**NdisFDevicePnPEventNotify**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdevicepnpeventnotify) 
[**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists) 
[**NdisFNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) 
[**NdisFPauseComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfpausecomplete) 
[**NdisFRegisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver) 
[**NdisFRestartComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartcomplete) 
[**NdisFRestartFilter**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter) 
[**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists) 
[**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) 
[**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete) 
[**NdisFSetAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsetattributes)