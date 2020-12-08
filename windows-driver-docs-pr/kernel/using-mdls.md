---
title: 使用 MDL
description: 使用 MDL
keywords:
- 内存管理 WDK 内核，
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8672b6444bdc87e9d1e95a6a19268db24e06b868
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803775"
---
# <a name="using-mdls"></a>使用 MDL


跨越一系列连续虚拟内存地址的 i/o 缓冲区可以分布在多个物理页面上，这些页面可能是不连续的。 操作系统使用 (MDL) 的 *内存描述符列表* 描述虚拟内存缓冲区的物理页面布局。

MDL 包含一个 [**mdl**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl) 结构，后跟一个数据数组，该结构描述了 i/o 缓冲区所在的物理内存。 MDL 的大小根据 MDL 描述的 i/o 缓冲区的特征而变化。 系统例程可用于计算 MDL 所需的大小并分配和释放 MDL。

MDL 结构不透明。 你的驱动程序应仅直接访问此结构的 **下一个** 和 **MdlFlags** 成员。 有关使用这两个成员的代码示例，请参阅以下示例部分。

MDL 的其余成员是不透明的。 请勿直接访问 MDL 的不透明成员。 相反，请使用以下宏，操作系统提供该宏以对结构执行基本操作：

[**MmGetMdlVirtualAddress**](./mm-bad-pointer.md) 返回 MDL 描述的 i/o 缓冲区的虚拟内存地址。

[**MmGetMdlByteCount**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount) 返回 i/o 缓冲区的大小（以字节为单位）。

[**MmGetMdlByteOffset**](./mm-bad-pointer.md) 返回 i/o 缓冲区开始处的物理页内的偏移量。

您可以使用 [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl) 例程分配 MDL。 若要释放 MDL，请使用 [**IoFreeMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl) 例程。 或者，可以通过调用 [**MmInitializeMdl**](./mm-bad-pointer.md) 例程来分配非分页内存块，然后将此内存块的格式设置为 MDL。

**IoAllocateMdl** 和 **MmInitializeMdl** 都不会初始化紧跟 MDL 结构的数据数组。 对于驻留在驱动程序分配的非分页内存块中的 MDL，请使用 [**MmBuildMdlForNonPagedPool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) 来初始化此数组，以描述 i/o 缓冲区所在的物理内存。

对于可分页内存，虚拟内存和物理内存之间的对应关系是临时的，因此遵循 MDL 结构的数据数组仅在特定情况下有效。 调用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) ，将可分页内存锁定到位置，并为当前布局初始化此数据数组。 在调用方使用 [**MmUnlockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 例程之前，不会分页内存，此时数据数组的内容将不再有效。

[**MmGetSystemAddressForMdlSafe**](./mm-bad-pointer.md)例程将指定 MDL 描述的物理页面映射到系统地址空间中的虚拟地址（如果它们尚未映射到系统地址空间）。 此虚拟地址适用于可能需要查看页来执行 i/o 的驱动程序，因为原始虚拟地址可能是只能在其原始上下文中使用的用户地址，可以随时删除。

请注意，使用 [**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) 例程生成部分 MDL 时，调用方应使用 **MmGetMdlVirtualAddress** 而不是 **MmGetSystemAddressForMdlSafe** 例程来确定要传入的虚拟地址。 **IoBuildPartialMdl** 使用 **MmGetMdlVirtualAddress** 从源 mdl 返回的地址来确定目标 mdl 的偏移量。 如果地址不同 (例如，当第一个地址是用户地址) 时，传递 **MmGetSystemAddressForMdlSafe** 返回的地址可能会导致数据损坏或 bug 检查。

当驱动程序调用 **IoAllocateMdl** 时，它可以通过将一个指向 irp 的指针指定为 **IoAllocateMdl** 的 *IRP* 参数，从而将 irp 与新分配的 MDL 关联起来。 IRP 可以有一个或多个与之关联的 MDLs。 如果 IRP 具有与之关联的单个 MDL，则 IRP 的 **MdlAddress** 成员将指向该 mdl。 如果 IRP 具有多个与之关联的 MDLs，则 **MdlAddress** 指向与 IRP 关联的 MDLs 的链接列表中的第一个 MDL，称为 *MDL 链*。 MDLs 由其 **下一** 成员链接。 链中最后一个 MDL 的 **下一个** MDL 成员设置为 **NULL**。

如果当驱动程序调用 **IoAllocateMdl** 时，它为 *SecondaryBuffer* 参数指定 **FALSE** ，IRP 的 **MDLADDRESS** 成员设置为指向新的 MDL。 如果 *SecondaryBuffer* 为 **TRUE**，则例程将在 MDL 链的末尾插入新 MDL。

完成 IRP 后，系统将解除锁定并释放与 IRP 关联的所有 MDLs。 系统在将 i/o 完成例程排队之前解锁 MDLs，并在执行 i/o 完成例程后释放它们。

驱动程序可以通过使用每个 MDL 的 **下一个** 成员访问链中的下一个 mdl 来遍历 MDL 链。 驱动程序可以通过更新 **下一个** 成员，手动将 MDLs 插入到链中。

MDL 链通常用于管理与单个 i/o 请求关联的缓冲区数组。  (例如，网络驱动程序可以在网络操作中对每个 IP 数据包使用一个缓冲区。 ) 数组中的每个缓冲区在链中都有其自己的 MDL。 当驱动程序完成请求时，它会将缓冲区合并为一个大的缓冲区。 然后，系统会自动清除请求的所有分配的 MDLs。

[I/o 管理器](windows-kernel-mode-i-o-manager.md)是 i/o 请求的频繁源。 当 i/o 管理器完成 i/o 请求时，i/o 管理器将释放 IRP，并释放附加到 IRP 的任何 MDLs。 其中一些 MDLs 可能已由位于设备堆栈中的 i/o 管理器下的驱动程序附加到 IRP。 同样，如果你的驱动程序是 i/o 请求的源，则你的驱动程序必须清除 IRP 以及 i/o 请求完成后附加到 IRP 的任何 MDLs。

### <a name="example"></a>示例

下面的代码示例是一个驱动程序实现的函数，它从 IRP 中释放 MDL 链：

```cpp
VOID MyFreeMdl(PMDL Mdl)
{
    PMDL currentMdl, nextMdl;

    for (currentMdl = Mdl; currentMdl != NULL; currentMdl = nextMdl) 
    {
        nextMdl = currentMdl->Next;
        if (currentMdl->MdlFlags & MDL_PAGES_LOCKED) 
        {
            MmUnlockPages(currentMdl);
        }
        IoFreeMdl(currentMdl);
    }
} 
```

如果链中 MDL 所描述的物理页面被锁定，则该示例函数会调用 [**MmUnlockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 例程来解锁页面，然后再调用 [**IOFREEMDL**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl) 以释放 MDL。 但是，在调用 **IoFreeMdl** 之前，示例函数不需要显式取消对页面的映射。 相反， **IoFreeMdl** 会在页面释放 MDL 时自动 messagebox 取消。
