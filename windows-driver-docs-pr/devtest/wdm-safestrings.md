---
title: SafeStrings 规则（wdm）
description: SafeStrings 规则指定驱动程序只调用那些保护系统免受无意或恶意入侵的字符串操作函数。 驱动程序的这些安全字符串函数是在 Ntstrsafe.h 而中定义的。
ms.assetid: 77e949cf-b184-4235-80c4-4718d4808d11
ms.date: 05/21/2018
keywords:
- SafeStrings 规则（wdm）
topic_type:
- apiref
api_name:
- SafeStrings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0613e89440b7a10782e6d8908341bcb2765b5c33
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917202"
---
# <a name="safestrings-rule-wdm"></a>SafeStrings 规则（wdm）


**SafeStrings**规则指定驱动程序只调用那些保护系统免受无意或恶意入侵的字符串操作函数。 驱动程序的这些安全字符串函数是在 Ntstrsafe.h 而中定义的。

若要遵守此规则，请使用被视为对于内核模式驱动程序安全的字符串函数。 安全字符串函数及其替换的 unsafe 函数在[**使用安全字符串函数**](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)中列出。 有两组安全字符串函数。 一组安全字符串函数用于内核模式代码（在 Ntstrsafe.h 而中定义）。 另一组安全字符串函数在用户模式应用程序中使用，并在 Strsafe 中定义。

如果内核模式驱动程序使用用户模式安全字符串函数，则驱动程序将违反此规则。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>SafeStrings</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="see-also"></a>另请参阅
--------

[**使用安全字符串函数**](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)
 

 





