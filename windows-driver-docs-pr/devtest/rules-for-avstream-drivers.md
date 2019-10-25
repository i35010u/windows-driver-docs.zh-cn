---
title: AVStream 驱动程序的规则
description: AVStream 微型端口驱动程序的 DDI 符合性规则验证内核流式处理驱动程序（ks）与其微型端口驱动程序之间的 DDI 接口协议。
ms.assetid: 0A104ADF-8607-4708-A0E3-1697F55B0CF5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc5aceb51bb87258551155096a69bb6702ad5187
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840047"
---
# <a name="rules-for-avstream-drivers"></a>AVStream 驱动程序的规则


AVStream 微型端口驱动程序的 DDI 符合性规则验证内核流式处理驱动程序（ks）与其微型端口驱动程序之间的 DDI 接口协议。

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
<td align="left"><p>KsCallbackReturn 规则指定内核流式处理（KS）微型端口驱动程序回调函数只返回允许的状态值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"><strong>KsDeviceMutex</strong></a></p></td>
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"><strong>KsDeviceMutex</strong></a>规则指定内核流式处理端口驱动程序在正确的序列中使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice" data-raw-source="[&lt;strong&gt;KsAcquireDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice)"><strong>KsAcquireDevice</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice" data-raw-source="[&lt;strong&gt;KsReleaseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice)"><strong>KsReleaseDevice</strong></a> 。 也就是说，每次调用<strong>KsAcquireDevice</strong>时，都必须具有对<strong>KsReleaseDevice</strong>的相应调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksfiltermutex.md" data-raw-source="[&lt;strong&gt;KsFilterMutex&lt;/strong&gt;](ks-ksfiltermutex.md)"><strong>KsFilterMutex</strong></a></p></td>
<td align="left"><p>KsFilterMutex 规则指定一个 KS 微型端口驱动程序获取并按正确的顺序释放筛选器互斥体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlddis.md" data-raw-source="[&lt;strong&gt;KsIrqlDDIs&lt;/strong&gt;](ks-ksirqlddis.md)"><strong>KsIrqlDDIs</strong></a></p></td>
<td align="left"><p>KsIrqlDDIs 规则指定内核流式处理（KS）微型端口驱动程序在正确的 IRQL 级别调用 KS DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksirqldevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlDeviceCallbacks&lt;/strong&gt;](ks-ksirqldevicecallbacks.md)"><strong>KsIrqlDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlDeviceCallbacks 规则指定内核流式处理（KS）微型端口驱动程序从具有调用时所具有的相同 IRQL 的 KS 设备回调函数返回。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlFilterCallbacks&lt;/strong&gt;](ks-ksirqlfiltercallbacks.md)"><strong>KsIrqlFilterCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlFilterCallbacks 规则指定内核流式处理（KS）微型端口驱动程序将从 KS 筛选器回调函数返回，该函数与调用回调函数时使用的 IRQL 相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ksmarkpendingirp.md" data-raw-source="[&lt;strong&gt;KsMarkPendingIrp&lt;/strong&gt;](ksmarkpendingirp.md)"><strong>KsMarkPendingIrp</strong></a></p></td>
<td align="left"><p>KsMarkPendingIrp 规则指定在通过以下回调函数返回 STATUS_PENDING 时，内核流（KS）微型端口驱动程序应将 Irp 标记为挂起：</p>
<ul>
<li>AVStrMiniFilterClose</li>
<li>AVStrMiniPinClose</li>
<li>AVStrMiniPinCreate</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlpincallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlPinCallbacks&lt;/strong&gt;](ks-ksirqlpincallbacks.md)"><strong>KsIrqlPinCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlPinCallbacks 规则指定内核流（KS）微型端口驱动程序从一个 KS Pin 回调函数返回，该函数与调用该函数时使用的 IRQL 相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsProcessingMutex&lt;/strong&gt;](ks-ksprocessingmutex.md)"><strong>KsProcessingMutex</strong></a></p></td>
<td align="left"><p>KsProcessingMutex 规则指定一个 KS 微型端口驱动程序按正确的顺序使用处理互斥体：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerclone.md" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](ks-ksstreampointerclone.md)"><strong>KsStreamPointerClone</strong></a></p></td>
<td align="left"><p>KsStreamPointerClone 规则指定内核流（KS）微型端口驱动程序正确使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)"><strong>KsStreamPointerClone</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)"><strong>KsStreamPointerDelete</strong></a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksstreampointerlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](ks-ksstreampointerlock.md)"><strong>KsStreamPointerLock</strong></a></p></td>
<td align="left"><p>KsStreamPointerLock 规则指定内核流式处理（KS）微型端口驱动程序按正确的顺序使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)"><strong>KsStreamPointerLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)"><strong>KsStreamPointerUnlock</strong></a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerunlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](ks-ksstreampointerunlock.md)"><strong>KsStreamPointerUnlock</strong></a></p></td>
<td align="left"><p>KsStreamPointerUnlock 规则指定内核流式处理（KS）微型端口驱动程序在卸载驱动程序之前解锁所有流指针（或设备停止）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimeddevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedDeviceCallbacks&lt;/strong&gt;](ks-kstimeddevicecallbacks.md)"><strong>KsTimedDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedDeviceCallbacks 规则指定内核流式处理（KS）微型端口驱动程序在500毫秒内从设备回调函数返回。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedFilterCallbacks&lt;/strong&gt;](ks-kstimedfiltercallbacks.md)"><strong>KsTimedFilterCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedFilterCallbacks 规则指定内核流式处理（KS）微型端口驱动程序在500毫秒内从筛选器回调函数返回。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedpincallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedPinCallbacks&lt;/strong&gt;](ks-kstimedpincallbacks.md)"><strong>KsTimedPinCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedPinCallbacks 规则指定内核流式处理（KS）微型端口驱动程序在500毫秒内从 pin 回调函数返回。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedpinsetdevicestate.md" data-raw-source="[&lt;strong&gt;KsTimedPinSetDeviceState&lt;/strong&gt;](ks-kstimedpinsetdevicestate.md)"><strong>KsTimedPinSetDeviceState</strong></a></p></td>
<td align="left"><p>KsTimedPinSetDeviceState 规则指定 AVStream （KS）微型端口驱动程序在所需时间内使用 AVStream 微型驱动程序的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate" data-raw-source="[&lt;em&gt;AVStrMiniPinSetDeviceState&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)"><em>AVStrMiniPinSetDeviceState</em></a>例程进行状态转换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsTimedProcessingMutex&lt;/strong&gt;](ks-kstimedprocessingmutex.md)"><strong>KsTimedProcessingMutex</strong></a></p></td>
<td align="left"><p>KsTimedProcessingMutex 规则指定一个 KS 微型端口驱动程序不应将处理互斥体保留超过100毫秒。</p></td>
</tr>
</tbody>
</table>

 

 

 





