---
title: C28146
description: 警告 C28146 内核模式驱动程序应使用 ntstrsafe.h 而，而不是 strsafe。 在源文件中找到。
ms.assetid: 00e3e96e-b31b-4060-8193-d69b7cca8181
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28146
ms.openlocfilehash: 4962ec22aee4692cdd3b55812fc4605fe3ec8f51
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383541"
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

 

