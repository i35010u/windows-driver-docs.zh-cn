---
title: InitFreeDeviceCreateType2 规则（kmdf）
description: InitFreeDeviceCreateType2 规则指定驱动程序在调用 WdfDeviceInitFree 后不得调用 WdfDeviceCreate。
ms.assetid: 43defbbb-ab5e-4c3e-bb9d-fdcbe203c617
ms.date: 05/21/2018
keywords:
- InitFreeDeviceCreateType2 规则（kmdf）
topic_type:
- apiref
api_name:
- InitFreeDeviceCreateType2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1fe9482a65f8b6432bb0ede1c3fc740e2b5e5e89
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917001"
---
# <a name="initfreedevicecreatetype2-rule-kmdf"></a>InitFreeDeviceCreateType2 规则（kmdf）


InitFreeDeviceCreateType2 规则指定驱动程序在调用[**WdfDeviceInitFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)后不得调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>InitFreeDeviceCreateType2</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate) 
[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 
[**WdfDeviceInitFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)另请参阅
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md) 
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md) 
[**PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md) 
[**InitFreeDeviceCreateType4**](kmdf-initfreedevicecreatetype4.md) 
[**PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md) 
[**PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md) 
[**PdoInitFreeDeviceCreateType4**](kmdf-pdoinitfreedevicecreatetype4.md) 
[**InitFreeNull**](kmdf-initfreenull.md)
 

 





