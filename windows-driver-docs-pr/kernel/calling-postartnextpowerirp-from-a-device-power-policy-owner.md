---
title: 从设备电源策略所有者调用 PoStartNextPowerIrp
description: 从设备电源策略所有者调用 PoStartNextPowerIrp
ms.assetid: 58576ff8-638e-4928-9a2d-337ac3f4d2d8
keywords:
- power Irp WDK 内核 PoStartNextPowerIrp
- PoStartNextPowerIrp
- 设备电源策略 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c27cdaae466f11c9d220e412f7a327b923fa31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524291"
---
# <a name="calling-postartnextpowerirp-from-a-device-power-policy-owner"></a>从设备电源策略所有者调用 PoStartNextPowerIrp





使用 Windows Vista 开始，调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)不是必需的和此例程的调用会执行任何电源管理操作。 但是，在 Windows Server 2003、 Windows XP 和 Windows 2000 中，拥有设备的电源策略功能驱动程序必须调用**PoStartNextPowerIrp**一次为每个[ **IRP\_MN\_查询\_电源**](https://msdn.microsoft.com/library/windows/hardware/ff551699)或[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)驱动程序收到的请求。 在调用发生时取决于请求和驱动程序是否会失败或成功请求，如下表所示的类型。

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
<td><p>在中<a href="https://msdn.microsoft.com/library/windows/hardware/ff548354" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548354)"> <em>IoCompletion</em> </a>例程，立即在返回之前。</p></td>
<td><p>在中<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <em>DispatchPower</em> </a>例程，然后才能调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_QUERY_POWER</strong> （系统电源状态）</p></td>
<td><p>在中<a href="https://msdn.microsoft.com/library/windows/hardware/ff559734" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559734)"> <strong>PoRequestPowerIrp</strong> </a>相关设备 IRP 之前完成系统 IRP, 的回调例程。</p></td>
<td><p>在中<em>DispatchPower</em>例程，然后再调用<strong>IoCompleteRequest</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP_MN_SET_POWER</strong> （设备电源状态）</p></td>
<td><p>在中<em>IoCompletion</em>例程，立即在返回之前。</p></td>
<td><p>不允许。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_SET_POWER</strong> （系统电源状态）</p></td>
<td><p>在中<strong>PoRequestPowerIrp</strong>相关设备 IRP 之前完成系统 IRP, 的回调例程。</p></td>
<td><p>不允许。</p></td>
</tr>
</tbody>
</table>

 

 

 




