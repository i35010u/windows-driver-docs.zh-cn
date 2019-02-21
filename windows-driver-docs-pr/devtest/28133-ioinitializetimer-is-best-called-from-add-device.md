---
title: C28133
description: 警告 C28133 最好最好从 AddDevice 调用。
ms.assetid: c832cf67-1fc2-491b-a9e3-d35c5d9f6b73
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28133
ms.openlocfilehash: 0ed3998850b8ea85fa62039ae5d5cdc07695c68c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542682"
---
# <a name="c28133"></a>C28133


警告 C28133:最好最好从 AddDevice 调用

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>最好仅每个设备对象调用一次。 从 AddDevice 调用该例程还有助于确保，它不意外调用一次以上。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序调用[**最好**](https://msdn.microsoft.com/library/windows/hardware/ff549344)以外的其他例程中其**AddDevice**例程。 代码分析工具使用此机会来建议的最佳做法建议，可以避免错误并使驱动程序代码更可靠。

 

 





