---
title: 授予 Oplock
description: 授予 Oplock
ms.assetid: 7faf17ef-1596-4952-9575-616f66b37ed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afe43266c7fcb41cc2ae1586d6e8ef1206b91079
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065950"
---
# <a name="granting-oplocks"></a>授予 Oplock


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


通过 [FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)请求 oplock。 以下列表显示了不同 oplock 类型的 FSCTLs， (哪些用户模式应用程序和内核模式驱动程序可以) ：

-   FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 1

-   FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 2

-   FSCTL \_ 请求 \_ 批处理 \_ OPLOCK

-   FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK

-   FSCTL \_ 请求 \_ OPLOCK

列表中的前四个 FSCTLs 用于请求旧版 oplock。 最后一个 FSCTL 用于向 Windows 7 oplock 请求请求 \_ oplock 输入 \_ \_ 标志 \_ 请求标志，该标志在请求 oplock 输入缓冲区结构的**Flags**成员中指定 \_ ，并 \_ \_ 作为[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)的*lpInBuffer*参数进行传递。 同样，可以使用 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 从内核模式请求 Windows 7 oplock。 文件系统微筛选器必须使用 [**FltAllocateCallbackData**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecallbackdata) 和 [**FltPerformAsynchronousIo**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltperformasynchronousio) 来请求 Windows 7 oplock。 若要指定需要四个 Windows 7 oplock 中的哪一个，请 \_ \_ \_ \_ \_ \_ \_ \_ \_ 在请求**RequestedOplockLevel** \_ OPLOCK \_ 输入缓冲区结构的 RequestedOplockLevel 成员中设置 \_ 一个或多个标志 OPLOCK 级别缓存读取、oplock 级别缓存句柄或 oplock 级别缓存写入。 有关详细信息，请参阅 [**FSCTL \_ 请求 \_ OPLOCK**](./fsctl-request-oplock.md)。

当对 oplock 进行请求并且可以授予 oplock 时，文件系统会返回状态 \_ "挂起 (，因此，永远不会为同步 i/o) 授予 oplock。 在 oplock 中断之前，FSCTL IRP 不会完成。 如果无法授予 oplock，则返回相应的错误代码。 最常返回的错误代码为状态 \_ OPLOCK \_ \_ ，但状态 \_ 无效 \_ 参数 (及其等效的用户模式模拟) 。

如前所述，当其他应用程序/客户端尝试访问同一流时，筛选器 oplock 允许应用程序 "后退"。 此机制允许应用程序访问流，而不会导致流的其他访问器在尝试打开流时收到共享冲突。 若要避免共享冲突，应使用一个特殊的三步骤过程请求筛选器 oplock (FSCTL \_ 请求 \_ 筛选器 \_ oplock) ：

1.  打开文件，其中包含所需的文件 \_ 读取 \_ 属性访问权限和文件共享读取的共享模式 \_ \_ |文件 \_ 共享 \_ 写入 |\_删除文件共享 \_ 。

2.  在步骤1中的句柄上请求筛选器 oplock。

3.  再次打开该文件以进行读访问。

在步骤1中打开的句柄不会导致其他应用程序收到共享冲突，因为它只是为属性访问打开 (文件 \_ 读取 \_ 特性) ，而不是 (文件 \_ 读取数据) 的数据访问 \_ 。 此句柄适用于请求筛选器 oplock，但不适用于对数据流执行实际 i/o。 步骤3中打开的句柄允许操作者的持有者在流上执行 i/o，而在步骤2中授予的 oplock 允许操作者在不导致与尝试访问流的另一应用程序发生共享冲突的情况下，使 oplock 成为 "跳出"。

NTFS 文件系统通过 "文件 \_ 保留 \_ OPFILTER create" 选项标志为此过程提供优化。 如果在上一过程的步骤1中指定了此标志，则 \_ \_ \_ 当文件系统可以确定步骤2将失败时，它允许文件系统使不会获得状态 OPLOCK 的 create 请求失败。 请注意，如果步骤1成功，则无法保证步骤2将会成功，即使 \_ \_ 为创建请求指定了文件保留 OPFILTER。

