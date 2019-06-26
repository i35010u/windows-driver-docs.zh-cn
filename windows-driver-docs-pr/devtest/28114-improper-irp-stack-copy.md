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
ms.openlocfilehash: 574512fe4459111f41f538afcaec0d45b8f523f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364145"
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

 

该驱动程序正在将 IRP 未正确复制。 未正确复制 IRP 可能会导致严重问题的驱动程序，包括丢失数据和系统崩溃。 如果必须复制 IRP 和[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)不满足需要，则 IRP 的某些成员不应复制或复制后应归零。

 

 





