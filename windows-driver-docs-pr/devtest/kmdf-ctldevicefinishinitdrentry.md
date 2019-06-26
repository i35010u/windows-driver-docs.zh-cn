---
title: CtlDeviceFinishInitDrEntry 规则 (kmdf)
description: CtlDeviceFinishInitDrEntry 规则指定，是否驱动程序在 DriverEntry 回调函数中创建控制设备对象，它必须调用 WdfControlFinishInitializing，创建设备后，它从 EvtDriverDeviceAdd 退出之前回调函数。 此规则不适用于非 PnP 驱动程序。
ms.assetid: b6470bc1-c4db-4b46-b83b-edcf4da56087
ms.date: 05/21/2018
keywords:
- CtlDeviceFinishInitDrEntry 规则 (kmdf)
topic_type:
- apiref
api_name:
- CtlDeviceFinishInitDrEntry
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b23a1d4a2a5d713f638c7637f2ca6f7955cec2b8
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393189"
---
# <a name="ctldevicefinishinitdrentry-rule-kmdf"></a>CtlDeviceFinishInitDrEntry 规则 (kmdf)


CtlDeviceFinishInitDrEntry 规则指定如果驱动程序创建中的控制设备对象[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)回调函数，它必须调用[ **WdfControlFinishInitializing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)创建设备后，它从退出之前[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 此规则不适用于非 PnP 驱动程序。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>CtlDeviceFinishInitDrEntry</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)
[**WdfControlFinishInitializing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)
[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)
[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)
 

 





