---
title: C28127
description: 警告 C28127 作为例程所使用的函数与预期的类型不完全匹配。
ms.assetid: ae8f554b-c1e1-42a7-b1ad-c5554af25953
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28127
ms.openlocfilehash: 2018d426dbcc0a1dfcca37e62d9e1fa943b4f9b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545865"
---
# <a name="c28127"></a>C28127


警告 C28127:作为例程所使用的函数与预期的类型不完全匹配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>可能的区别是实际的函数返回一个值，并应为的函数类型是 void</p></td>
</tr>
</tbody>
</table>

 

驱动程序传递或分配了意外的类型 （即，函数签名） 的函数 （指针）。 这通常发生在 C 中预期的返回函数的类型为 VOID，以及对于 （隐式） 的函数**int**返回实际提供值。 它还可能当参数都兼容，但不是完全相同。 一般情况下，回调函数应预期的类型完全匹配，这非常轻松地实现使用函数 typedef。

此类型不匹配消息主要用于验证代码分析工具可以识别的回调。

 

 





