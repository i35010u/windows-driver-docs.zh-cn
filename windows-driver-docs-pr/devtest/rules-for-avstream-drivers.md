---
title: 有关 AVStream 驱动程序的规则
description: 有关 AVStream 微型端口驱动程序的 DDI 符合性规则验证内核流式处理驱动程序 (ks.sys) 和其微型端口驱动程序之间的 DDI 接口协议。
ms.assetid: 0A104ADF-8607-4708-A0E3-1697F55B0CF5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0b2fd294c050f07af713a665f83125a51add4261
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526272"
---
# <a name="rules-for-avstream-drivers"></a>有关 AVStream 驱动程序的规则


有关 AVStream 微型端口驱动程序的 DDI 符合性规则验证内核流式处理驱动程序 (ks.sys) 和其微型端口驱动程序之间的 DDI 接口协议。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ks-kscallbackreturn.md" data-raw-source="[&lt;strong&gt;KsCallbackReturn&lt;/strong&gt;](ks-kscallbackreturn.md)"><strong>KsCallbackReturn</strong></a></p></td>
<td align="left"><p>KsCallbackReturn 规则指定一个内核流式处理 (KS) 微型端口驱动程序回调函数返回仅允许的状态值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"><strong>KsDeviceMutex</strong></a></p></td>
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"> <strong>KsDeviceMutex</strong> </a>规则指定流式处理微型端口驱动程序的内核使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff560911" data-raw-source="[&lt;strong&gt;KsAcquireDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560911)"> <strong>KsAcquireDevice</strong> </a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff566783" data-raw-source="[&lt;strong&gt;KsReleaseDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566783)"><strong>KsReleaseDevice</strong> </a>正确的顺序。 也就是说，每次调用<strong>KsAcquireDevice</strong>必须具有相应地调用<strong>KsReleaseDevice</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksfiltermutex.md" data-raw-source="[&lt;strong&gt;KsFilterMutex&lt;/strong&gt;](ks-ksfiltermutex.md)"><strong>KsFilterMutex</strong></a></p></td>
<td align="left"><p>KsFilterMutex 规则指定 KS 微型端口驱动程序获取并释放该筛选器互斥体以正确的顺序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlddis.md" data-raw-source="[&lt;strong&gt;KsIrqlDDIs&lt;/strong&gt;](ks-ksirqlddis.md)"><strong>KsIrqlDDIs</strong></a></p></td>
<td align="left"><p>KsIrqlDDIs 规则指定，内核流式处理 (KS) 微型端口驱动程序调用 KS DDIs 在正确的 IRQL 级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksirqldevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlDeviceCallbacks&lt;/strong&gt;](ks-ksirqldevicecallbacks.md)"><strong>KsIrqlDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlDeviceCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 KS 设备回调函数具有相同的 IRQL 时调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlFilterCallbacks&lt;/strong&gt;](ks-ksirqlfiltercallbacks.md)"><strong>KsIrqlFilterCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlFilterCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 KS 筛选器回调函数具有相同的 IRQL 时调用回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ksmarkpendingirp.md" data-raw-source="[&lt;strong&gt;KsMarkPendingIrp&lt;/strong&gt;](ksmarkpendingirp.md)"><strong>KsMarkPendingIrp</strong></a></p></td>
<td align="left"><p>KsMarkPendingIrp 规则指定内核流 (KS) 微型端口驱动程序过程应将作为挂起的 Irp 标记时从以下的回调函数返回 STATUS_PENDING 使用：</p>
<ul>
<li>AVStrMiniFilterClose</li>
<li>AVStrMiniPinClose</li>
<li>AVStrMiniPinCreate</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlpincallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlPinCallbacks&lt;/strong&gt;](ks-ksirqlpincallbacks.md)"><strong>KsIrqlPinCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlPinCallbacks 规则指定内核流 (KS) 微型端口驱动程序返回从它必须在调用同一 IRQL KS Pin 回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsProcessingMutex&lt;/strong&gt;](ks-ksprocessingmutex.md)"><strong>KsProcessingMutex</strong></a></p></td>
<td align="left"><p>KsProcessingMutex 规则指定 KS 微型端口驱动程序使用正确的顺序处理互斥体：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerclone.md" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](ks-ksstreampointerclone.md)"><strong>KsStreamPointerClone</strong></a></p></td>
<td align="left"><p>KsStreamPointerClone 规则指定内核流 (KS) 微型端口驱动程序正确使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567129" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567129)"> <strong>KsStreamPointerClone</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff567130" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567130)"> <strong>KsStreamPointerDelete</strong></a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksstreampointerlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](ks-ksstreampointerlock.md)"><strong>KsStreamPointerLock</strong></a></p></td>
<td align="left"><p>KsStreamPointerLock 规则指定一个内核流式处理 (KS) 微型端口驱动程序使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567134" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567134)"> <strong>KsStreamPointerLock</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff567137" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567137)"> <strong>KsStreamPointerUnlock</strong></a>正确的顺序的函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerunlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](ks-ksstreampointerunlock.md)"><strong>KsStreamPointerUnlock</strong></a></p></td>
<td align="left"><p>KsStreamPointerUnlock 规则指定一个内核流式处理 (KS) 微型端口驱动程序解锁所有流指针之前的驱动程序已卸载 （或停用设备）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimeddevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedDeviceCallbacks&lt;/strong&gt;](ks-kstimeddevicecallbacks.md)"><strong>KsTimedDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedDeviceCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 500 毫秒内的某个设备回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedFilterCallbacks&lt;/strong&gt;](ks-kstimedfiltercallbacks.md)"><strong>KsTimedFilterCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedFilterCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 500 毫秒内的某个筛选器回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedpincallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedPinCallbacks&lt;/strong&gt;](ks-kstimedpincallbacks.md)"><strong>KsTimedPinCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedPinCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 500 毫秒内的某个 pin 回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedpinsetdevicestate.md" data-raw-source="[&lt;strong&gt;KsTimedPinSetDeviceState&lt;/strong&gt;](ks-kstimedpinsetdevicestate.md)"><strong>KsTimedPinSetDeviceState</strong></a></p></td>
<td align="left"><p>KsTimedPinSetDeviceState 规则指定 AVStream (KS) 微型端口驱动程序，可使用 AVStream 微型驱动程序的状态转换&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff556359" data-raw-source="[&lt;em&gt;AVStrMiniPinSetDeviceState&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556359)"> <em>AVStrMiniPinSetDeviceState</em> </a>例程中所需的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsTimedProcessingMutex&lt;/strong&gt;](ks-kstimedprocessingmutex.md)"><strong>KsTimedProcessingMutex</strong></a></p></td>
<td align="left"><p>KsTimedProcessingMutex 规则指定 KS 微型端口驱动程序不应阻止处理 mutex 超过 100 毫秒。</p></td>
</tr>
</tbody>
</table>

 

 

 





