---
title: 已检验版本 ASSERT
description: 已检验版本 ASSERT
ms.assetid: f002950d-6af9-42bb-9a1f-186873b09919
keywords:
- 检查生成 WDK，断言
- 断言 WDK 检查生成
- 错误 WDK 检查版本
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: b60262b4fce41ce1af187d9338284a946722e9a9
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999074"
---
# <a name="checked-build-asserts"></a>已检验版本 ASSERT


## <span id="ddk_checked_build_asserts_tools"></span><span id="DDK_CHECKED_BUILD_ASSERTS_TOOLS"></span>


本主题包含驱动程序编写器遇到的常见[**断言**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))的列表。

有关如何处理这些断言（以及未列出的其他内容）的一些提示，请参阅[检查的生成如何指示问题](how-the-checked-build-indicates-a-problem.md)。

"例程" 列中列出的例程是驱动程序编写器或系统组件为引发此错误而要调用的最常见的例程。 下面列出的一些例程是驱动程序调用的记录例程。 其他是只有系统组件可以调用的内部例程。 请记住，从驱动程序调用其他某个函数可能会导致调用的函数在内部调用列出的函数之一，进而发出**断言**。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程调用</th>
<th align="left">断言文本</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl" data-raw-source="[&lt;strong&gt;IoAllocateMdl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)"><strong>IoAllocateMdl</strong></a></p></td>
<td align="left"><p>ASSERT （长度）</p></td>
<td align="left"><p>所描述的用户缓冲区的长度为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>IoAttachDeviceToDeviceStack</strong></a></p></td>
<td align="left"><p>ASSERT （sourceExtension-&gt;AttachedTo = = <strong>NULL</strong> ）</p></td>
<td align="left"><p>所连接的设备对象（源设备）已附加到另一个设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a></p></td>
<td align="left"><p>ASSERT （Irp&gt;类型 = = IO_TYPE_IRP）</p></td>
<td align="left"><p>PIRP 参数不指向 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp" data-raw-source="[&lt;strong&gt;IoCancelIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)"><strong>IoCancelIrp</strong></a></p></td>
<td align="left"><p>ASSERT （Irp&gt;类型 = = IO_TYPE_IRP）</p></td>
<td align="left"><p>PIRP 参数不指向 IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a></p></td>
<td align="left"><p>ASSERT （Irp&gt;类型 = = IO_TYPE_IRP）</p></td>
<td align="left"><p>PIRP 参数不指向 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （！Irp-&gt;CancelRoutine）</p></td>
<td align="left"><p>IRP 中存在一个取消例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （Irp-&gt;IoStatus！ = STATUS_PENDING）</p></td>
<td align="left"><p>尝试使用 STATUS_PENDING 完成 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （Irp-&gt;IoStatus！ = 0xffffffff）</p></td>
<td align="left"><p>尝试使用无效的状态代码完成 IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （Irp-&gt;Tail. AuxiliaryBuffer！ = <strong>NULL</strong> ）</p></td>
<td align="left"><p>IRP 正在使用 STATUS_REPARSE，IO_REPARSE_TAG_MOUNT_POINT 完成，辅助缓冲区为<strong>NULL</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a></p></td>
<td align="left"><p>ASSERT （（DriverObject&gt;& DRVO_UNLOAD_INVOKED） = = 0）</p></td>
<td align="left"><p>已创建设备对象，但创建它的驱动程序标记为要卸载。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>ASSERT （Irp&gt;类型 = = IO_TYPE_IRP）</p></td>
<td align="left"><p>PIRP 不指向 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT （& IsListEmpty （Irp）-&gt;ThreadListEntry））</p></td>
<td align="left"><p>正在释放的 IRP 仍在线程的 IRP 列表中，因此仍在使用中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT （Irp-&gt;CurrentLocation &gt;= irp-&gt;StackCount）</p></td>
<td align="left"><p>正在释放 IRP，但尚未完成处理此 IRP 的所有驱动程序的 i/o 完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p>ASSERT （Irp-&gt;CancelRoutine = = <strong>NULL</strong>）</p></td>
<td align="left"><p>IRP 中还有一个已请求重用的取消例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoReuseIrp</strong></p></td>
<td align="left"><p>ASSERT （IsListEmpty （&Irp-&gt;ThreadListEntry））</p></td>
<td align="left"><p>正在重用的 IRP 仍在线程的 IRP 列表中，因此仍在使用中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice" data-raw-source="[&lt;strong&gt;IoSetHardErrorOrVerifyDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice)"><strong>IoSetHardErrorOrVerifyDevice</strong></a></p></td>
<td align="left"><p>断言（Irp-&gt;Tail. Thread！ = <strong>NULL</strong> ）</p></td>
<td align="left"><p>IRP 不在任何线程的 IRP 列表上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopLoadDriver</strong></p></td>
<td align="left"><p>ASSERT （driverObject-&gt;MajorFunction [i]！ = <strong>NULL</strong>）</p></td>
<td align="left"><p>驱动程序将调度入口点设置为<strong>DriverEntry</strong>例程中的<strong>NULL</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （irp-&gt;IoStatus！ = 0xffffffff）</p></td>
<td align="left"><p>IRP 以明显无效的状态完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （reparseBuffer-&gt;ReparseTag = = IO_REPARSE_TAG_MOUNT_POINT）</p></td>
<td align="left"><p>已完成 IRP，状态为 = = STATUS_REPARSE，信息 = = IO_REPARSE_TAG_MOUNT_POINT，但 ReparseTag 不是 MOUNT_POINT 的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （reparseBuffer-&gt;ReparseDataLength &lt; MAXIMUM_REPARSE_DATA_BUFFER_SIZE）</p></td>
<td align="left"><p>已完成 IRP，状态为 = = STATUS_REPARSE，信息 = = IO_REPARSE_TAG_MOUNT_POINT，但返回的标记的长度无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT （reparseBuffer&gt; &lt; MAXIMUM_REPARSE_DATA_BUFFER_SIZE）</p></td>
<td align="left"><p>已完成 IRP，状态为 = = STATUS_REPARSE，信息 = = IO_REPARSE_TAG_MOUNT_POINT，但返回的标记的长度无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopSynchronousServiceTail</strong></p></td>
<td align="left"><p>ASSERT （！Irp-&gt;PendingReturned）</p></td>
<td align="left"><p>IRP 已标记为挂起，但以状态！ = STATUS_PENDING 同步调度返回的例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages" data-raw-source="[&lt;strong&gt;MmProbeAndLockPages&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)"><strong>MmProbeAndLockPages</strong></a></p></td>
<td align="left"><p>ASSERT （MemoryDescriptorList-&gt;ByteCount！ = 0）</p></td>
<td align="left"><p>传入的 MDL 中的字节计数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT （（（ULONG） MemoryDescriptorList-&gt;ByteOffset & ~ （PAGE_SIZE-1）） = = 0）</p></td>
<td align="left"><p>MDL 中第一页的偏移量为&gt;= PAGE_SIZE;MDL 的格式不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT （（（ULONG_PTR） MemoryDescriptorList-&gt;StartVa & （PAGE_SIZE-1）） = = 0）</p></td>
<td align="left"><p>MDL 中的起始 VA 不是页对齐的;MDL 的格式不正确。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & （MDL_PAGES_LOCKED |MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL |MDL_IO_SPACE）） = = 0）</p></td>
<td align="left"><p>此函数调用的 MDL 状态不正常。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT （NumberOfPagesToLock！ = 0）</p></td>
<td align="left"><p>MDL 介绍了一系列页面，其中包含零页要锁定的页面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT （<strong>FALSE</strong>）</p></td>
<td align="left"><p>MDL 描述的缓冲区中的页已被锁定到内存中，这种情况很长。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)"><strong>MmUnlockPages</strong></a></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & MDL_PAGES_LOCKED）！ = 0）</p></td>
<td align="left"><p>包含此 MDL 描述的缓冲区的页未被锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & MDL_SOURCE_IS_NONPAGED_POOL） = = 0）</p></td>
<td align="left"><p>MDL 描述非分页池的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & MDL_PARTIAL） = = 0）</p></td>
<td align="left"><p>MDL 是通过调用<strong>IoBuildPartialMdl</strong>生成的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT （MemoryDescriptorList-&gt;ByteCount！ = 0）</p></td>
<td align="left"><p>MDL 描述长度为零字节的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT （NumberOfPages！ = 0）</p></td>
<td align="left"><p>MDL 不包含任何页面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT （（SPFN_NUMBER）进程-&gt;NumberOfLockedPages &gt;= 0）</p></td>
<td align="left"><p>与 MDL 关联的进程未锁定任何页。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT （<em>Page &lt;= MmHighestPhysicalPage）</p></td>
<td align="left"><p>MDL 中的页面帧指针无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool" data-raw-source="[&lt;strong&gt;MmBuildMdlForNonPagedPool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)"><strong>MmBuildMdlForNonPagedPool</strong></a></p></td>
<td align="left"><p>ASSERT （MemoryDescriptorList-&gt;ByteCount！ = 0）</p></td>
<td align="left"><p>MDL 描述的缓冲区长度为零字节。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & （MDL_PAGES_LOCKED |MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL）） = = 0）</p></td>
<td align="left"><p>此函数调用的 MDL 状态不正常</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>ASSERT （NumberOfPages！ = 0）</p></td>
<td align="left"><p>MDL 描述了零页的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache" data-raw-source="[&lt;strong&gt;MmMapLockedPagesSpecifyCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)"><strong>MmMapLockedPagesSpecifyCache</strong></a></p></td>
<td align="left"><p>ASSERT （MemoryDescriptorList-&gt;ByteCount！ = 0）</p></td>
<td align="left"><p>MDL 长度为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & MDL_MAPPED_TO_SYSTEM_VA） = = 0）</p></td>
<td align="left"><p>此 MDL 描述的缓冲区已映射到内核虚拟地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & （MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL_HAS_BEEN_MAPPED）） = = 0）</p></td>
<td align="left"><p>此函数调用的 MDL 状态不正常。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT （（MemoryDescriptorList-&gt;MdlFlags & （MDL_PAGES_LOCKED |MDL_PARTIAL））！ = 0）</p></td>
<td align="left"><p>MDL 未处于此操作的正确状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT （PointerPte&gt;= = 0）</p></td>
<td align="left"><p>MDL 描述的缓冲区包含不在内存中的页面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT （Pfn2-&gt;ReferenceCount！ = 0）</p></td>
<td align="left"><p>MDL 描述的缓冲区包含内存中未锁定的页面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages" data-raw-source="[&lt;strong&gt;MmUnmapLockedPages&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages)"><strong>MmUnmapLockedPages</strong></a></p></td>
<td align="left"><p>ASSERT （MemoryDescriptorList-&gt;ByteCount！ = 0）</p></td>
<td align="left"><p>MDL 描述长度为零字节的缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT （MemoryDescriptorList-&gt;MdlFlags & MDL_MAPPED_TO_SYSTEM_VA）</p></td>
<td align="left"><p>传递给此函数以指定基址的参数指示核心虚拟地址空间中的一个地址，但这并不同意 MDL 中的缓冲区说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT （PointerPte&gt;= = 1）</p></td>
<td align="left"><p>MDL 描述的缓冲区中的页面不在内存中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT （</em>Page = = MI_GET_PAGE_FRAME_FROM_PTE （PointerPte））</p></td>
<td align="left"><p>MDL 中的页面帧指针无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT （Pfn3-&gt;ReferenceCount！ = 0）</p></td>
<td align="left"><p>MDL 描述的缓冲区包含内存中未锁定的页面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace" data-raw-source="[&lt;strong&gt;MmMapIoSpace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)"><strong>MmMapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT （PhysicalAddress. Largeint.highpart = = 0）</p></td>
<td align="left"><p>此功能运行在物理内存不超过 4 GB 的基于 x86 的系统上，但传递给此函数以指定 i/o 空间的高32位的参数为非零值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT （NumberOfBytes！ = 0）</p></td>
<td align="left"><p>传递给此函数以指定要映射的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT （PointerPte&gt;= = 0）</p></td>
<td align="left"><p>地址风行一时中的页面不在 i/o 空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace" data-raw-source="[&lt;strong&gt;MmUnmapIoSpace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)"><strong>MmUnmapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT （NumberOfBytes！ = 0）</p></td>
<td align="left"><p>传递给此函数以指定取消映射的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory" data-raw-source="[&lt;strong&gt;MmAllocateContiguousMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)"><strong>MmAllocateContiguousMemory</strong></a></p></td>
<td align="left"><p>ASSERT （NumberOfBytes！ = 0）</p></td>
<td align="left"><p>传递给此函数以指定要分配的字节数的参数为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MemorySpecifyCache</strong></p></td>
<td align="left"><p>ASSERT （NumberOfBytes！ = 0）</p></td>
<td align="left"><p>传递给此函数以指定要分配的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory" data-raw-source="[&lt;strong&gt;MmAllocateNonCachedMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)"><strong>MmAllocateNonCachedMemory</strong></a></p></td>
<td align="left"><p>ASSERT （NumberOfBytes！ = 0）</p></td>
<td align="left"><p>传递给此函数以指定要分配的字节数的参数为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT （NumberOfBytes！ = 0）</p></td>
<td align="left"><p>传递给此函数以指定要释放的字节数的参数为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT （PAGE_ALIGN （BaseAddress） = = BaseAddress）</p></td>
<td align="left"><p>传递给此函数以指定基址的参数无效。</p></td>
</tr>
</tbody>
</table>

 

 

 





