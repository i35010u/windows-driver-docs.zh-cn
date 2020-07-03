---
title: AddDevice 规则（wdm）
description: AddDevice 规则指定驱动程序的 AddDevice 例程仅在调用 IoCreateDevice 后才调用 IoAttachDeviceToDeviceStack。
ms.assetid: 6379633a-194f-45b8-8c21-85eecf300aeb
ms.date: 05/21/2018
keywords:
- AddDevice 规则（wdm）
topic_type:
- apiref
api_name:
- AddDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eff45ab446193ded0421562f69d69b565792c45f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916280"
---
# <a name="adddevice-rule-wdm"></a>AddDevice 规则（wdm）


**AddDevice**规则指定驱动程序的[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程仅在调用[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)后才调用[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) 。

此规则仅适用于具有[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的驱动程序。

此规则不会验证驱动程序是否调用**IoCreateDevice**或**IoAttachDeviceToDeviceStack** ，且不会监视对[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)的调用。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>AddDevice</strong>规则。</p>
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

[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) 
[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)
 

 





