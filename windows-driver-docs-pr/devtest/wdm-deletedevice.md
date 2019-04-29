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
ms.openlocfilehash: eb4b84b429e319d2446b0188a18500932f757d24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363387"
---
# <a name="deletedevice-rule-wdm"></a>DeleteDevice 规则 (wdm)


**DeleteDevice**规则指定驱动程序不应依赖于 I/O 管理器或 PnP 管理器使 DeviceObject 保持活动状态后调用[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)。

驱动程序应调用[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)较低的驱动程序返回后。 这是建议的行为。 此规则适用于 FDO 和 FIDO 驱动程序。

在处理时[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求，该驱动程序应只调用[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)后[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)或者[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)返回。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DeleteDevice</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





