---
title: C28146
description: 警告 C28146 内核模式驱动程序应使用 ntstrsafe.h，不 strsafe.h。 在源文件中找到。
ms.assetid: 00e3e96e-b31b-4060-8193-d69b7cca8181
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28146
ms.openlocfilehash: 4821f4657117e0ed28071d24a72b80fabf02bbfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547660"
---
# <a name="c28146"></a>C28146


警告 C28146:内核模式驱动程序应使用 ntstrsafe.h，不 strsafe.h。 在源文件中找到

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>标头 ntstrsafe.h 包含适用于内核模式代码中使用该函数在 strsafe.h 中找到的版本。</p></td>
</tr>
</tbody>
</table>

 

内核模式驱动程序包括 Strsafe.h，而不是 Ntstrsafe.h。 有关 Ntstrsafe.h 和 Strsafe.h 信息，请参阅[使用安全字符串函数](https://msdn.microsoft.com/library/windows/hardware/ff565508)。

 

 





