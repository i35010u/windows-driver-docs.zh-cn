---
title: MarkStartDevice 规则（wdm）
description: MarkStartDevice 规则指定驱动程序 pends IRP \_ MN \_ \_ 正确启动设备 IRP。 此规则仅适用于 FDO 和 FIDO 驱动程序。
ms.assetid: ABFE062D-37A7-4931-961C-76092D7C05B7
ms.date: 05/21/2018
keywords:
- MarkStartDevice 规则（wdm）
topic_type:
- apiref
api_name:
- MarkStartDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6230b3208d68079ff1bdff8fdf05a44028f0fac
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917268"
---
# <a name="markstartdevice-rule-wdm"></a>MarkStartDevice 规则（wdm）


**MarkStartDevice**规则指定驱动程序 pends irp \_ MN \_ \_ 正确启动设备 IRP。 此规则仅适用于 FDO 和 FIDO 驱动程序。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>MarkStartDevice</strong>规则。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 
[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) 
[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification) 
[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 
[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





