---
title: 从筛选器驱动程序调用 PoStartNextPowerIrp
description: 从筛选器驱动程序调用 PoStartNextPowerIrp
ms.assetid: 6005f107-8f90-4530-91c2-9f0947cacb0a
keywords:
- power Irp WDK 内核 PoStartNextPowerIrp
- PoStartNextPowerIrp
- 筛选器驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8064a7a16578e324fda85081118b642bc6a0d5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385264"
---
# <a name="calling-postartnextpowerirp-from-a-filter-driver"></a>从筛选器驱动程序调用 PoStartNextPowerIrp


使用 Windows Vista 开始，调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)不是必需的和此例程的调用会执行任何电源管理操作。 但是，在 Windows Server 2003、 Windows XP 和 Windows 2000 中，筛选器驱动程序必须调用**PoStartNextPowerIrp**一次为每个[ **IRP\_MN\_查询\_电源** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)或[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)驱动程序收到的请求。 在调用发生时取决于请求和驱动程序是否会失败或成功请求，如下表所示的类型。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>请求的类型</th>
<th>如果驱动程序成功请求，会发生在调用：</th>
<th>如果驱动程序使请求失败，会发生在调用：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IRP_MN_QUERY_POWER</strong> （设备电源状态）</p></td>
<td><p>在中<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <em>IoCompletion</em> </a>例程，立即在返回之前。</p></td>
<td><p>在中<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <em>DispatchPower</em> </a>例程，然后才能调用<strong>IoCompleteRequest</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_QUERY_POWER</strong> （系统电源状态）</p></td>
<td><p>在中<em>DispatchPower</em>例程之后获取删除锁, 和之前设置 IRP 堆栈位置。</p></td>
<td><p>在中<em>DispatchPower</em>例程，然后再调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP_MN_SET_POWER</strong> （设备电源状态）</p></td>
<td><p>在中<em>IoCompletion</em>例程，立即在返回之前。</p></td>
<td><p>不允许。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_SET_POWER</strong> （系统电源状态）</p></td>
<td><p>在中<em>DispatchPower</em>例程之后获取删除锁, 和之前设置 IRP 堆栈位置。</p></td>
<td><p>不允许。</p></td>
</tr>
</tbody>
</table>

 

 

 




