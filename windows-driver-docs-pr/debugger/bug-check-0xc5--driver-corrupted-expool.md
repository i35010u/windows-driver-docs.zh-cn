---
title: Bug 检查 0xC5 DRIVER_CORRUPTED_EXPOOL
description: DRIVER_CORRUPTED_EXPOOL bug 检查具有 0x000000C5 值。 这表示系统尝试访问无效内存过高的 IRQL 的进程时。
ms.assetid: e375e7d3-9cb1-474f-ade2-1bc65dd79864
keywords:
- Bug 检查 0xC5 DRIVER_CORRUPTED_EXPOOL
- DRIVER_CORRUPTED_EXPOOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_EXPOOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 113612c470706a72ae3d53e15a51f0da6b4d86a4
ms.sourcegitcommit: 6c485b8f350dadc1b44d85cfd9fa49e5e5663406
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67266385"
---
# <a name="bug-check-0xc5-drivercorruptedexpool"></a>Bug 检查 0xC5：驱动程序\_损坏\_EXPOOL


该驱动程序\_损坏\_EXPOOL bug 检查的值为 0x000000C5。 这表示系统尝试访问无效内存过高的 IRQL 的进程时。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="drivercorruptedexpool-parameters"></a>驱动程序\_损坏\_EXPOOL 参数


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
<td align="left"><p>在引用的时间的 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>引用内存的地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

尝试访问可分页内存 （或可能是完全无效的内存） 内核 IRQL 时过高。 此问题的最终原因几乎可以肯定是损坏了系统池的驱动程序。

在大多数情况下，此 bug 检查结果如果驱动程序损坏了一个小的分配 (小于页面\_大小)。 更大的分配会导致[ **bug 检查 0xD0** ](bug-check-0xd0--driver-corrupted-mmpool.md) (驱动程序\_损坏\_MMPOOL)。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。 如果您最近安装了任何新的软件，检查以查看是否已正确安装。 检查更新的驱动程序制造商的网站上。

若要调试此错误，使用驱动程序验证程序的特殊池选项。 如果该操作未显示导致该错误的驱动程序，使用全局标志实用工具启用特殊的池的池标记。

有关特殊的池的信息，请查阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier) Windows 驱动程序工具包的一部分。

 

 




