---
title: IrpCancelField 规则 (wdm)
description: IrpCancelField 规则指定驱动程序时，它有挂起 IRP 上设置的取消例程检查 Irp-取消成员的值。
ms.assetid: e9221436-21ca-47f0-9dc4-e8b1a7a44854
ms.date: 05/21/2018
keywords:
- IrpCancelField 规则 (wdm)
topic_type:
- apiref
api_name:
- IrpCancelField
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55a3b6a4b76fa16fb6f562530175c31caf5c6b23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325377"
---
# <a name="irpcancelfield-rule-wdm"></a>IrpCancelField 规则 (wdm)


**IrpCancelField**规则指定驱动程序检查的值**Irp-&gt;取消**IRP 上设置在取消例程，它有挂起的成员。

Static Driver Verifier 适用此规则在驱动程序的末尾[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程和驱动程序的调度例程的末尾。

有关驱动程序应如何处理 IRP 取消的信息，请参阅[**同步 IRP 取消**](https://msdn.microsoft.com/library/windows/hardware/ff564531)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrpCancelField</strong>规则。</p>
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

[**IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)
[**IoCsqInsertIrpEx**](https://msdn.microsoft.com/library/windows/hardware/ff549067)
[**IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)
[**IoSetCancelRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549674) See also
--------

[**同步 IRP 取消**](https://msdn.microsoft.com/library/windows/hardware/ff564531)
 

 





