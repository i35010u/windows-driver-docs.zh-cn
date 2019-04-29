---
title: C28750
description: 警告 C28750 已禁止的 lstrlen 及其变体的使用情况。
ms.assetid: 5057FE71-286A-4710-922F-DFC639717C75
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28750
ms.openlocfilehash: a4f429c51ec7978b617049e6cad163037ce65e5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374737"
---
# <a name="c28750"></a>C28750


警告 C28750:已禁止的 lstrlen 及其变体的用法

此警告意味着，正在使用的函数已禁止，并具有更好的替换项。

无法传输操作期间发生的异常的 lstrlen 函数和相关的变体。 这会导致错误条件发生这种情况晚得多，可能在另一个线程，从而难以诊断的错误条件。 此外，等效的替代函数可由编译器进行优化和避免异常处理程序的性能开销 (**\_尝试**并**\_除**块)。

Lstrlen 函数和及其变体被阻止，因为它们无法传输异常。 正确的缓解操作是将它们转换为另一个字符串长度函数 (通常 strlen、 wcslen、 \_tcslen)。 但是，尽管查看 lstrlen 更改，您应确认字符串缓冲区来自受信任的代码。 如果处理不受信任数据时，应改为从切换到 strnlen 系列 （或 StringCchLength 系列） 的函数，它们将确保它们不会超过不受信任的数据块的边界的 strlen 系列。

与不同的 lstrlen，none 替换捕获的异常。 此外，lstrlen 允许为 NULL 指针，因此如果为 NULL 指针可能在 lstrlen 替换 strlen 或 strnlen 在代码中，显式 NULL 签入该点时需要。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">API</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="lstrlen"></span><span id="LSTRLEN"></span>lstrlen</p></td>
<td align="left"><p>受信任的数据替换选项： _tcslen</p>
<p>不受信任的数据替换： _tcsnlen，StringCchLength</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="lstrlenA"></span><span id="lstrlena"></span><span id="LSTRLENA"></span>lstrlenA</p></td>
<td align="left"><p>受信任的数据替换选项： strlen</p>
<p>不受信任的数据替换： strnlen、 StringCchLengthA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="lstrlenW"></span><span id="lstrlenw"></span><span id="LSTRLENW"></span>lstrlenW</p></td>
<td align="left"><p>受信任的数据替换选项： wcslen</p>
<p>不受信任的数据替换： wcsnlen、 StringCchLengthW</p></td>
</tr>
</tbody>
</table>

 

 

 





