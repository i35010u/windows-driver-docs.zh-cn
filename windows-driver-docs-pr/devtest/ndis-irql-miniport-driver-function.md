---
title: 'Irql \_ 微型端口 \_ 驱动程序 \_ 函数规则 (ndis) '
description: Irql \_ 微型端口 \_ 驱动程序 \_ 函数规则指定必须在正确的 Irql 级别调用微型端口驱动程序的 NDIS 函数。
ms.assetid: b82627db-63bd-413f-9d7f-dbb611cf2c50
ms.date: 05/21/2018
keywords:
- 'Irql_Miniport_Driver_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_Miniport_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6175d9d8de48c8e4f774d77467f8c9f96609f2a9
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384917"
---
# <a name="irql_miniport_driver_function-rule-ndis"></a>Irql \_ 微型端口 \_ 驱动程序 \_ 函数规则 (ndis) 


Irql \_ 微型端口 \_ 驱动程序 \_ 函数规则指定必须在正确的 Irql 级别调用微型端口驱动程序的 NDIS 函数。

此规则验证 NDIS 微型端口驱动程序日志记录、NDIS 端口和 NDIS DMA 接口的功能。

**NdisMCreateLog** 
**NdisMDeregisterDmaChannel** 
**NdisMDeregisterIoPortRange** 
**NdisMDeregisterMiniportDriver** 
**NdisMFlushLog** 
**NdisMFreePort** 
**NdisMFreeSharedMemory** 
**NdisMGetDeviceProperty** 
**NdisMGetDmaAlignment** 
**NdisMMapIoSpace** 
**NdisMPauseComplete** 
**NdisMQueryAdapterInstanceName** 
**NdisMReadDmaCounter** 
**NdisMRegisterDmaChannel** 
**NdisMRegisterIoPortRange** 
**NdisMRegisterMiniportDriver** 
**NdisMRemoveMiniport** 
**NdisMResetComplete** 
**NdisMRestartComplete** 
**NdisMSetMiniportAttributes** 
**NdisMSetupDmaTransfer** 
**NdisMSleep** 
**NdisMUnmapIoSpace** 
**NdisMUpdateSharedMemory** 
**NdisMWriteLogData**

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_Miniport_Driver_Function</strong> 规则。</p>
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

[**NdisMCreateLog**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcreatelog) 
[**NdisMDeregisterDmaChannel**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterdmachannel) 
[**NdisMDeregisterIoPortRange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterioportrange) 
[**NdisMDeregisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) 
[**NdisMFlushLog**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismflushlog) 
[**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport) 
[**NdisMFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory) 
[**NdisMGetDeviceProperty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdeviceproperty) 
[**NdisMGetDmaAlignment**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdmaalignment) 
[**NdisMMapIoSpace**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismmapiospace) 
[**NdisMPauseComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismpausecomplete) 
[**NdisMQueryAdapterInstanceName**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryadapterinstancename) 
[**NdisMReadDmaCounter**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreaddmacounter) 
[**NdisMRegisterDmaChannel**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterdmachannel) 
[**NdisMRegisterIoPortRange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterioportrange) 
[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 
[**NdisMRemoveMiniport**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismremoveminiport) 
[**NdisMResetComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete) 
[**NdisMRestartComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismrestartcomplete) 
[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 
[**NdisMSetupDmaTransfer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetupdmatransfer) 
[**NdisMSleep**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsleep) 
[**NdisMUnmapIoSpace**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismunmapiospace) 
[**NdisMWriteLogData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismwritelogdata)