---
title: C28127
description: 警告 C28127 用作例程的函数与预期的类型不完全匹配。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28127
ms.openlocfilehash: 022eaf85a3fc85417ccfd738d71ede500a2a27cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840413"
---
# <a name="c28127"></a>C28127


警告 C28127：用作例程的函数与预期类型不完全匹配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>这可能是因为实际函数返回一个值，而预期的函数类型为 void</p></td>
</tr>
</tbody>
</table>

 

驱动程序将传递或分配函数 (指针) 类型 (即函数签名) 。 当函数的预期返回类型为 VOID，且实际提供) **int** 返回值 (隐含的函数时，通常会在 C 中出现这种情况。 当参数兼容但不完全相同时，也会发生这种情况。 通常情况下，回调函数应完全匹配预期的类型，这是使用函数 typedef 最容易实现的。

此类型不匹配消息主要用于验证代码分析工具是否可以识别回调。

 

 





