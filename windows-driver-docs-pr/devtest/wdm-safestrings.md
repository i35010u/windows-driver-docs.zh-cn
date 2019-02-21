---
title: SafeStrings 规则 (wdm)
description: SafeStrings 规则指定驱动程序调用仅保护系统免受无意或恶意入侵这些字符串操作函数。 驱动程序这些安全的字符串函数 Ntstrsafe.h 中定义。
ms.assetid: 77e949cf-b184-4235-80c4-4718d4808d11
ms.date: 05/21/2018
keywords:
- SafeStrings 规则 (wdm)
topic_type:
- apiref
api_name:
- SafeStrings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b2b0d542473ecffe88968f770c5b03045856057
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519866"
---
# <a name="safestrings-rule-wdm"></a>SafeStrings 规则 (wdm)


**SafeStrings**规则指定驱动程序调用仅保护系统免受无意或恶意入侵这些字符串操作函数。 驱动程序这些安全的字符串函数 Ntstrsafe.h 中定义。

若要符合此规则，请使用被认为是安全的内核模式驱动程序的字符串函数。 中列出的安全字符串函数和不安全的函数，它们替换[**使用安全字符串函数**](https://msdn.microsoft.com/library/windows/hardware/ff565508)。 有两个组的安全字符串函数。 一组安全的字符串函数是在内核模式代码 （Ntstrsafe.h 中定义） 中使用。 另一组安全的字符串函数是在用户模式应用程序中使用，它们在 Strsafe.h 定义。

如果内核模式驱动程序将使用用户模式下安全字符串函数，该驱动程序与此规则冲突。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SafeStrings</strong>规则。</p>
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

<a name="see-also"></a>另请参阅
--------

[**使用安全的字符串函数**](https://msdn.microsoft.com/library/windows/hardware/ff565508)
 

 





