---
title: DanglingDeviceObjectReference 规则 (wdm)
description: DanglingDeviceObjectReference 规则指定驱动程序使用相同的设备对象指针 IoGetAttachedDeviceReference 返回调用 ObDereferenceObject。
ms.assetid: b2aeaa16-f246-48c7-9e80-719d441a44ef
ms.date: 05/21/2018
keywords:
- DanglingDeviceObjectReference 规则 (wdm)
topic_type:
- apiref
api_name:
- DanglingDeviceObjectReference
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de23677b9e93415dc160004cf6e239cbe12e9903
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546073"
---
# <a name="danglingdeviceobjectreference-rule-wdm"></a>DanglingDeviceObjectReference 规则 (wdm)


**DanglingDeviceObjectReference**规则指定驱动程序调用[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)与同一个设备对象指针的[ **IoGetAttachedDeviceReference** ](https://msdn.microsoft.com/library/windows/hardware/ff549145)返回。

此规则还指定驱动程序通过调用所引用的所有设备对象指针**IoGetAttachedDeviceReference**通过调用取消引用**ObDereferenceObject**之前驱动程序将退出。 ObfDereferenceObject

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DanglingDeviceObjectReference</strong>规则。</p>
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

[**IoGetAttachedDeviceReference**](https://msdn.microsoft.com/library/windows/hardware/ff549145)
 

 





