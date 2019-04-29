---
title: IrqlDispatch 规则 (wdm)
description: IrqlDispatch 规则指定驱动程序调用以下 DDIs，仅当执行在 IRQL DISPATCH_LEVEL 时。
ms.assetid: f72d4f27-b488-4d0a-97b7-9cb40f00e346
ms.date: 05/21/2018
keywords:
- IrqlDispatch 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a6105b18917e1077944e6d1249ca52a9f8ec2e38
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359445"
---
# <a name="irqldispatch-rule-wdm"></a>IrqlDispatch 规则 (wdm)


**IrqlDispatch**规则指定驱动程序调用以下 DDIs，仅当执行在 IRQL = 调度\_级别。

-   [**FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)

-   [**FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513)

-   [**GetScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff546531)

-   [**IoAllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff548216)

-   [**IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)

-   [**IoFreeController**](https://msdn.microsoft.com/library/windows/hardware/ff549104)

-   [**IoStartNextPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550358)

-   [**KeAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551921)

-   [**KeInsertByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552178)

-   [**KeInsertDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552180)

-   [**KeReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553150)

-   [**KeRemoveByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553152)

-   [**KeRemoveDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553156)

-   [**PutScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff559967)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xA:IRQL\_不\_较少\_或者\_相等**](https://msdn.microsoft.com/library/windows/hardware/ff560129) ， [ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020003) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlDispatch</strong>规则。</p>
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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用对象
----------

[**AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573)
[**AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575) 
 [ **BuildMdlFromScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff540686)
[**BuildScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff540689) 
 [ **FlushAdapterBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff545917)
[**FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)
[**FreeCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff546511) 
 [ **FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513)
[**GetDmaAlignment** ](https://msdn.microsoft.com/library/windows/hardware/ff546530)
 [ **GetScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff546531)
[**IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224) 
[ **IoFreeController**](https://msdn.microsoft.com/library/windows/hardware/ff549104)
[**IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358) 
[ **IoWriteErrorLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff550527)
[**KeInsertByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552178)
 [ **KeInsertDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552180)
[**KeRemoveByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553152) 
 [ **KeRemoveDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553156)
[**MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402) 
 [ **PutDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff559965)
[**PutScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff559967) 
 [ **ReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff560782)另请参阅
--------

[**管理硬件优先级**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**使用自旋锁的同时防止错误和死锁**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





