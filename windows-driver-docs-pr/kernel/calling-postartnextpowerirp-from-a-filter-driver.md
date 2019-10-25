---
title: 从筛选器驱动程序调用 PoStartNextPowerIrp
description: 从筛选器驱动程序调用 PoStartNextPowerIrp
ms.assetid: 6005f107-8f90-4530-91c2-9f0947cacb0a
keywords:
- power Irp WDK 内核，PoStartNextPowerIrp
- PoStartNextPowerIrp
- 筛选器驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e86feb41a2a1dc34ef9cfdcfb15772b41341cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837138"
---
# <a name="calling-postartnextpowerirp-from-a-filter-driver"></a>从筛选器驱动程序调用 PoStartNextPowerIrp


从 Windows Vista 开始，调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，筛选器驱动程序必须**对每**个[**IRP\_MN\_QUERY\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) or [**IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) request驱动程序接收的。 调用发生时，将取决于请求的类型以及该驱动程序是失败还是成功请求，如下表所示。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>请求类型</th>
<th>如果驱动程序成功执行请求，则调用发生：</th>
<th>如果驱动程序未通过该请求，则会发生调用：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IRP_MN_QUERY_POWER</strong> （设备电源状态）</p></td>
<td><p>在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a>例程中，在返回之前立即发生。</p></td>
<td><p>在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a>例程中，在调用<strong>IoCompleteRequest</strong>之前。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_QUERY_POWER</strong> （系统电源状态）</p></td>
<td><p>在<em>DispatchPower</em>例程中，在获取删除锁后，在设置 IRP 堆栈位置之前。</p></td>
<td><p>在<em>DispatchPower</em>例程中，在调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>之前。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP_MN_SET_POWER</strong> （设备电源状态）</p></td>
<td><p>在<em>IoCompletion</em>例程中，在返回之前立即发生。</p></td>
<td><p>不允许。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_SET_POWER</strong> （系统电源状态）</p></td>
<td><p>在<em>DispatchPower</em>例程中，在获取删除锁后，在设置 IRP 堆栈位置之前。</p></td>
<td><p>不允许。</p></td>
</tr>
</tbody>
</table>

 

 

 




