---
title: C28162
description: 警告 C28162 退出同时保留使用浮点硬件的权限。
ms.assetid: e5e12470-4b38-457e-91a2-aae4b21ee466
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28162
ms.openlocfilehash: dcbb74dbc12e3923ff1ef7baa14f358e1f73d567
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361335"
---
# <a name="c28162"></a>C28162


警告 C28162:退出同时保留使用浮点硬件的权限

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>此函数已批注退出并还原的浮点数。</p></td>
</tr>
</tbody>
</table>

 

**\_内核\_float\_还原\_** 批注用来释放使用浮点数的权限，但其中没有已知的函数检测到通过函数的路径执行成功调用操作。 此警告可能表示的条件 (**\_时\_**) 需要批注，或者它可能指示编码错误。

 

 





