---
title: C28750
description: 警告 C28750 禁止使用 lstrlen 及其变种。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28750
ms.openlocfilehash: 9344fad1f0c9fbddf4ff8297f4cb523d445b58f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784087"
---
# <a name="c28750"></a>C28750


警告 C28750： lstrlen 及其变体的禁止使用情况

此警告意味着使用的函数已被禁止，并具有更好的替换项。

Lstrlen 函数和相关变体无法传输在操作过程中发生的异常。 这可能会导致以后出现错误情况（可能出现在不同的线程上），从而使错误条件更难诊断。 此外，可通过编译器优化等效的替换函数，并避免 (**\_ try** 和 **\_ except** 块) 的异常处理程序的性能开销。

Lstrlen 函数及其变量将被禁止，因为它们无法传输异常。 正确的缓解措施是将它们转换为其他字符串长度函数 (通常为 strlen、wcslen、 \_ tcslen) 。 但是，当你查看 lstrlen 更改时，你应确认字符串缓冲区来自受信任的代码。 如果处理的是不受信任的数据，则应改为从 strlen 系列的函数切换到 strnlen 系列 (或 StringCchLength 家族) ，这将确保它们不会超出不受信任的数据块的界限。

与 lstrlen 不同，任何替换都不会捕获异常。 此外，lstrlen 允许使用 NULL 指针，因此，如果在代码中的该点可能出现空指针，则将 lstrlen 替换为 strlen 或 strnlen 时，需要显式 NULL 检查。

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
<p>不受信任的数据替换： strnlen、StringCchLengthA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="lstrlenW"></span><span id="lstrlenw"></span><span id="LSTRLENW"></span>lstrlenW</p></td>
<td align="left"><p>受信任的数据替换选项： wcslen</p>
<p>不受信任的数据替换： wcsnlen、StringCchLengthW</p></td>
</tr>
</tbody>
</table>

 

 

 





