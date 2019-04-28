---
title: DoubleExFreePool 规则 (storport)
description: 此规则将验证该驱动程序不会尝试两次免费的相同池内存块。
ms.assetid: D7EAD257-02CA-418C-B67D-FADCB4F7A6C1
ms.date: 05/21/2018
keywords:
- DoubleExFreePool 规则 (storport)
topic_type:
- apiref
api_name:
- DoubleExFreePool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d45f226cf622c18ffa9d66b5b5fbfc47d744c8ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345751"
---
# <a name="doubleexfreepool-rule-storport"></a>DoubleExFreePool 规则 (storport)


此规则将验证该驱动程序不会尝试两次免费的相同池内存块。

规则跟踪的第一次传递到的内存指针**ExFreePool**。 如果再次传递相同的指针，则该驱动程序未能通过该规则。 如果该驱动程序调用**RemoveHeadList**或**RemoveEntryList**，规则将传递。

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DoubleExFreePool</strong>规则。</p>
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

[**ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)
[**RemoveEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff561029)
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





