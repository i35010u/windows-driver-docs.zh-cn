---
title: Bug 检查 0x50 PAGE_FAULT_IN_NONPAGED_AREA
description: PAGE_FAULT_IN_NONPAGED_AREA bug 检查具有 0x00000050 值。 这表示已引用无效的系统内存。
ms.assetid: 63b4ab82-f7a9-4e14-bf7c-707a22d7e251
keywords:
- Bug 检查 0x50 PAGE_FAULT_IN_NONPAGED_AREA
- PAGE_FAULT_IN_NONPAGED_AREA
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_NONPAGED_AREA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45de2f9ce0be5e46ca1d4011be2095233b8c8b9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575488"
---
# <a name="bug-check-0x50-pagefaultinnonpagedarea"></a>Bug 检查 0x50：页\_容错\_IN\_未分页\_区域


页面\_容错\_IN\_未分页\_区域 bug 检查的值为 0x00000050。 这表示已引用无效的系统内存。 通常的内存地址是错误或内存地址指向已释放内存。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="pagefaultinnonpagedarea-parameters"></a>页\_容错\_IN\_未分页\_区域参数


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
<td align="left"><p>引用的内存地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>读取操作</p>
<p><strong>1:</strong>写入操作</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>（如果已知） 引用内存的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

之后安装的硬件故障或发生故障情况下安装的硬件可能出现 bug 检查 0x50 （通常与有缺陷的 RAM，是其主内存、 RAM L2 缓存或视频 RAM）。

另一个可能原因是发生故障的系统服务或有故障的驱动程序代码的安装。

防病毒软件也会触发此错误，如可能已损坏的 NTFS 卷。

<a name="resolution"></a>分辨率
----------

**收集的信息**

如果在蓝色屏幕上的已列出，请检查驱动程序的名称。

检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

**Windows 内存诊断**

运行 Windows 内存诊断工具，用于测试的内存。 单击开始按钮，然后单击控制面板。 在搜索框中，键入内存，然后依次**诊断您的计算机的内存问题**。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

**解决硬件故障问题：** 如果硬件具有最近添加到系统，则删除它才能看到如果错误重复出现。 如果现有硬件出现故障，删除或更换有故障的组件。 应运行硬件诊断系统制造商提供。 有关这些过程的详细信息，请参阅您的计算机的所有者的手册。

**解决错误系统服务问题：** 禁用服务，并确认这会解决该错误。 如果是这样，请与系统服务有关的可能更新的制造商联系。 如果在系统启动期间发生错误，请调查 Windows 修复选项。 有关详细信息，请参阅[Windows 10 中的恢复选项](https://windows.microsoft.com/windows-10/windows-10-recovery-options)。

**在解决有关防病毒软件问题：** 禁用计划，并确认这会解决该错误。 如果是这样，请与联系有关可能的更新程序的制造商。

**在解决有关损坏的 NTFS 卷问题：** 运行**Chkdsk /f /r**以检测和修复磁盘错误。 系统分区上的磁盘扫描开始之前，必须重新启动系统。 请联系硬驱动程序系统查找任何诊断工具，它们为硬盘驱动器子系统提供的生产。

有关常规的蓝色屏幕上，故障排除信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

<a name="remarks"></a>备注
-------

通常情况下，此地址已释放的内存中，或只需无效。

这不会受到**试用-除**处理程序-通过探测来仅进行保护。

 

 




