---
title: C28156
description: 警告 C28156 实际 IRQL 是与所需的 IRQL 不一致。
ms.assetid: dc9c108f-adf1-4364-9d2b-711c8c9db939
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28156
ms.openlocfilehash: 21851e4e6fb8a9b1af265a6309b9a6a17a3ddd7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361508"
---
# <a name="c28156"></a>C28156


警告 C28156:实际 IRQL 是与所需的 IRQL 不一致

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>在退出时的值未设置为所需的值。</p></td>
</tr>
</tbody>
</table>

 

 **\_IRQL\_需要\_** 批注指定当该函数完成后，但该驱动程序是在其中至少一个路径时，驱动程序，应在特定的 IRQL 执行在不同的 IRQL 在函数完成时执行。

 

 





