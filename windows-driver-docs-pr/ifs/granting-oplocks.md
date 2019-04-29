---
title: 授予 Oplock
description: 授予 Oplock
ms.assetid: 7faf17ef-1596-4952-9575-616f66b37ed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e2f77d7b12be4d97f73dd0f93dccb23e001a59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370139"
---
# <a name="granting-oplocks"></a>授予 Oplock


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


通过请求时 Oplock [FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)s。 以下列表显示了不同的机会锁类型 （这可能发出用户模式应用程序和内核模式驱动程序） FSCTLs:

-   FSCTL\_REQUEST\_OPLOCK\_LEVEL\_1

-   FSCTL\_REQUEST\_OPLOCK\_LEVEL\_2

-   FSCTL\_请求\_批处理\_OPLOCK

-   FSCTL\_REQUEST\_FILTER\_OPLOCK

-   FSCTL\_REQUEST\_OPLOCK

在列表中的前四个 FSCTLs 用于请求旧 oplock。 最后一个 FSCTL 用于与请求中请求 Windows 7 oplock\_OPLOCK\_输入\_标志\_中指定的请求标志**标志**成员的请求\_OPLOCK\_输入\_作为传递的缓冲区结构*lpInBuffer*参数[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)。 以类似方式[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)可以用于从内核模式下请求 Windows 7 oplock。 文件系统微筛选器必须使用[ **FltAllocateCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff541703)并[ **FltPerformAsynchronousIo** ](https://msdn.microsoft.com/library/windows/hardware/ff543420)请求 Windows 7 oplock。 若要指定这四个 Windows 7 oplock 是所需，一个或多个标志 OPLOCK\_级别\_缓存\_读取、 OPLOCK\_级别\_缓存\_句柄或 OPLOCK\_级别\_缓存\_中设置写入**RequestedOplockLevel**请求的成员\_OPLOCK\_输入\_缓冲区结构。 有关详细信息，请参阅[ **FSCTL\_请求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)。

文件系统时为可以授予 oplock 和 oplock 发出请求，返回状态\_PENDING （因此，oplock 永远不会授予同步 i/o）。 FSCTL IRP 破坏 oplock 之前未完成。 如果不能授予 oplock，则返回相应的错误代码。 返回的最常见的错误代码是状态\_OPLOCK\_不\_GRANTED 和状态\_无效\_参数 （和其等效的用户模式下模拟）。

正如前面提到的筛选器机会锁允许"返回"其他应用程序/客户端尝试访问相同的流时应用程序。 此机制允许应用程序而不会导致流的其他访问器以接收共享冲突，尝试打开流时访问的流。 若要避免共享冲突，特殊的三步骤过程应该用于请求筛选器 oplock (FSCTL\_请求\_筛选器\_OPLOCK):

1.  打开文件的文件所需掌握\_读取\_属性和文件共享模式\_共享\_读取 |文件\_共享\_编写 |文件\_共享\_删除。

2.  步骤 1 中请求筛选器 oplock 句柄上。

3.  打开文件再次进行读取访问权限。

在步骤 1 中打开的句柄不会导致其他应用程序以接收共享冲突，因为它处于打开状态，仅属性访问权限 (文件\_读取\_属性)，并不是数据访问 (文件\_读取\_数据)。 此句柄适合有关请求筛选器 oplock，而不是在数据流上执行实际 I/O。 在步骤 3 中打开的句柄允许机会锁持有的者执行 I/O 流，而在步骤 2 中授予 oplock 则允许机会锁的持有者"地获取"而不会导致对尝试访问该流的其他应用程序共享冲突。

NTFS 文件系统为提供了优化此过程通过文件\_保留\_OPFILTER 创建选项标志。 如果在上一个过程的步骤 1 中指定此标志，它允许文件系统无法创建请求状态\_OPLOCK\_不\_授予如果文件系统可以确定该步骤 2 将失败。 请注意，如果步骤 1 成功，则步骤 2 不能保证将成功，即使文件\_保留\_OPFILTER 指定用于创建请求。

下表列出了需要授予 oplock 所需的条件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">请求类型</th>
<th align="left">条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>级别 1</p>
<p>Filter</p>
<p>Batch</p></td>
<td align="left"><p>如果所有以下条件都为 true，则授予仅：</p>
<ul>
<li>该请求是对于给定的流的文件。
<ul>
<li>如果一个目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流，则用于异步访问。
<ul>
<li>如果打开用于同步访问，则返回 STATUS_OPLOCK_NOT_GRANTED （oplock 未授予对于同步 I/O 请求）。</li>
</ul></li>
<li>有没有<a href="https://msdn.microsoft.com/library/windows/hardware/ff565748" data-raw-source="[TxF](https://msdn.microsoft.com/library/windows/hardware/ff565748)">TxF</a>上的文件的任何流的事务。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有其他打开的流 （甚至在同一线程） 上。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态是：</p>
<ul>
<li><p>没有机会锁：授予的请求。</p></li>
<li><p>级别 2:原始级别 2 请求断开与 FILE_OPLOCK_BROKEN_TO_NONE。 然后授予请求排他 oplock。</p></li>
<li><p>第 1 级批处理筛选器、 读取、 读取句柄、 读写或读写句柄：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>级别 2</p></td>
<td align="left"><p>如果所有以下条件都为 true，则授予仅：</p>
<ul>
<li>该请求是对于给定的流的文件。
<ul>
<li>如果一个目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流，则用于异步访问。
<ul>
<li>如果打开用于同步访问，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有对该文件 TxF 的事务。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有当前的字节范围锁定在流上。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
<li>请注意，在 Windows 7 之前的操作系统将验证是否字节范围锁曾经存在在流上自上次复位它已打开，并使请求失败，如果是这样。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态是：</p>
<ul>
<li><p>没有机会锁：授予的请求。</p></li>
<li>级别 2 和/或读取：授予的请求。 您可以有多个级别 2/读取 oplock 授予对同一个流在同一时间。 在相同的句柄，甚至可以存在多个级别 2 （但不是读取） oplock。
<ul>
<li>如果已向它授予读取 oplock 句柄上请求读取 oplock 时，完成第一个读取 oplock IRP 与之前的第二个读取 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 授予 oplock。</li>
</ul></li>
<li><p>级别 1，批处理，筛选器，读取句柄、 读取写入、 读写句柄：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>Read</p></td>
<td align="left"><p>如果所有以下条件都为 true，则授予仅：</p>
<ul>
<li>该请求是对于给定的流的文件。
<ul>
<li>如果一个目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流，则用于异步访问。
<ul>
<li>如果打开用于同步访问，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有对该文件 TxF 的事务。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有当前的字节范围锁定在流上。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态是：</p>
<ul>
<li><p>没有机会锁：授予的请求。</p></li>
<li>级别 2 和/或读取：授予的请求。 您可以有多个级别 2/读取 oplock 授予对同一个流在同一时间。
<ul>
<li>此外，如果现有 oplock 具有与新的请求相同的 oplock 密钥，其 IRP 是已完成，但 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE。</li>
</ul></li>
<li>读取句柄和现有 oplock 具有新的请求的不同 oplock 密钥：授予的请求。 在同一个流上可共存多个读取和读取句柄 oplock （请参阅此表后面的说明）。
<ul>
<li>其他 （oplock 键是相同） 返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>级别 1，批处理，筛选器，读写、 读写句柄：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>读取句柄</p></td>
<td align="left"><p>如果所有以下条件都为 true，则授予仅：</p>
<ul>
<li>该请求是对于给定的流的文件。
<ul>
<li>如果一个目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流，则用于异步访问。
<ul>
<li>如果打开用于同步访问，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有对该文件 TxF 的事务。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有当前的字节范围锁定在流上。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态是：</p>
<ul>
<li><p>没有机会锁： 授予的请求。</p></li>
<li>读取： 授予的请求。
<ul>
<li>如果现有读取 oplock 具有相同 oplock 密钥作为新的请求，其 IRP 已完成并且 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE。 这意味着 oplock 读取从升级到读取句柄。</li>
<li>任何现有的读取 oplock，但没有与新的请求相同的 oplock 密钥保持不变。</li>
</ul></li>
<li><p>级别 2、 级别 1，批处理，筛选器，读写、 读写句柄：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>读写</p></td>
<td align="left"><p>如果所有以下条件都为 true，则授予仅：</p>
<ul>
<li>该请求是对于给定的流的文件。
<ul>
<li>如果一个目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流，则用于异步访问。
<ul>
<li>如果打开用于同步访问，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有对该文件 TxF 的事务。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>如果有其他打开的流 （甚至在同一线程） 上它们必须具有相同的 oplock 键。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态是：</p>
<ul>
<li><p>没有机会锁： 授予的请求。</p></li>
<li>读取或读写和现有 oplock 具有与请求相同的 oplock 键： 现有 oplock IRP 已完成，但 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE，授予的请求。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>级别 2、 级别 1，批处理，筛选器，读取句柄、 读写句柄：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>读写句柄</p></td>
<td align="left"><p>如果以下所有都为 true，则授予仅：</p>
<ul>
<li>该请求是对于给定的流的文件。
<ul>
<li>如果一个目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流，则用于异步访问。
<ul>
<li>如果打开用于同步访问，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>没有对该文件 TxF 的事务。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>如果有其他打开请求在流上 （甚至通过相同的线程） 它们必须具有相同的 oplock 键。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态是：</p>
<ul>
<li><p>没有机会锁： 授予的请求。</p></li>
<li>读取读取句柄、 读写或读写句柄和现有 oplock 具有与请求相同的 oplock 键： 现有 oplock IRP 已完成，但 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE，授予的请求。
<ul>
<li>返回其他 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>级别 2、 级别 1，批处理，筛选器：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**请注意**  读取和第 2 级 oplock 可能共存对同一个流，并读取和读句柄 oplock 可能共存，但级别 2 和读取句柄 oplock 可能不能共存。

 

 

 




