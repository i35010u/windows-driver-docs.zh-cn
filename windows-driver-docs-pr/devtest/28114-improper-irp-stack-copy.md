---
title: C28114
description: 警告 C28114 复制整个 IRP 堆栈条目时，应清除或更新的某些字段已初始化。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28114
ms.openlocfilehash: a2fb6b48194224517d3581f6d23bf75f22317dd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837817"
---
# <a name="c28114"></a>C28114


警告： C28114：复制整个 IRP 堆栈条目会将某些字段初始化，应清除或更新这些字段。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>使用 <strong>IoCopyCurrentIrpStackLocationToNext</strong> 完成此</p></td>
</tr>
</tbody>
</table>

 

驱动程序复制 IRP 不正确。 复制 IRP 不当可能会导致驱动程序出现严重问题，包括数据丢失和系统崩溃。 如果必须复制 IRP 并且 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) 无法满足需要，则 irp 的某些成员不应复制，也不应在复制后归零。

 

