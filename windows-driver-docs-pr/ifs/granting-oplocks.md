---
title: 授予 Oplock
description: 授予 Oplock
ms.assetid: 7faf17ef-1596-4952-9575-616f66b37ed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2886050fe69afa1d9b986e6bb8b6050ea7628d0e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841224"
---
# <a name="granting-oplocks"></a>授予 Oplock


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


通过[FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)请求 oplock。 以下列表显示了不同 oplock 类型的 FSCTLs （用户模式应用程序和内核模式驱动程序可以颁发）：

-   FSCTL\_请求\_OPLOCK\_级别\_1

-   FSCTL\_请求\_OPLOCK\_级别\_2

-   FSCTL\_请求\_批\_OPLOCK

-   FSCTL\_REQUEST\_FILTER\_OPLOCK

-   FSCTL\_请求\_OPLOCK

列表中的前四个 FSCTLs 用于请求旧版 oplock。 最后一个 FSCTL 用于请求 Windows 7 oplock 请求\_OPLOCK\_输入\_标志在请求的**Flags**成员中指定\_请求标志\_oplock\_，作为[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)的*lpInBuffer*参数进行传递。 同样，可以使用[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)从内核模式请求 Windows 7 oplock。 文件系统微筛选器必须使用[**FltAllocateCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecallbackdata)和[**FltPerformAsynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltperformasynchronousio)来请求 Windows 7 oplock。 若要指定所需的四个 Windows 7 oplock 中的一个，\_缓存中的一个或多个标志 OPLOCK\_级别缓存\_读取、OPLOCK\_级别\_缓存\_句柄或 OPLOCK\_\_缓存\_写入是在请求的**RequestedOplockLevel**成员中设置的，\_OPLOCK\_输入\_缓冲结构。 有关详细信息，请参阅[**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)。

当向 oplock 发出请求，并且可授予 oplock 时，文件系统将返回状态\_"挂起" （因此，绝不会为同步 i/o 授予 oplock）。 在 oplock 中断之前，FSCTL IRP 不会完成。 如果无法授予 oplock，则返回相应的错误代码。 最常返回的错误代码是状态\_OPLOCK\_未\_授予，状态\_无效\_参数（及其等效的用户模式模拟）。

如前所述，当其他应用程序/客户端尝试访问同一流时，筛选器 oplock 允许应用程序 "后退"。 此机制允许应用程序访问流，而不会导致流的其他访问器在尝试打开流时收到共享冲突。 若要避免共享冲突，应使用一个特殊的三步骤过程请求筛选器 oplock （FSCTL\_REQUEST\_FILTER\_OPLOCK）：

1.  使用所需的文件访问权限打开文件\_读取\_属性以及文件\_共享\_读取的共享模式 |文件\_共享\_写入 |\_删除文件\_共享。

2.  在步骤1中的句柄上请求筛选器 oplock。

3.  再次打开该文件以进行读访问。

在步骤1中打开的句柄不会导致其他应用程序收到共享冲突，因为它仅用于属性访问（文件\_读取\_属性），而不是数据访问（文件\_读取\_数据）。 此句柄适用于请求筛选器 oplock，但不适用于对数据流执行实际 i/o。 步骤3中打开的句柄允许操作者的持有者在流上执行 i/o，而在步骤2中授予的 oplock 允许操作者在不导致与尝试访问流的另一应用程序发生共享冲突的情况下，使 oplock 成为 "跳出"。

NTFS 文件系统通过文件\_保留\_OPFILTER 创建选项标志为此过程提供优化。 如果在上一过程的步骤1中指定了此标志，则该标志允许文件系统在文件系统可以确定步骤2将失败的情况下，将具有状态\_OPLOCK\_\_的创建请求失败。 请注意，如果步骤1成功，则无法保证步骤2将会成功，即使为创建请求指定了文件\_保留\_OPFILTER。

下表列出了授予 oplock 所需的条件。

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
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED （不会为同步 i/o 请求授予 oplock）。</li>
</ul></li>
<li>文件的任何流上都没有<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-kernel-transaction-manager" data-raw-source="[TxF](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-kernel-transaction-manager)">TxF</a>事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>流上没有其他打开的（即使是由同一线程进行）。
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
<li>如果目录，则返回 STATUS_INVALID_PARAMETER。</li>
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
<li>级别2和/或读取：已授予请求。 可以同时在同一个流上授予多个级别 2/读取 oplock。 多个级别2（但不是读取） oplock 甚至可以存在于同一个句柄。
<ul>
<li>如果对已向其授予读取 oplock 的句柄请求读取 oplock，则第一个读取 oplock 的 IRP 将在第二个读取 oplock 被授予之前通过 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成。</li>
</ul></li>
<li><p>级别1、批处理、筛选器、读取句柄、读写、读写句柄： STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>已阅读</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录，则返回 STATUS_INVALID_PARAMETER。</li>
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
<li>读取句柄和现有 oplock 具有与新请求不同的 oplock 密钥：已授予请求。 多个读取和读取句柄 oplock 可以共存于同一个流上（请参阅此表后面的说明）。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
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
<li>如果目录，则返回 STATUS_INVALID_PARAMETER。</li>
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
<li><p>级别2，级别1，批处理，筛选器，读写，读写-处理：返回 STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>读写</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>文件上没有 TxF 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>如果流上有其他打开（即使是由同一线程打开），它们必须具有相同的 oplock 键。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li>读取或读/写，并且现有 oplock 与请求具有相同的 oplock 密钥：现有 oplock 的 IRP 是通过 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成的，但会授予请求。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>级别2、级别1、批处理、筛选器、读取句柄、读写句柄： STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>读写-句柄</p></td>
<td align="left"><p>仅当满足以下所有条件时才授予：</p>
<ul>
<li>请求适用于给定的文件流。
<ul>
<li>如果目录，则返回 STATUS_INVALID_PARAMETER。</li>
</ul></li>
<li>打开流以进行异步访问。
<ul>
<li>如果为同步访问打开，则返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>文件上没有 TxF 事务。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li>如果在流上有其他打开的请求（即使是通过同一线程），它们必须具有相同的 oplock 键。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
</ul>
<p>请注意，如果当前 oplock 状态为：</p>
<ul>
<li><p>无 Oplock：已授予请求。</p></li>
<li>读取、读取句柄、读写或读写句柄和现有 oplock 与请求具有相同的 oplock 密钥：现有 oplock 的 IRP 是通过 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE 完成的，但会授予请求。
<ul>
<li>否则，将返回 STATUS_OPLOCK_NOT_GRANTED。</li>
</ul></li>
<li><p>返回级别2、级别1、批处理、筛选器： STATUS_OPLOCK_NOT_GRANTED。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**请注意**   读取和级别 2 oplock 可能共存于同一个流上，读取和读取句柄 oplock 可能共存，但级别2和读取句柄 oplock 可能不共存。

 

 

 




