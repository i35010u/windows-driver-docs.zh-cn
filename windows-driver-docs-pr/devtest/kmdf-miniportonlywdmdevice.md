---
title: MiniportOnlyWdmDevice 规则 (kmdf)
description: MiniportOnlyWdmDevice 规则指定，WDF 驱动程序不应使用 IoCreateDevice 和 IoCreateDeviceSecure 函数创建裸机 WDM 设备对象。
ms.assetid: 23B9431E-3932-42F3-B797-0820D9A43295
ms.date: 05/21/2018
keywords:
- MiniportOnlyWdmDevice 规则 (kmdf)
topic_type:
- apiref
api_name:
- MiniportOnlyWdmDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81294b8bec4e679e8ae11ecedc4703798cfcc27e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392995"
---
# <a name="miniportonlywdmdevice-rule-kmdf"></a>MiniportOnlyWdmDevice 规则 (kmdf)


**MiniportOnlyWdmDevice**规则指定 WDF 驱动程序不应使用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)并[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)函数来创建裸机 WDM 设备对象。 这将导致计算机崩溃如果有人试图将 IRP 发送到 WDM 设备。 这是因为设备的 IRP 调度条目已设置为特定于 WDF 的条目，但该框架尚未创建 WDF 设备。 但是，微型端口驱动程序可以使用 DDIs，因为驱动程序调度入口点不为其设置。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>MiniportOnlyWdmDevice</strong>规则。</p>
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

[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)
[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)
[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)
 

 





