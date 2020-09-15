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
ms.openlocfilehash: dc9c041e7d9fc1caa3f7445bc25831198d375a45
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107542"
---
# <a name="calling-postartnextpowerirp-from-a-filter-driver"></a>从筛选器驱动程序调用 PoStartNextPowerIrp


从 Windows Vista 开始，调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，筛选器驱动程序必须针对每个[**IRP \_ MN \_ 查询 \_ 能力**](./irp-mn-query-power.md)或[**irp \_ MN \_ 设置 \_ **](./irp-mn-set-power.md)驱动程序收到的 power request 调用**PoStartNextPowerIrp**一次。 调用发生时，将取决于请求的类型以及该驱动程序是失败还是成功请求，如下表所示。

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
<td><p> (设备电源状态<strong>IRP_MN_QUERY_POWER</strong>) </p></td>
<td><p>在 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a> 例程中，在返回之前立即发生。</p></td>
<td><p>在 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a> 例程中，在调用 <strong>IoCompleteRequest</strong>之前。</p></td>
</tr>
<tr class="even">
<td><p> (系统电源状态<strong>IRP_MN_QUERY_POWER</strong>) </p></td>
<td><p>在 <em>DispatchPower</em> 例程中，在获取删除锁后，在设置 IRP 堆栈位置之前。</p></td>
<td><p>在 <em>DispatchPower</em> 例程中，在调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>之前。</p></td>
</tr>
<tr class="odd">
<td><p> (设备电源状态<strong>IRP_MN_SET_POWER</strong>) </p></td>
<td><p>在 <em>IoCompletion</em> 例程中，在返回之前立即发生。</p></td>
<td><p>不允许。</p></td>
</tr>
<tr class="even">
<td><p> (系统电源状态<strong>IRP_MN_SET_POWER</strong>) </p></td>
<td><p>在 <em>DispatchPower</em> 例程中，在获取删除锁后，在设置 IRP 堆栈位置之前。</p></td>
<td><p>不允许。</p></td>
</tr>
</tbody>
</table>

 

