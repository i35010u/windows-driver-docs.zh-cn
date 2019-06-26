---
title: DeviceInitAPI 规则 (kmdf)
description: 对于对 FDO 设备，framework 设备对象初始化方法和 framework FDO 初始化方法必须在调用之前，驱动程序的设备对象调用 WdfDeviceCreate 方法。
ms.assetid: 526807b8-748e-4bc1-b795-9971ed98509c
ms.date: 05/21/2018
keywords:
- DeviceInitAPI 规则 (kmdf)
topic_type:
- apiref
api_name:
- DeviceInitAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f77512cc36650f5729e9c5ac968019ce4ebfaa69
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393184"
---
# <a name="deviceinitapi-rule-kmdf"></a>DeviceInitAPI 规则 (kmdf)


对于对 FDO 设备，framework 设备对象初始化方法和 framework FDO 初始化方法必须在调用之前驱动程序调用[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)设备方法对象。

FDO 设备、 framework 设备对象初始化方法和 framework FDO 初始化方法，用于存储区中的信息[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构，不能在驱动程序调用后调用[**WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate) framework 设备对象。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>DeviceInitAPI</strong>规则。</p>
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

[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)  
[**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)  
[**WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)  
[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)  
[**WdfDeviceInitRegisterPnpStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)  
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)  
[**WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)  
[**WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)  
[**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)  
[**WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)  
[**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)  
[**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)  
[**WdfDeviceInitSetIoInCallerContextCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)  
[**WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)  
[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)  
[**WdfDeviceInitSetPowerInrush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerinrush)  
[**WdfDeviceInitSetPowerNotPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)  
[**WdfDeviceInitSetPowerPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)  
[**WdfDeviceInitSetPowerPolicyEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)  
[**WdfDeviceInitSetPowerPolicyOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)  
[**WdfDeviceInitSetRequestAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)  
[**WdfFdoInitAllocAndQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty)  
[**WdfFdoInitOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)  
[**WdfFdoInitQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitqueryproperty)  
[**WdfFdoInitSetDefaultChildListConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)  
[**WdfFdoInitSetEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitseteventcallbacks)  
[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetfilter)  
[**WdfFdoInitWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitwdmgetphysicaldevice)  
 

 





