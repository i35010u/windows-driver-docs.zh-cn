---
title: C28114
description: 警告 C28114 复制整个 IRP 堆栈条目时，应清除或更新的某些字段已初始化。
ms.assetid: 39e3e313-e40f-4cb9-a534-c9e74fd1e88b
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28114
ms.openlocfilehash: 924409277079cecf27d8451a2ebbcf23b3f08b61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839602"
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
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>使用<strong>IoCopyCurrentIrpStackLocationToNext</strong>完成此</p></td>
</tr>
</tbody>
</table>

 

驱动程序复制 IRP 不正确。 复制 IRP 不当可能会导致驱动程序出现严重问题，包括数据丢失和系统崩溃。 如果必须复制 IRP 并且[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)无法满足需要，则 irp 的某些成员不应复制，也不应在复制后归零。

 

 





