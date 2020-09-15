---
title: Windows 内核的已过时例程
description: Windows 内核的已过时例程
ms.assetid: 876f48be-1d8f-4c65-bc84-e35c31919c47
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b98784b9d42022d92fcda840414d7d3f94f8418
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106242"
---
# <a name="windows-kernel-obsolete-routines"></a>Windows 内核的已过时例程


为了支持现有的二进制文件，将导出以下过时例程：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>过时例程</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ExAcquireResourceExclusive</strong></td>
<td><p>改用 <a href="/previous-versions/ff544351(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](/previous-versions/ff544351(v=vs.85))"><strong>ExAcquireResourceExclusiveLite</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>ExAcquireResourceShared</strong></td>
<td><p>改用 <a href="/previous-versions/ff544363(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireResourceSharedLite&lt;/strong&gt;](/previous-versions/ff544363(v=vs.85))"><strong>ExAcquireResourceSharedLite</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>ExAllocateFromZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="even">
<td><strong>ExConvertExclusiveToShared</strong></td>
<td><p>改用 <a href="/previous-versions/ff544558(v=vs.85)" data-raw-source="[&lt;strong&gt;ExConvertExclusiveToSharedLite&lt;/strong&gt;](/previous-versions/ff544558(v=vs.85))"><strong>ExConvertExclusiveToSharedLite</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>ExDeleteResource</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite" data-raw-source="[&lt;strong&gt;ExDeleteResourceLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)"><strong>ExDeleteResourceLite</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>ExExtendZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="odd">
<td><strong>ExFreeToZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="even">
<td><strong>ExInitializeResource</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite" data-raw-source="[&lt;strong&gt;ExInitializeResourceLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)"><strong>ExInitializeResourceLite</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInitializeWorkItem</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)"><strong>IoAllocateWorkItem</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>ExInitializeZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedAllocateFromZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedDecrementLong</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement" data-raw-source="[&lt;strong&gt;InterlockedDecrement&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)"><strong>InterlockedDecrement</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedExchangeAddLargeInteger</strong></td>
<td><p>有关以原子方式添加 2 64 位数字的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=71056" data-raw-source="[InterlockedExchangeAdd64](https://go.microsoft.com/fwlink/p/?linkid=71056)">InterlockedExchangeAdd64</a>。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedExchangeUlong</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange" data-raw-source="[&lt;strong&gt;InterlockedExchange&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange)"><strong>InterlockedExchange</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedExtendZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedFreeToZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedIncrementLong</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement" data-raw-source="[&lt;strong&gt;InterlockedIncrement&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)"><strong>InterlockedIncrement</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsFullZone</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="odd">
<td><strong>ExIsObjectInFirstZoneSegment</strong></td>
<td><p>改为使用后备链表列表。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](/windows-hardware/drivers/ddi/index)">缓冲区管理</a>。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsResourceAcquired</strong></td>
<td><p>改用 <a href="/previous-versions/windows/hardware/drivers/ff545466(v=vs.85)" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredLite&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff545466(v=vs.85))"><strong>ExIsResourceAcquiredLite</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>ExIsResourceAcquiredExclusive</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsResourceAcquiredShared</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>ExReleaseResource</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)"><strong>ExReleaseResourceLite</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>ExReleaseResourceForThread</strong></td>
<td><p>改用 <a href="/previous-versions/ff545585(v=vs.85)" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](/previous-versions/ff545585(v=vs.85))"><strong>ExReleaseResourceForThreadLite</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>IoAllocateAdapterChannel</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel" data-raw-source="[&lt;strong&gt;AllocateAdapterChannel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)"><strong>AllocateAdapterChannel</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>IoAssignResources</strong></td>
<td><p>Pnp 管理器为 PnP 设备的驱动程序分配资源，PnP 管理器通过每个 <a href="/windows-hardware/drivers/kernel/irp-mn-start-device" data-raw-source="[&lt;strong&gt;IRP_MN_START_DEVICE&lt;/strong&gt;](./irp-mn-start-device.md)"><strong>IRP_MN_START_DEVICE</strong></a> 请求传递资源列表。 必须支持 PnP 管理器无法枚举的旧设备的驱动程序应改用 <a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice" data-raw-source="[&lt;strong&gt;IoReportDetectedDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)"><strong>IoReportDetectedDevice</strong></a> 和 <a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection" data-raw-source="[&lt;strong&gt;IoReportResourceForDetection&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection)"><strong>IoReportResourceForDetection</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>IoAttachDeviceByPointer</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>IoAttachDeviceToDeviceStack</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>IoFlushAdapterBuffers</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers" data-raw-source="[&lt;strong&gt;FlushAdapterBuffers&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)"><strong>FlushAdapterBuffers</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>IoFreeAdapterChannel</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel" data-raw-source="[&lt;strong&gt;FreeAdapterChannel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)"><strong>FreeAdapterChannel</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>IoFreeMapRegisters</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers" data-raw-source="[&lt;strong&gt;FreeMapRegisters&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)"><strong>FreeMapRegisters</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>IoMapTransfer</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer" data-raw-source="[&lt;strong&gt;MapTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)"><strong>MapTransfer</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>IoQueryDeviceDescription</strong></td>
<td><p>此例程检索有关给定总线、控制器或外设对象的硬件配置信息，或从 <strong>\Registry\Machine\Hardware\Description</strong> 树中这三种类型的任意组合。 需要硬件配置信息的驱动程序应改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty" data-raw-source="[&lt;strong&gt;IoGetDeviceProperty&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)"><strong>IoGetDeviceProperty</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>IoReportResourceUsage</strong></td>
<td><p>此例程在 <strong>\Registry\Machine\Hardware\ResourceMap</strong> 树中声明硬件资源（例如中断向量、设备内存范围或特定 DMA 控制器通道），以便随后加载的驱动程序无法尝试使用相同的资源。 如果新驱动程序必须支持非 PnP 可枚举的旧设备，则驱动程序应调用 <a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection" data-raw-source="[&lt;strong&gt;IoReportResourceForDetection&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection)"><strong>IoReportResourceForDetection</strong></a> 来声明设备的资源。</p></td>
</tr>
<tr class="even">
<td><strong>KeGetDcacheFillSize</strong></td>
<td><p>驱动程序应改为调用 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment" data-raw-source="[&lt;strong&gt;GetDmaAlignment&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment)"><strong>GetDmaAlignment</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>MmCreateMdl</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl" data-raw-source="[&lt;strong&gt;IoAllocateMdl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)"><strong>IoAllocateMdl</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>MmIsNonPagedSystemAddressValid</strong></td>
<td></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)  
[缓冲区管理](/windows-hardware/drivers/ddi/index)  
[**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85))  
[**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))  
[**ExConvertExclusiveToSharedLite**](/previous-versions/ff544558(v=vs.85))  
[**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)  
[**ExInitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)  
[**ExIsResourceAcquiredExclusiveLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)  
[**ExIsResourceAcquiredSharedLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)  
[**ExReleaseResourceForThreadLite**](/previous-versions/ff545585(v=vs.85))  
[**ExReleaseResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)  
[**InterlockedDecrement**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)  
[**InterlockedExchange**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange)  
[**InterlockedIncrement**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)  
[**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)  
[**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)  
[**FreeMapRegisters**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)  
[**GetDmaAlignment**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment)  
[InterlockedExchangeAdd64](https://go.microsoft.com/fwlink/p/?linkid=71056)  
[**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)  
[**IoAllocateWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)  
[**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)  
[**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)  
[**IoReportDetectedDevice**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)  
[**IoReportResourceForDetection**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection)  
[**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md)  
[**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)