---
title: C28161
description: 警告 C28161 在不获取使用浮动硬件的权限的情况下退出。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28161
ms.openlocfilehash: 181fdca49f55836e1ec35dc532831537f78079df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793149"
---
# <a name="c28161"></a>C28161


警告 C28161：在未获取使用浮动硬件的权限的情况下退出

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>已将此函数批注为在可用浮点点退出。</p></td>
</tr>
</tbody>
</table>

 

**\_ 内核 \_ 浮点 \_ 保存 \_** 批注用于获取使用浮点的权限，但检测到通过函数的路径，但没有已知的函数可用于执行该操作。 此警告可能表明需要) 批注 **\_ 时 \_** 出现条件 (，或它可能指示编码错误。

 

 





