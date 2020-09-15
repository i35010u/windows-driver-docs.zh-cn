---
title: 'SafeStrings 规则 (wdm) '
description: SafeStrings 规则指定驱动程序只调用那些保护系统免受无意或恶意入侵的字符串操作函数。 驱动程序的这些安全字符串函数是在 Ntstrsafe.h 而中定义的。
ms.assetid: 77e949cf-b184-4235-80c4-4718d4808d11
ms.date: 05/21/2018
keywords:
- 'SafeStrings 规则 (wdm) '
topic_type:
- apiref
api_name:
- SafeStrings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1f8357f5ca0c4ed8a7a17ec6e024ea95c7d56b1a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102452"
---
# <a name="safestrings-rule-wdm"></a>SafeStrings 规则 (wdm) 


**SafeStrings**规则指定驱动程序只调用那些保护系统免受无意或恶意入侵的字符串操作函数。 驱动程序的这些安全字符串函数是在 Ntstrsafe.h 而中定义的。

若要遵守此规则，请使用被视为对于内核模式驱动程序安全的字符串函数。 安全字符串函数及其替换的 unsafe 函数在 [**使用安全字符串函数**](../kernel/using-safe-string-functions.md)中列出。 有两组安全字符串函数。 一组安全字符串函数用于在 Ntstrsafe.h 而) 中定义 (内核模式代码。 另一组安全字符串函数在用户模式应用程序中使用，并在 Strsafe 中定义。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>SafeStrings</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="see-also"></a>请参阅
--------

[**使用安全字符串函数**](../kernel/using-safe-string-functions.md)
