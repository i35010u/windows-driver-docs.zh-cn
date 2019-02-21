---
title: IoBuildDeviceControlWait 规则 (wdm)
description: IoBuildDeviceControlWait 规则指定是否 IoCallDriver 或 PoCallDriver 返回状态，应调用 KeWaitForSingleObject 例程\_PENDING。
ms.assetid: F1AC3698-EA1F-400D-B2B2-3FD9B8E0FE75
ms.date: 05/21/2018
keywords:
- IoBuildDeviceControlWait 规则 (wdm)
topic_type:
- apiref
api_name:
- IoBuildDeviceControlWait
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b6e11f6f41c2e79b116f755a44e27215711e4c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520557"
---
# <a name="iobuilddevicecontrolwait-rule-wdm"></a>IoBuildDeviceControlWait 规则 (wdm)


**IoBuildDeviceControlWait**规则指定[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)如果应调用例程[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)将返回状态\_PENDING。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoBuildDeviceControlWait</strong>规则。</p>
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

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)
[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
[**KeWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





