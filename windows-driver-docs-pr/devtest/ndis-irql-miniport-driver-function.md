---
title: Irql\_微型端口\_驱动程序\_函数规则（ndis）
description: "\"Irql\\_微型端口\\_驱动程序\\_函数规则\" 指定必须在正确的 IRQL 级别调用微型端口驱动程序的 NDIS 函数。"
ms.assetid: b82627db-63bd-413f-9d7f-dbb611cf2c50
ms.date: 05/21/2018
keywords:
- Irql_Miniport_Driver_Function 规则（ndis）
topic_type:
- apiref
api_name:
- Irql_Miniport_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 87aba64cef8cd8fed8e0cb11c59ff1373d032838
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839388"
---
# <a name="irql_miniport_driver_function-rule-ndis"></a>Irql\_微型端口\_驱动程序\_函数规则（ndis）


"Irql\_微型端口\_驱动程序\_函数规则" 指定必须在正确的 IRQL 级别调用微型端口驱动程序的 NDIS 函数。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Irql_Miniport_Driver_Function</strong>规则。</p>
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

[**NdisMCreateLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcreatelog)
[**NdisMDeregisterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterdmachannel)
[**NdisMDeregisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterioportrange)
[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)
[**NdisMFlushLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismflushlog)
[**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)
[**NdisMFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)
[**NdisMGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdeviceproperty)
[**NdisMGetDmaAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdmaalignment)
[**NdisMMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismmapiospace)
[**NdisMPauseComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismpausecomplete)
[**NdisMQueryAdapterInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryadapterinstancename)
[**NdisMReadDmaCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreaddmacounter)
[**NdisMRegisterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterdmachannel)
[**NdisMRegisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterioportrange)
[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)
[**NdisMRemoveMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismremoveminiport)
[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)
[**NdisMRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismrestartcomplete)
[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)
[**NdisMSetupDmaTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetupdmatransfer)
[**NdisMSleep**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsleep)
[**NdisMUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismunmapiospace)
[**NdisMWriteLogData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismwritelogdata)








