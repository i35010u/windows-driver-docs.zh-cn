---
title: 从设备电源策略所有者调用 PoStartNextPowerIrp
description: 从设备电源策略所有者调用 PoStartNextPowerIrp
ms.assetid: 58576ff8-638e-4928-9a2d-337ac3f4d2d8
keywords:
- power Irp WDK 内核，PoStartNextPowerIrp
- PoStartNextPowerIrp
- 设备电源策略 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1f3e23a6a934ece6e2af0967a65f97400a3a709
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188643"
---
# <a name="calling-postartnextpowerirp-from-a-device-power-policy-owner"></a>从设备电源策略所有者调用 PoStartNextPowerIrp





从 Windows Vista 开始，调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，拥有设备电源策略的函数驱动程序必须针对每个[**IRP \_ MN \_ 查询 \_ 能力**](./irp-mn-query-power.md)或[**irp \_ MN \_ 设置 \_ **](./irp-mn-set-power.md)驱动程序收到的 power request 调用**PoStartNextPowerIrp**一次。 调用发生时，将取决于请求的类型以及该驱动程序是失败还是成功请求，如下表所示。

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
<td><p>在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a> 例程中，在返回之前立即发生。</p></td>
<td><p>在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a> 例程中，在调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>之前。</p></td>
</tr>
<tr class="even">
<td><p> (系统电源状态<strong>IRP_MN_QUERY_POWER</strong>) </p></td>
<td><p>在完成系统 IRP 之前，在相关设备 IRP 的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)"><strong>PoRequestPowerIrp</strong></a> 回调例程中立即执行。</p></td>
<td><p>在 <em>DispatchPower</em> 例程中，在调用 <strong>IoCompleteRequest</strong>之前。</p></td>
</tr>
<tr class="odd">
<td><p> (设备电源状态<strong>IRP_MN_SET_POWER</strong>) </p></td>
<td><p>在 <em>IoCompletion</em> 例程中，在返回之前立即发生。</p></td>
<td><p>不允许。</p></td>
</tr>
<tr class="even">
<td><p> (系统电源状态<strong>IRP_MN_SET_POWER</strong>) </p></td>
<td><p>在完成系统 IRP 之前，在相关设备 IRP 的 <strong>PoRequestPowerIrp</strong> 回调例程中立即执行。</p></td>
<td><p>不允许。</p></td>
</tr>
</tbody>
</table>

 

 

