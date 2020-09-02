---
title: 'PdoDeviceInitAPI 规则 (kmdf) '
description: PdoDeviceInitAPI 规则指定 WdfPdoInitAllocate 和所有其他设备对象初始化 DDIs 为 \_ 物理设备对象设置 WDFDEVICE INIT 结构 (PDO) 必须在驱动程序为 pdo 调用 WdfDeviceCreate 之前调用它。
ms.assetid: 6a2e6e82-7fac-4366-a46d-1bd80d3bf92e
ms.date: 05/21/2018
keywords:
- 'PdoDeviceInitAPI 规则 (kmdf) '
topic_type:
- apiref
api_name:
- PdoDeviceInitAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ba2c0b5bd6f0ae59911131ce1701d1aefeec3b7
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381965"
---
# <a name="pdodeviceinitapi-rule-kmdf"></a>PdoDeviceInitAPI 规则 (kmdf) 


**PdoDeviceInitAPI**规则指定[**WdfPdoInitAllocate**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)和所有其他设备对象初始化 DDIs 为物理设备对象设置[**WDFDEVICE \_ INIT**](../wdf/wdfdevice_init.md)结构 (PDO) 必须在驱动程序为 pdo 调用[**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之前调用它。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>PdoDeviceInitAPI</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)  
[**WdfDeviceInitAssignName**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)  
[**WdfDeviceInitAssignSDDLString**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)  
[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)  
[**WdfDeviceInitRegisterPnpStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)  
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)  
[**WdfDeviceInitRegisterPowerStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)  
[**WdfDeviceInitSetCharacteristics**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)  
[**WdfDeviceInitSetDeviceClass**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)  
[**WdfDeviceInitSetDeviceType**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)  
[**WdfDeviceInitSetExclusive**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)  
[**WdfDeviceInitSetFileObjectConfig**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)  
[**WdfDeviceInitSetIoInCallerContextCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)  
[**WdfDeviceInitSetIoType**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)  
[**WdfDeviceInitSetPnpPowerEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)  
[**WdfDeviceInitSetPowerInrush**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerinrush)  
[**WdfDeviceInitSetPowerNotPageable**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)  
[**WdfDeviceInitSetPowerPageable**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)  
[**WdfDeviceInitSetPowerPolicyEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)  
[**WdfDeviceInitSetPowerPolicyOwnership**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)  
[**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)  
[**WdfFdoRetrieveNextStaticChild**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoretrievenextstaticchild)  
[**WdfPdoInitAddCompatibleID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid)  
[**WdfPdoInitAddDeviceText**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext)  
[**WdfPdoInitAddHardwareID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid)  
[**WdfPdoInitAllocate**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)  
[**WdfPdoInitAssignDeviceID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid)  
[**WdfPdoInitAssignInstanceID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid)  
[**WdfPdoInitAssignRawDevice**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)  
[**WdfPdoInitSetDefaultLocale**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitsetdefaultlocale)  
[**WdfPdoInitSetEventCallbacks**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitseteventcallbacks)  
 

