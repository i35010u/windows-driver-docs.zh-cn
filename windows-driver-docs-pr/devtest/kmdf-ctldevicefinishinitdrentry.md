---
title: 'CtlDeviceFinishInitDrEntry 规则 (kmdf) '
description: CtlDeviceFinishInitDrEntry 规则指定如果驱动程序在 DriverEntry 回调函数中创建控制设备对象，则该对象必须在创建设备后、从 EvtDriverDeviceAdd 回调函数退出之前调用 WdfControlFinishInitializing。 此规则不适用于非 PnP 驱动程序。
ms.date: 05/21/2018
keywords:
- 'CtlDeviceFinishInitDrEntry 规则 (kmdf) '
topic_type:
- apiref
api_name:
- CtlDeviceFinishInitDrEntry
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7de186a0703a4fdb278f88f8ef9e7cbb2cf1d0c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841323"
---
# <a name="ctldevicefinishinitdrentry-rule-kmdf"></a>CtlDeviceFinishInitDrEntry 规则 (kmdf) 


CtlDeviceFinishInitDrEntry 规则指定如果驱动程序在 [**DriverEntry**](../wdf/driverentry-for-kmdf-drivers.md)回调函数中创建控制设备对象，则该对象必须在创建设备后、从 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数退出之前调用 [**WdfControlFinishInitializing**](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing) 。 此规则不适用于非 PnP 驱动程序。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>CtlDeviceFinishInitDrEntry</strong> 规则。</p>
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

[**WdfControlDeviceInitAllocate**](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate) 
[**WdfControlFinishInitializing**](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing) 
[**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 
[**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)
