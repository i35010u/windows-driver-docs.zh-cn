---
title: 已检验版本 ASSERT
description: 已检验版本 ASSERT
ms.assetid: f002950d-6af9-42bb-9a1f-186873b09919
keywords:
- 检查内部版本号 WDK，assert 语句
- 断言检查 WDK 版本
- 错误 WDK 检查生成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6834664e7ac21b81a19ccad8b7f6d3ded02b331
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348942"
---
# <a name="checked-build-asserts"></a>已检验版本 ASSERT


## <span id="ddk_checked_build_asserts_tools"></span><span id="DDK_CHECKED_BUILD_ASSERTS_TOOLS"></span>


本主题包含一系列常见[ **ASSERT**](https://msdn.microsoft.com/library/windows/hardware/ff542107)s 遇到的驱动程序编写人员。

有关如何对这些断言的句柄 （以及其他未列出），一些提示，请参阅[已检验的版本如何指示问题](how-the-checked-build-indicates-a-problem.md)。

"调用例程"列中列出的例程是驱动程序编写人员或系统组件将调用以引发此错误的最常见例程。 下面列出的例程的一些是有案可稽的驱动程序调用的例程。 其他人是内部仅系统组件可以调用的例程。 记住，从您的驱动程序调用一些其他函数可能会导致所调用的函数在内部调用其中一个列出的函数，可以在打开问题**ASSERT**。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">调用的例程</th>
<th align="left">ASSERT 文本</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548263" data-raw-source="[&lt;strong&gt;IoAllocateMdl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548263)"><strong>IoAllocateMdl</strong></a></p></td>
<td align="left"><p>ASSERT(Length)</p></td>
<td align="left"><p>用户缓冲区所描述的长度为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548300" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548300)"><strong>IoAttachDeviceToDeviceStack</strong></a></p></td>
<td align="left"><p>ASSERT( sourceExtension-&gt;AttachedTo == <strong>NULL</strong> )</p></td>
<td align="left"><p>设备对象，该对象被附加 （源设备） 已附加到另一个设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>IoCallDriver</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP 参数不指向 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548338" data-raw-source="[&lt;strong&gt;IoCancelIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548338)"><strong>IoCancelIrp</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP 参数不指向 IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"><strong>IoCompleteRequest</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP 参数不指向 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( !Irp-&gt;CancelRoutine )</p></td>
<td align="left"><p>没有在取消例程 IRP 中存在。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;IoStatus.Status != STATUS_PENDING )</p></td>
<td align="left"><p>尝试完成与 STATUS_PENDING IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;IoStatus.Status != 0xffffffff )</p></td>
<td align="left"><p>尝试完成 IRP 具有无效的状态代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Tail.Overlay.AuxiliaryBuffer != <strong>NULL</strong> )</p></td>
<td align="left"><p>IRP 已经完成 STATUS_REPARSE，IO_REPARSE_TAG_MOUNT_POINT，使用，并且辅助缓冲区<strong>NULL</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548397" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548397)"><strong>IoCreateDevice</strong></a></p></td>
<td align="left"><p>ASSERT((DriverObject-&gt;Flags &amp; DRVO_UNLOAD_INVOKED) == 0)</p></td>
<td align="left"><p>已创建一个设备对象，但创建它的驱动程序标记为要卸载。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549113" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549113)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP 不指向 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT(IsListEmpty(&amp;(Irp)-&gt;ThreadListEntry))</p></td>
<td align="left"><p>正在释放 IRP 仍位于线程的 IRP 列表，并因此仍在使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;CurrentLocation &gt;= Irp-&gt;StackCount )</p></td>
<td align="left"><p>IRP 被释放，但 I/O 完成尚未完成处理此 IRP 的所有驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549661" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549661)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p>ASSERT(Irp-&gt;CancelRoutine == <strong>NULL</strong>)</p></td>
<td align="left"><p>没有剩余的 IRP，会为请求重复使用的取消例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoReuseIrp</strong></p></td>
<td align="left"><p>ASSERT(IsListEmpty(&amp;Irp-&gt;ThreadListEntry))</p></td>
<td align="left"><p>重新使用 IRP 仍位于线程的 IRP 列表，并因此仍在使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549707" data-raw-source="[&lt;strong&gt;IoSetHardErrorOrVerifyDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549707)"><strong>IoSetHardErrorOrVerifyDevice</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Tail.Overlay.Thread != <strong>NULL</strong> )</p></td>
<td align="left"><p>IRP 不在任何线程的 IRP 列表中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopLoadDriver</strong></p></td>
<td align="left"><p>ASSERT(driverObject-&gt;MajorFunction[i] != <strong>NULL</strong>)</p></td>
<td align="left"><p>该驱动程序设置为调度入口点<strong>NULL</strong>在其<strong>DriverEntry</strong>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (irp-&gt;IoStatus.Status ！ = 0xffffffff)</p></td>
<td align="left"><p>IRP 已完成，但显然无效的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT(reparseBuffer-&gt;ReparseTag == IO_REPARSE_TAG_MOUNT_POINT)</p></td>
<td align="left"><p>IRP 已完成，状态 = = STATUS_REPARSE 和信息 = = IO_REPARSE_TAG_MOUNT_POINT，但 ReparseTag 不适用于 MOUNT_POINT。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT(reparseBuffer-&gt;ReparseDataLength &lt; MAXIMUM_REPARSE_DATA_BUFFER_SIZE)</p></td>
<td align="left"><p>IRP 已完成，状态 = = STATUS_REPARSE 和信息 = = IO_REPARSE_TAG_MOUNT_POINT，但返回标记的长度无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT(reparseBuffer-&gt;Reserved &lt; MAXIMUM_REPARSE_DATA_BUFFER_SIZE)</p></td>
<td align="left"><p>IRP 已完成，状态 = = STATUS_REPARSE 和信息 = = IO_REPARSE_TAG_MOUNT_POINT，但返回标记的长度无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopSynchronousServiceTail</strong></p></td>
<td align="left"><p>ASSERT( !Irp-&gt;PendingReturned )</p></td>
<td align="left"><p>IRP 标记为挂起，但调度例程以同步方式返回状态 ！ = STATUS_PENDING。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554664" data-raw-source="[&lt;strong&gt;MmProbeAndLockPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554664)"><strong>MmProbeAndLockPages</strong></a></p></td>
<td align="left"><p>断言 (MemoryDescriptorList-&gt;ByteCount ！ = 0)</p></td>
<td align="left"><p>传入的 MDL 中的字节数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (((ULONG)MemoryDescriptorList-&gt;ByteOffset &amp; ~(PAGE_SIZE - 1)) == 0)</p></td>
<td align="left"><p>MDL 中的第一页中的偏移量是&gt;= PAGE_SIZE; MDL 的格式不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>断言 (((ULONG_PTR) MemoryDescriptorList-&gt;StartVa &amp; (PAGE_SIZE-1)) = = 0)</p></td>
<td align="left"><p>在 MDL 起始 VA 不对齐; 页MDL 结构不正确。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>断言 ((MemoryDescriptorList-&gt;MdlFlags &amp; (MDL_PAGES_LOCKED |MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL |MDL_IO_SPACE)) = = 0)</p></td>
<td align="left"><p>MDL 不是此函数调用的正确状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (NumberOfPagesToLock != 0)</p></td>
<td align="left"><p>MDL 介绍一系列页面和零页锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>断言 (<strong>FALSE</strong>)</p></td>
<td align="left"><p>描述 MDL 缓冲区中的页面已被锁定到内存的次数过多。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556381" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556381)"><strong>MmUnlockPages</strong></a></p></td>
<td align="left"><p>断言 ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_PAGES_LOCKED) ！ = 0)</p></td>
<td align="left"><p>包含描述此 MDL 缓冲区的页未被锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>断言 ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_SOURCE_IS_NONPAGED_POOL) = = 0)</p></td>
<td align="left"><p>MDL 介绍从非分页缓冲池的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>断言 ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_PARTIAL) = = 0)</p></td>
<td align="left"><p>通过调用生成 MDL <strong>IoBuildPartialMdl</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>断言 (MemoryDescriptorList-&gt;ByteCount ！ = 0)</p></td>
<td align="left"><p>MDL 描述由零个字节长的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT (NumberOfPages != 0)</p></td>
<td align="left"><p>MDL 不包含任何页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT ((SPFN_NUMBER)Process-&gt;NumberOfLockedPages &gt;= 0)</p></td>
<td align="left"><p>MDL 与关联的进程没有锁定的任何页面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT (<em>Page &lt;= MmHighestPhysicalPage)</p></td>
<td align="left"><p>MDL 中的页帧指针不是有效的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554498" data-raw-source="[&lt;strong&gt;MmBuildMdlForNonPagedPool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554498)"><strong>MmBuildMdlForNonPagedPool</strong></a></p></td>
<td align="left"><p>断言 (MemoryDescriptorList-&gt;ByteCount ！ = 0)</p></td>
<td align="left"><p>描述 MDL 缓冲区是零个字节长。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>断言 ((MemoryDescriptorList-&gt;MdlFlags &amp; (MDL_PAGES_LOCKED |MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL)) = = 0)</p></td>
<td align="left"><p>MDL 不在此函数调用的正确状态</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>ASSERT (NumberOfPages != 0)</p></td>
<td align="left"><p>MDL 描述具有零个页的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554629" data-raw-source="[&lt;strong&gt;MmMapLockedPagesSpecifyCache&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554629)"><strong>MmMapLockedPagesSpecifyCache</strong></a></p></td>
<td align="left"><p>断言 (MemoryDescriptorList-&gt;ByteCount ！ = 0)</p></td>
<td align="left"><p>MDL 长度为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_MAPPED_TO_SYSTEM_VA) == 0)</p></td>
<td align="left"><p>描述此 MDL 缓冲区已映射到内核虚拟地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT ((MemoryDescriptorList-&gt;MdlFlags &amp; ( MDL_MAPPED_TO_SYSTEM_VA | MDL_SOURCE_IS_NONPAGED_POOL | MDL_PARTIAL_HAS_BEEN_MAPPED)) == 0)</p></td>
<td align="left"><p>MDL 不是此函数调用的正确状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>断言 ((MemoryDescriptorList-&gt;MdlFlags &amp; (MDL_PAGES_LOCKED |MDL_PARTIAL)) ！ = 0)</p></td>
<td align="left"><p>MDL 处于此操作的正确状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT (PointerPte-&gt;u.Hard.Valid == 0)</p></td>
<td align="left"><p>描述 MDL 缓冲区包含不是驻留在内存中的页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>断言 (Pfn2-&gt;u3.e2.ReferenceCount ！ = 0)</p></td>
<td align="left"><p>描述 MDL 缓冲区包含不在内存中锁定的页。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556391" data-raw-source="[&lt;strong&gt;MmUnmapLockedPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556391)"><strong>MmUnmapLockedPages</strong></a></p></td>
<td align="left"><p>断言 (MemoryDescriptorList-&gt;ByteCount ！ = 0)</p></td>
<td align="left"><p>MDL 描述由零个字节长的缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>断言 (MemoryDescriptorList-&gt;MdlFlags &amp; MDL_MAPPED_TO_SYSTEM_VA)</p></td>
<td align="left"><p>传递给此函数可指定的基址指示内核虚拟地址空间中的地址，但这不同意在 MDL 缓冲区说明指定的参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT (PointerPte-&gt;u.Hard.Valid == 1)</p></td>
<td align="left"><p>描述 MDL 缓冲区中的页不是驻留在内存中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>断言 (</em>页 MI_GET_PAGE_FRAME_FROM_PTE (PointerPte) = =)</p></td>
<td align="left"><p>MDL 中的页帧指针不是有效的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>断言 (Pfn3-&gt;u3.e2.ReferenceCount ！ = 0)</p></td>
<td align="left"><p>描述 MDL 缓冲区包含不在内存中锁定的页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554618" data-raw-source="[&lt;strong&gt;MmMapIoSpace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554618)"><strong>MmMapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT (PhysicalAddress.HighPart == 0)</p></td>
<td align="left"><p>这在不超过 4 gb 的物理内存的基于 x86 的系统上运行，但传递给此函数可指定 I/O 空间地址的高 32 位的参数为非零值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>传递给此函数可指定要映射的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT (PointerPte-&gt;u.Hard.Valid == 0)</p></td>
<td align="left"><p>地址范围内的页面不在 I/O 空间中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556387" data-raw-source="[&lt;strong&gt;MmUnmapIoSpace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556387)"><strong>MmUnmapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>传递给此函数可指定要取消映射的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554460" data-raw-source="[&lt;strong&gt;MmAllocateContiguousMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554460)"><strong>MmAllocateContiguousMemory</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>传递给此函数可指定要分配的字节数的参数为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MemorySpecifyCache</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>传递给此函数可指定要分配的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554479" data-raw-source="[&lt;strong&gt;MmAllocateNonCachedMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554479)"><strong>MmAllocateNonCachedMemory</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>传递给此函数可指定要分配的字节数的参数为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>传递给此函数可指定要释放的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT (PAGE_ALIGN (BaseAddress) == BaseAddress)</p></td>
<td align="left"><p>传递给此函数指定的基址不是有效的参数。</p></td>
</tr>
</tbody>
</table>

 

 

 