下表列出了授予 oplock 所需的条件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">请求类型</th>
<th align="left">Conditions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>级别 1</p>
<p>筛选器</p>
<p>Batch</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录 STATUS_INVALID_PARAMETER，则返回。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开了，则将返回 STATUS_OPLOCK_NOT_GRANTED， (不向) 的同步 i/o 请求授予 oplock。</li>
</ul></li>
<li>文件的任何流上都没有 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-kernel-transaction-manager" data-raw-source="[TxF](../kernel/windows-kernel-mode-kernel-transaction-manager.md)">TxF</a> 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>即使 () 的同一线程，也不会在流上打开其他打开。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li><p>级别2：原始第2级请求与 FILE_OPLOCK_BROKEN_TO_NONE 断开。 然后授予请求的排他 oplock。</p></li>
<li><p>级别1、批处理、筛选器、读取、读取句柄、读写或读写句柄：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>级别 2</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录 STATUS_INVALID_PARAMETER，则返回。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>文件上没有 TxF 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>流上没有当前的字节范围锁。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
<li>请注意，在 Windows 7 之前，操作系统会验证自上次打开后是否已在流上存在字节范围锁，如果是，则会导致请求失败。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li>级别2和/或读取：已授予请求。 可以同时在同一个流上授予多个级别 2/读取 oplock。 多个第2级 (但不读取) oplock 甚至可以存在于相同的句柄上。
<ul>
<li>如果对已向其授予读取 oplock 的句柄请求读取 oplock，则第一个读取 oplock 的 IRP 会在第二次读取 oplock 被授予之前以 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成。</li>
</ul></li>
<li><p>返回级别1，批处理，筛选器，读取句柄，读写，读写句柄： STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>读取</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录 STATUS_INVALID_PARAMETER，则返回。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>文件上没有 TxF 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>流上没有当前的字节范围锁。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li>级别2和/或读取：已授予请求。 可以同时在同一个流上授予多个级别 2/读取 oplock。
<ul>
<li>此外，如果现有 oplock 与新请求具有相同的 oplock 密钥，则其 IRP 将使用 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成。</li>
</ul></li>
<li>读取句柄和现有 oplock 具有与新请求不同的 oplock 密钥：已授予请求。 多个读取和读取句柄 oplock 可以共存于同一流 (请参阅此表后面的说明) 。
<ul>
<li>否则 (oplock 密钥) 返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>返回级别1，批处理，筛选器，读写，读写句柄： STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>读取句柄</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录 STATUS_INVALID_PARAMETER，则返回。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>文件上没有 TxF 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>流上没有当前的字节范围锁。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li>Read：已授予请求。
<ul>
<li>如果现有读取 oplock 与新请求具有相同的 oplock 密钥，则其 IRP 将使用 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成。 这意味着，oplock 将从读取升级到读取句柄。</li>
<li>与新请求不具有相同 oplock 密钥的任何现有读取 oplock 均保持不变。</li>
</ul></li>
<li><p>级别2，级别1，批处理，筛选器，读写，读写-处理： STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>读写</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录 STATUS_INVALID_PARAMETER，则返回。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>文件上没有 TxF 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>如果其他打开的流 (甚至是同一线程) 则它们必须具有相同的 oplock 键。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li>读取或读/写，并且现有 oplock 与请求具有相同的 oplock 密钥：现有 oplock 的 IRP 已通过 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成，并授予请求。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>级别2、级别1、批处理、筛选器、读取句柄、读写句柄：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>读写-句柄</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录 STATUS_INVALID_PARAMETER，则返回。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>文件上没有 TxF 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>如果在流上有其他打开的请求 (甚至是同一线程) 它们必须具有相同的 oplock 键。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li>读取、读取句柄、读写或读写句柄和现有 oplock 与请求具有相同的 oplock 密钥：现有 oplock 的 IRP 已通过 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成，并授予请求。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>返回级别2、级别1、批处理、筛选器： STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**注意**   读取和级别 2 oplock 可以共存于同一流上，读取和读取句柄 oplock 可能共存，但级别2和读取-句柄 oplock 可能不会共存。

 

 

