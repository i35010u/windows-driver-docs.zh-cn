---
title: C28114
description: 警告 C28114 复制整个 IRP 某些字段初始化个堆栈条目叶都应清除，或更新。
ms.assetid: 39e3e313-e40f-4cb9-a534-c9e74fd1e88b
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28114
ms.openlocfilehash: 7bab641cbf7f420e73c2e1574bd8bef686f25ec5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361437"
---
# <a name="c28114"></a>C28114


警告：C28114:复制整个 IRP 堆栈条目离开初始化，应清除或更新某些字段。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>使用<strong>IoCopyCurrentIrpStackLocationToNext</strong>来实现此目的</p></td>
</tr>
</tbody>
</table>

 

该驱动程序正在将 IRP 未正确复制。 未正确复制 IRP 可能会导致严重问题的驱动程序，包括丢失数据和系统崩溃。 如果必须复制 IRP 和[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)不满足需要，则 IRP 的某些成员不应复制或复制后应归零。

 

 





