---
title: DeleteDevice 规则 (wdm)
description: DeleteDevice 规则指定驱动程序不应依赖于 I/O 管理器或 PnP 管理器使 DeviceObject IoDeleteDevice 调用后保持活动状态。
ms.assetid: C7068AD1-C9F4-4BB0-8964-24FFB4658AF6
ms.date: 05/21/2018
keywords:
- DeleteDevice 规则 (wdm)
topic_type:
- apiref
api_name:
- DeleteDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 13b65263b53cc6639acbf359fa69a5b03f56f93c
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393991"
---
# <a name="deletedevice-rule-wdm"></a>DeleteDevice 规则 (wdm)


**DeleteDevice**规则指定驱动程序不应依赖于 I/O 管理器或 PnP 管理器使 DeviceObject 保持活动状态后调用[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)。

驱动程序应调用[ **IoDeleteDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)较低的驱动程序返回后。 这是建议的行为。 此规则适用于 FDO 和 FIDO 驱动程序。

在处理时[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求，该驱动程序应只调用[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)后[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)或者[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)返回。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>DeleteDevice</strong>规则。</p>
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

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)
 

 





