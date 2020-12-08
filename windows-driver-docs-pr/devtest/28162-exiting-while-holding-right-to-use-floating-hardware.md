---
title: C28162
description: 在持有使用浮点硬件的权利时警告 C28162 退出。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28162
ms.openlocfilehash: 5925c7d07fc87c35d7ff927d56cbcabc9679883c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793145"
---
# <a name="c28162"></a>C28162


警告 C28162：在持有使用浮点硬件的权利时退出

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>已将此函数批注为已还原浮点。</p></td>
</tr>
</tbody>
</table>

 

**\_ 内核 \_ 浮点 \_ 还原 \_** 批注用于释放使用浮点的权限，但检测到通过函数的路径，但没有已知的函数可用于执行该操作。 此警告可能表明需要) 批注 **\_ 时 \_** 出现条件 (，或它可能指示编码错误。

 

 





