---
title: 'InitFreeNull 规则 (kmdf) '
description: InitFreeNull 规则指定 \_ 无法使用指向 WDFDEVICE INIT 结构的 NULL 指针调用作为参数的 DDIs 接收 PWDFDEVICE init \_ 。
ms.assetid: 99ced415-9af9-4d06-a10f-4c960897ad5f
ms.date: 05/21/2018
keywords:
- 'InitFreeNull 规则 (kmdf) '
topic_type:
- apiref
api_name:
- InitFreeNull
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a44b6b86d9d4d47fbe355b47e9716a608a79133a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382639"
---
# <a name="initfreenull-rule-kmdf"></a>InitFreeNull 规则 (kmdf) 


**InitFreeNull**规则指定 \_ 无法使用指向[WDFDEVICE \_ INIT](../wdf/wdfdevice_init.md)结构的**NULL**指针调用作为参数的 DDIs 接收 PWDFDEVICE init。

框架提供的方法初始化 [WDFDEVICE \_ INIT](../wdf/wdfdevice_init.md) 结构。 当驱动程序调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 创建功能设备对象 (FDO) 或 (PDO) 的物理设备对象时， **WdfDeviceCreate** 方法会将第一个参数设置为 **NULL** （如果成功）。

如果驱动程序在调用设备对象初始化方法或 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)时遇到错误，则驱动程序必须调用 WdfDeviceInitFree。 成功调用 WdfDeviceInitFree 后，应将 [WDFDEVICE \_ init](../wdf/wdfdevice_init.md) 结构的指针设置为 **null** (PWDFDEVICE \_ INIT =**null**) 。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>InitFreeNull</strong> 规则。</p>
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
[**WdfDeviceInitFree**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree) 
[**WdfDeviceInitRegisterPnpStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback) 
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback) 
[**WdfDeviceInitRegisterPowerStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback) 
[**WdfPdoInitAddCompatibleID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid) 
[**WdfPdoInitAddDeviceText**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext) 
[**WdfPdoInitAddHardwareID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid) 
[**WdfPdoInitAssignDeviceID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid) 
[**WdfPdoInitAssignInstanceID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid) 
[**WdfPdoInitAssignRawDevice**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)另请参阅
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md) 
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md) 
[**InitFreeDeviceCreateType2**](kmdf-initfreedevicecreatetype2.md) 
[**PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md) 
[**InitFreeDeviceCreateType4**](kmdf-initfreedevicecreatetype4.md) 
[**PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md) 
[**PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md) 
[**PdoInitFreeDeviceCreateType4**](kmdf-pdoinitfreedevicecreatetype4.md)
 

