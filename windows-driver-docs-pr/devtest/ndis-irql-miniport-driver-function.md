---
title: Irql\_微型端口\_驱动程序\_函数规则 (ndis)
description: Irql\_微型端口\_驱动程序\_函数规则指定必须在正确的 IRQL 级别调用微型端口驱动程序的 NDIS 函数。
ms.assetid: b82627db-63bd-413f-9d7f-dbb611cf2c50
ms.date: 05/21/2018
keywords:
- Irql_Miniport_Driver_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_Miniport_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 091104219c644dbef52faf10b9aaebe29f4bb9e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565713"
---
# <a name="irqlminiportdriverfunction-rule-ndis"></a>Irql\_微型端口\_驱动程序\_函数规则 (ndis)


Irql\_微型端口\_驱动程序\_函数规则指定必须在正确的 IRQL 级别调用微型端口驱动程序的 NDIS 函数。

此规则验证 NDIS 微型端口驱动程序日志记录、 NDIS 端口和 NDIS DMA 接口的函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_Miniport_Driver_Function</strong>规则。</p>
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

<a name="applies-to"></a>适用对象
----------

[**NdisMCreateLog**](https://msdn.microsoft.com/library/windows/hardware/ff563572)
[**NdisMDeregisterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff563574)
[**NdisMDeregisterIoPortRange**](https://msdn.microsoft.com/library/windows/hardware/ff563577) 
 [ **NdisMDeregisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563578)
[**NdisMFlushLog** ](https://msdn.microsoft.com/library/windows/hardware/ff563584) 
 [ **NdisMFreePort**](https://msdn.microsoft.com/library/windows/hardware/ff563588)
[**NdisMFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563589) 
 [ **NdisMGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff563592)
[**NdisMGetDmaAlignment** ](https://msdn.microsoft.com/library/windows/hardware/ff563593) 
 [**NdisMMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff563613)
[**NdisMPauseComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563628) 
 [ **NdisMQueryAdapterInstanceName**](https://msdn.microsoft.com/library/windows/hardware/ff563630)
[**NdisMReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff563641) 
 [ **NdisMRegisterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff563646)
[**NdisMRegisterIoPortRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563651) 
[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)
[**NdisMRemoveMiniport** ](https://msdn.microsoft.com/library/windows/hardware/ff563661) 
 [ **NdisMResetComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563663)
[**NdisMRestartComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563665) 
 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672) 
 [ **NdisMSetupDmaTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff563675)
[**NdisMSleep** ](https://msdn.microsoft.com/library/windows/hardware/ff563677) 
 [ **NdisMUnmapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff563691)
[**NdisMWriteLogData**](https://msdn.microsoft.com/library/windows/hardware/ff563695)








