---
title: C28156
description: 警告 C28156 实际的 IRQL 与所需 IRQL 不一致。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28156
ms.openlocfilehash: 51e2e4a72c43b55ea56c3fd0fec8e2d8befc2c75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793161"
---
# <a name="c28156"></a>C28156


警告 C28156：实际的 IRQL 与所需 IRQL 不一致

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>退出时的值未设置为所需的值。</p></td>
</tr>
</tbody>
</table>

 

**\_ IRQL \_ 要求 \_** 使用批注指定在函数完成时，驱动程序应以特定的 irql 执行，但至少有一个路径在函数完成时，在不同的 irql 下执行驱动程序。

 

 





