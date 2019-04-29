---
title: 驱动程序对硬件的访问
description: 驱动程序对硬件的访问
ms.assetid: 66743284-6cdd-467e-b3b4-3d588cd296a5
keywords:
- 即插即用 WDK KMDF，硬件访问
- 插 WDK KMDF，硬件访问
- 电源管理 WDK KMDF，硬件访问
- 访问硬件 WDK KMDF
- framework 对象 WDK KMDF，设备对象
- framework 对象 WDK KMDF，硬件访问
- 设备对象 WDK KMDF
- 事件回调函数 WDK KMDF
- 回调函数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcef70cb291c05c242dda3bc4721dc558047b931
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391356"
---
# <a name="driver-access-to-hardware"></a>驱动程序对硬件的访问


下表列出了所有 framework 设备对象定义，按字母顺序的事件回调函数。 下表显示了您的驱动程序可以访问的硬件的回调函数的 WDFDEVICE 句柄表示的回调函数。 您可以访问硬件，因为设备处于其工作 (D0) 状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件回叫 functionsfor framework 设备对象</th>
<th align="left">是可访问的硬件？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540843" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540843)"><em>EvtDeviceArmWakeFromS0</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540844" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540844)"><em>EvtDeviceArmWakeFromSx</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540846" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSxWithReason&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540846)"><em>EvtDeviceArmWakeFromSxWithReason</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"><em>EvtDeviceD0Exit</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540858" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540858)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
<td align="left"><p>父总线可能是在 D0。 设备可能是在 D0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540860" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540860)"><em>EvtDeviceDisarmWakeFromS0</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540862" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540862)"><em>EvtDeviceDisarmWakeFromSx</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540863" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540863)"><em>EvtDeviceEject</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540866" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540866)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
<td align="left"><p>父总线位于 D0，但可能不到设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540868" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540868)"><em>EvtDeviceFileCreate</em></a></p></td>
<td align="left"><p>可能</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540870" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540870)"><em>EvtDeviceFilterAddResourceRequirements</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540872" data-raw-source="[&lt;em&gt;EvtDeviceFilterRemoveResourceRequirements&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540872)"><em>EvtDeviceFilterRemoveResourceRequirements</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"><em>EvtDevicePrepareHardware</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540886" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540886)"><em>EvtDeviceRelationsQuery</em></a></p></td>
<td align="left"><p>是的但该设备可能处于睡眠状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"><em>EvtDeviceReleaseHardware</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540892" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540892)"><em>EvtDeviceRemoveAddedResources</em></a></p></td>
<td align="left"><p>是的但尚未分配到设备的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540894" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540894)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540895" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540895)"><em>EvtDeviceResourcesQuery</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540898" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540898)"><em>EvtDeviceSelfManagedIoCleanup</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540901" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540901)"><em>EvtDeviceSelfManagedIoFlush</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540902" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540902)"><em>EvtDeviceSelfManagedIoInit</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540905" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540905)"><em>EvtDeviceSelfManagedIoRestart</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a></p></td>
<td align="left"><p>否，如果设备已被意外删除;否则为是。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540909" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540909)"><em>EvtDeviceSetLock</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540913" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540913)"><em>EvtDeviceSurpriseRemoval</em></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540915" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540915)"><em>EvtDeviceUsageNotification</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540919" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromS0Triggered&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540919)"><em>EvtDeviceWakeFromS0Triggered</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540923" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromSxTriggered&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540923)"><em>EvtDeviceWakeFromSxTriggered</em></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"><em>EvtDeviceWdmIrpPreprocess</em></a></p></td>
<td align="left"><p>取决于 IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540874" data-raw-source="[&lt;em&gt;EvtDevicePnpStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540874)"><em>EvtDevicePnpStateChange</em></a></p></td>
<td align="left"><p>取决于状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540876" data-raw-source="[&lt;em&gt;EvtDevicePowerPolicyStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540876)"><em>EvtDevicePowerPolicyStateChange</em></a></p></td>
<td align="left"><p>取决于状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540878" data-raw-source="[&lt;em&gt;EvtDevicePowerStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540878)"><em>EvtDevicePowerStateChange</em></a></p></td>
<td align="left"><p>取决于状态。</p></td>
</tr>
</tbody>
</table>

 

 

 





