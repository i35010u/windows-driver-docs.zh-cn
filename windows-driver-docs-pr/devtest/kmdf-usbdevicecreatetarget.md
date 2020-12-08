---
title: 'UsbDeviceCreateTarget 规则 (kmdf) '
description: UsbDeviceCreateTarget 规则指定在设备上下文中当前存在的 WDFUSBDEVICE 对象)  (s 时，不会创建多个 WDFUSBDEVICE 对象。
ms.date: 05/21/2018
keywords:
- 'UsbDeviceCreateTarget 规则 (kmdf) '
topic_type:
- apiref
api_name:
- UsbDeviceCreateTarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1ef8cd6454b63d31dec9e19fe989970b7e9fb05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817447"
---
# <a name="usbdevicecreatetarget-rule-kmdf"></a>UsbDeviceCreateTarget 规则 (kmdf) 


**UsbDeviceCreateTarget** 规则指定在设备上下文中当前存在的 WDFUSBDEVICE 对象)  (s 时，不会创建多个 WDFUSBDEVICE 对象。

例如，当系统尝试管理资源并且需要为驱动程序分配不同的内存块时，可以多次调用 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 事件回调函数。 在这种情况下，在框架最初调用 *EvtDevicePrepareHardware* 后，将调用 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)事件回调函数以取消映射内存资源。 然后再次调用 *EvtDevicePrepareHardware* 来映射资源，以便驱动程序可以访问分配给设备的内存。 此规则检查驱动程序首先确认目标 WDFUSBDEVICE 为 **NULL** ，并且不只是创建新设备并替换上一个句柄。

**驱动程序模型： KMDF**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>UsbDeviceCreateTarget</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfUsbTargetDeviceCreate**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate) 
[ **WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)
