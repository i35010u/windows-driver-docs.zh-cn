---
title: C28161
description: 而无需获取使用浮点硬件的权限的警告 C28161 退出。
ms.assetid: 4132409d-10aa-4014-a2d9-77c62e137795
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28161
ms.openlocfilehash: 4e0dcc8479f32f2a66301c67047e9ce03d0dc324
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361330"
---
# <a name="c28161"></a>C28161


警告 C28161:正在退出而不获取使用浮点硬件的权限

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>此函数已批注退出并可用的浮点数。</p></td>
</tr>
</tbody>
</table>

 

**\_内核\_float\_保存\_** 批注用于获取使用浮点数的权限，但其中没有已知要执行的函数检测到通过函数的路径操作已成功调用。 此警告可能表示的条件 (**\_时\_**) 需要批注，或者它可能指示编码错误。

 

 





