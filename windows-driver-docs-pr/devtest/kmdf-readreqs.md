---
title: ReadReqs 规则 (kmdf)
description: 读取请求 ReadReqs 规则指定将不传递到不适合 KMDF 方法。
ms.assetid: 96ab967b-976a-456b-b155-08732dd6700a
ms.date: 05/21/2018
keywords:
- ReadReqs 规则 (kmdf)
topic_type:
- apiref
api_name:
- ReadReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1849e9bd6f3dbc1bb4ab15298a97a55c307adef7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384101"
---
# <a name="readreqs-rule-kmdf"></a>ReadReqs 规则 (kmdf)


**ReadReqs**规则指定的读取请求将不传递到不适合 KMDF 方法。

提供给 EvtIoRead 回调中的驱动程序的所有请求都保证要读取的请求。 无法将这些读取的请求发送到以下 DDIs:

[**WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)

[**WdfIoTargetSendIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548660)

[**WdfIoTargetSendInternalIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548656)

[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548651)

[**WdfIoTargetSendWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548672)

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ReadReqs</strong>规则。</p>
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

[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548651)
[**WdfIoTargetSendInternalIoctlSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548656) 
 [ **WdfIoTargetSendIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548660)
[**WdfIoTargetSendWriteSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548672) 
[ **WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)
 

 





