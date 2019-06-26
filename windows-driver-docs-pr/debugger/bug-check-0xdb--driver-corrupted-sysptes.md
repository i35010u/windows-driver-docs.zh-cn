---
title: Bug 检查 0xDB DRIVER_CORRUPTED_SYSPTES
description: DRIVER_CORRUPTED_SYSPTES bug 检查具有 0x000000DB 值。 这表示尝试内存时，无效的 IRQL，很可能是由于系统 Pte 的损坏。
ms.assetid: f21a7582-c665-4677-851b-702888d9fe13
keywords:
- Bug 检查 0xDB DRIVER_CORRUPTED_SYSPTES
- DRIVER_CORRUPTED_SYSPTES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_SYSPTES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 01cb478d7c6e5ab8f37930cf03f91c10e50411d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361565"
---
# <a name="bug-check-0xdb-drivercorruptedsysptes"></a>Bug 检查 0xDB：驱动程序\_损坏\_SYSPTES


该驱动程序\_损坏\_SYSPTES bug 检查的值为 0x000000DB。 这表示尝试内存时，无效的 IRQL，很可能是由于系统 Pte 的损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="drivercorruptedsysptes-parameters"></a>驱动程序\_损坏\_SYSPTES 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>在代码中引用的内存地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序尝试访问在可分页 （或完全无效） 内存过高的 IRQL。 此 bug 检查几乎总是引起的损坏系统 Pte 驱动程序。

<a name="resolution"></a>分辨率
----------

如果发生此错误检查，可以通过编辑注册表检测到问题所在。 在中 **\\ \\HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\内存管理**注册表项，创建或编辑**TrackPtes**值，并将其设置为等于 DWORD 3。 然后重新启动。 系统然后将保存的堆栈跟踪，并且如果该驱动程序提交相同的错误，则系统将发出[ **bug 检查 0xDA** ](bug-check-0xda--system-pte-misuse.md) (系统\_PTE\_误用)。 然后堆栈跟踪将标识导致错误的驱动程序。

 

 




