---
title: FwdIrpToIoQueueValid 规则 (kmdf)
description: 规则 FwdIrpToIoQueueValid 指定驱动程序将 IRP 发送到的 I/O 队列，使用从 EvtDeviceWdmIrpDispatch 回调或 EvtDeviceWdmIrpPreprocess 回调 WdfDeviceWdmDispatchIrpToIoQueue 方法。
ms.assetid: 338A1577-AD16-4632-BD8D-C9FDBC4FCDBD
ms.date: 05/21/2018
keywords:
- FwdIrpToIoQueueValid 规则 (kmdf)
topic_type:
- apiref
api_name:
- FwdIrpToIoQueueValid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 62dbc3ca0c9138e494f2265d17ba78e7e11151c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356439"
---
# <a name="fwdirptoioqueuevalid-rule-kmdf"></a>FwdIrpToIoQueueValid 规则 (kmdf)


该规则**FwdIrpToIoQueueValid**指定驱动程序将 IRP 发送到一个 I/O 排队，请使用[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)从任一方法[*EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调或[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>FwdIrpToIoQueueValid</strong>规则。</p>
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

[**WdfDeviceWdmDispatchIrpToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/hh451105)
 

 





