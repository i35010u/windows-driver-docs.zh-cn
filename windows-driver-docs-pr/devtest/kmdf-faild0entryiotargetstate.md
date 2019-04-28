---
title: FailD0EntryIoTargetState 规则 (kmdf)
description: FailD0EntryIoTargetState 规则指定 EvtDeviceD0Entry 中启动的 USB 持续读取器的 I/O 目标将获取停止适当地从同一回调是否 EvtDeviceD0Entry 失败。
ms.assetid: 7FB616EB-2079-42AE-A724-990EFBF3F84D
ms.date: 05/21/2018
keywords:
- FailD0EntryIoTargetState 规则 (kmdf)
topic_type:
- apiref
api_name:
- FailD0EntryIoTargetState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 991fb8b77a5fccce386683c7260a31c7cc304ba9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350410"
---
# <a name="faild0entryiotargetstate-rule-kmdf"></a>FailD0EntryIoTargetState 规则 (kmdf)


**FailD0EntryIoTargetState**规则指定的 I/O 目标的 USB 持续读取器中启动[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)获取适当地停止从同一个回调如果*EvtDeviceD0Entry*失败。

当[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)回调函数失败时，该框架不会执行的驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>FailD0EntryIoTargetState</strong>规则。</p>
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

[**WdfIoTargetStart**](https://msdn.microsoft.com/library/windows/hardware/ff548677)
[**WdfIoTargetStop**](https://msdn.microsoft.com/library/windows/hardware/ff548680)
[**WdfUsbTargetPipeConfigContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff551130)
[**WdfUsbTargetPipeGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff551146)
 

 





