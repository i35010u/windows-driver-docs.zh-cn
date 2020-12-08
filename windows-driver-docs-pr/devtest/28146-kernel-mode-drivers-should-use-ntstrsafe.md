---
title: C28146
description: 警告 C28146 内核模式驱动程序应使用 ntstrsafe.h 而，而不是 strsafe。 在源文件中找到。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28146
ms.openlocfilehash: 217b3e939f72c781b2d5ac74e768825006a1e4cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793189"
---
# <a name="c28146"></a>C28146


警告 C28146：内核模式驱动程序应使用 ntstrsafe.h 而，而不是 strsafe。 在源文件中找到

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>标头 ntstrsafe.h 而包含在 strsafe 中找到的、适合在内核模式代码中使用的函数的版本。</p></td>
</tr>
</tbody>
</table>

 

内核模式驱动程序包含 Strsafe，而不是 Ntstrsafe.h 而。 有关 Ntstrsafe.h 而和 Strsafe 的信息，请参阅 [使用安全字符串函数](../kernel/using-safe-string-functions.md)。

 

