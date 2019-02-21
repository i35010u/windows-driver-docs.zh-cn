---
title: DeviceCreateFail 规则 (kmdf)
description: DeviceCreateFail 规则指定的 EVT\_WDF\_驱动程序\_设备\_添加对 WdfDeviceCreate 调用失败时返回的错误状态。
ms.assetid: 07272d72-d9a2-42b2-b89b-c7bc903c1425
ms.date: 05/21/2018
keywords:
- DeviceCreateFail 规则 (kmdf)
topic_type:
- apiref
api_name:
- DeviceCreateFail
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b2ca5d4005acd0b811bb63d4da66d00bc2b3680
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522993"
---
# <a name="devicecreatefail-rule-kmdf"></a>DeviceCreateFail 规则 (kmdf)


**DeviceCreateFail**规则指定的 EVT\_WDF\_驱动程序\_设备\_添加返回的错误状态时调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)失败。

对于服务设备的驱动程序，必须已成功创建设备对象。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DeviceCreateFail</strong>规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
 

 





