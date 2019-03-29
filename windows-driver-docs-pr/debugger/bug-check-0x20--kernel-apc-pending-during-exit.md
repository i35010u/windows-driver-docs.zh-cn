---
title: Bug Check 0x20 KERNEL_APC_PENDING_DURING_EXIT
description: KERNEL_APC_PENDING_DURING_EXIT bug 检查具有 0x00000020 值。 这表明异步过程调用 (APC) 仍是挂起的线程在退出时。
ms.assetid: 0ef7c2b2-0864-4206-b786-bac9df9cedc7
keywords:
- Bug Check 0x20 KERNEL_APC_PENDING_DURING_EXIT
- KERNEL_APC_PENDING_DURING_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_APC_PENDING_DURING_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea2b4ff9450cbbecc2fbb32b86df6d3354155673
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350362"
---
# <a name="bug-check-0x20-kernelapcpendingduringexit"></a>Bug 检查 0x20：内核\_APC\_PENDING\_在\_退出


内核\_APC\_PENDING\_在\_退出 bug 检查的值为 0x00000020。 这表明异步过程调用 (APC) 仍是挂起的线程在退出时。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="kernelapcpendingduringexit-parameters"></a>内核\_APC\_PENDING\_在\_退出参数


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
<td align="left"><p>在退出过程发现的挂起的 APC 的地址</p></td>
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

密钥的数据项是 APC 禁用线程计数 (参数 2)。 如果计数为非零值，它将指明问题的原因。

APC 禁用计数将减少每次将驱动程序调用**KeEnterCriticalRegion**， **FsRtlEnterFileSystem**，或获取互斥锁。

APC 禁用计数每的次递增一个驱动程序调用**KeLeaveCriticalRegion**， **KeReleaseMutex**，或**FsRtlExitFileSystem**。

由于这些调用应该总是以对，APC 禁用计数应在线程退出时为零。 负值指示的驱动程序具有未重新启用这些情况下禁用 APC 的调用。 正值指示反向为 true。

如果您遇到此错误，是很值得怀疑计算机--尤其是异常或非标准的驱动程序上安装的所有驱动程序。

此当前 IRQL (参数 3) 应为零。 如果不是这样，驱动程序的取消例程可能通过在提升的 IRQL 返回导致此 bug 检查。 在这种情况下，仔细注意在发生崩溃，次时运行 （和内容已关闭），并在发生崩溃时注意所有已安装的驱动程序。 在这种情况下的原因通常是驱动程序中的严重 bug。


## <a name="resolution"></a>分辨率
[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。
 

 




