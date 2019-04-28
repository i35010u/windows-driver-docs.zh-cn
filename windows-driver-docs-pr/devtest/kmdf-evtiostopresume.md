---
title: EvtIoStopResume 规则 (kmdf)
description: EvtIoStopResume 规则指定是否驱动程序注册 EvtIoStop 回调函数，然后使用重新排队参数等于 FALSE 调用 WdfRequestStopAcknowledge，驱动程序必须注册 EvtIoResume 回调函数。
ms.assetid: 52bcaf8a-545c-4607-89c3-d4474bd50376
ms.date: 05/21/2018
keywords:
- EvtIoStopResume 规则 (kmdf)
topic_type:
- apiref
api_name:
- EvtIoStopResume
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b3d9d22c0df4c9b80b5e8a67b0344bdc464c3ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340327"
---
# <a name="evtiostopresume-rule-kmdf"></a>EvtIoStopResume 规则 (kmdf)


**EvtIoStopResume**规则指定如果驱动程序注册[ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)回调函数，然后调用[ **WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)与*重新排队*参数等于**FALSE**，该驱动程序必须注册[ *EvtIoResume* ](https://msdn.microsoft.com/library/windows/hardware/ff541779)回调函数。 框架提供的请求**EvtIoResume**设备再次进入 D0 状态时的回调函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>EvtIoStopResume</strong>规则。</p>
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

[**WdfRequestStopAcknowledge**](https://msdn.microsoft.com/library/windows/hardware/ff550033)
 

 





