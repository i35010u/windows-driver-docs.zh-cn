---
title: Bug 检查 0x20 KERNEL_APC_PENDING_DURING_EXIT
description: KERNEL_APC_PENDING_DURING_EXIT bug 检查的值为0x00000020。 这表示在线程退出时，异步过程调用（APC）仍处于挂起状态。
ms.assetid: 0ef7c2b2-0864-4206-b786-bac9df9cedc7
keywords:
- Bug 检查 0x20 KERNEL_APC_PENDING_DURING_EXIT
- KERNEL_APC_PENDING_DURING_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_APC_PENDING_DURING_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4b919df6dd569d53c1a0413a8608bc4dd1709851
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534826"
---
# <a name="bug-check-0x20-kernel_apc_pending_during_exit"></a>Bug 检查0x20： \_ \_ \_ 退出期间内核 APC \_ 挂起


\_ \_ 退出 bug 检查期间等待的内核 APC 的 \_ \_ 值为0x00000020。 这表示在线程退出时，异步过程调用（APC）仍处于挂起状态。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="kernel_apc_pending_during_exit-parameters"></a>\_ \_ \_ 在 \_ 退出参数期间内核 APC 挂起


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>退出过程中发现的 APC 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>线程的 APC 禁用计数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>当前 IRQL</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Key data 项是线程的 APC 禁用计数（参数2）。 如果计数为非零，则它将指示问题的根源。

每次驱动程序调用**KeEnterCriticalRegion**、 **FsRtlEnterFileSystem**或获取互斥体时，APC 禁用计数都将减少。

每次驱动程序调用**KeLeaveCriticalRegion**、 **KeReleaseMutex**或**FsRtlExitFileSystem**时，APC 禁用计数都将递增。

由于这些调用应始终成对出现，因此在线程退出时，APC 禁用计数应为零。 负值表示驱动程序已禁用 APC 调用，而无需重新启用它们。 正值指示反转为 true。

如果你看到此错误，则非常怀疑计算机上安装的所有驱动程序-特别是异常或非标准驱动程序。

当前 IRQL （参数3）应为零。 如果不是这样，则驱动程序的取消例程可能会通过返回提升的 IRQL 来导致此 bug 检查。 在这种情况下，请仔细记下发生崩溃时正在运行的内容（以及关闭的内容），并在发生故障时记下所有已安装的驱动程序。 这种情况的原因通常是驱动程序中的严重错误。


## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 




