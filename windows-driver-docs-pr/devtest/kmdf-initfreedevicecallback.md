---
title: InitFreeDeviceCallback 规则 (kmdf)
description: InitFreeDeviceCallback 规则指定如果驱动程序时遇到错误时它可以初始化新的 framework 设备对象，和驱动程序收到 WDFDEVICE 驱动程序，必须调用 WdfDeviceInitFree\_调用 INIT 结构WdfControlDeviceInitAllocate。
ms.assetid: 518f60cf-283a-4924-8bbd-2f5e26d3e850
ms.date: 05/21/2018
keywords:
- InitFreeDeviceCallback 规则 (kmdf)
topic_type:
- apiref
api_name:
- InitFreeDeviceCallback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8850213bb4773300918c25b02817217070244069
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393261"
---
# <a name="initfreedevicecallback-rule-kmdf"></a>InitFreeDeviceCallback 规则 (kmdf)


InitFreeDeviceCallback 规则指定一个驱动程序必须调用[ **WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)如果驱动程序时遇到错误时它可以初始化新的 framework 设备对象，和驱动程序收到[ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)调用结构[ **WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>InitFreeDeviceCallback</strong>规则。</p>
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
[**WdfDeviceInitAssignName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname) 
 [ **WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)
[**WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback) 
 [**WdfDeviceInitFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)
[**WdfDeviceInitRegisterPnpStateChangeCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback) 
 [ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)
[**WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback) 
 [ **WdfPdoInitAddCompatibleID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid)
[**WdfPdoInitAddDeviceText** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext)
 [ **WdfPdoInitAddHardwareID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid)
[**WdfPdoInitAssignDeviceID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid)
 [ **WdfPdoInitAssignInstanceID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid)
[**WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)
 

 





