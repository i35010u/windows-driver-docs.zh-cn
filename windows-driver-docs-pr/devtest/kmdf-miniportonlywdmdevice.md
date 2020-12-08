---
title: 'MiniportOnlyWdmDevice 规则 (kmdf) '
description: MiniportOnlyWdmDevice 规则指定 WDF 驱动程序不应使用 IoCreateDevice 和 IoCreateDeviceSecure 函数创建裸机设备对象。
ms.date: 05/21/2018
keywords:
- 'MiniportOnlyWdmDevice 规则 (kmdf) '
topic_type:
- apiref
api_name:
- MiniportOnlyWdmDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c381d08e36f323e7a70784f265d9dfefd2f62534
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839001"
---
# <a name="miniportonlywdmdevice-rule-kmdf"></a>MiniportOnlyWdmDevice 规则 (kmdf) 


**MiniportOnlyWdmDevice** 规则指定 WDF 驱动程序不应使用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)和 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)函数创建裸机设备对象。 如果有人尝试将 IRP 发送到 WDM 设备，这将导致计算机崩溃。 这是因为，将设备的 IRP 调度条目设置为特定于 WDF 的条目，但框架尚未创建 WDF 设备。 但微型端口驱动程序可以使用 DDIs，因为没有为其设置驱动程序调度入口点。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>MiniportOnlyWdmDevice</strong> 规则。</p>
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

[**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 
[**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 
[**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)
