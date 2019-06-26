---
title: 使用 MDL
description: 使用 MDL
ms.assetid: 60652eb8-cfdb-4591-88ff-cf9dc4b9743d
keywords:
- 内存管理 WDK 内核，
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22e711691c8993c2ddbc3ee064865580331fc17f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381613"
---
# <a name="using-mdls"></a>使用 MDL


跨越一系列连续的虚拟内存地址的 I/O 缓冲区可以分布在多个物理页面上，这些页面可以是不连续。 操作系统使用*内存描述符列表*(MDL) 来描述虚拟内存缓冲区的物理页布局。

MDL 组成[ **MDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)后跟描述 I/O 的缓冲区所驻留的物理内存的数据数组的结构。 MDL 的大小而异 MDL 描述的 I/O 缓冲区的特征。 可用来计算所需的 MDL 大小来分配和释放 MDL 系统例程。

不完全不透明 MDL 结构。 您的驱动程序应直接访问仅**下一步**并**MdlFlags**此结构的成员。 使用这两个成员的代码示例，请参阅下面的示例部分。

不透明 MDL 的其他成员。 不直接访问不透明 MDL 的成员。 相反，使用操作系统提供了执行基本操作在结构上的以下宏：

[**MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)返回由 MDL 描述的 I/O 缓冲区的虚拟内存地址。

[**MmGetMdlByteCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount)返回的大小，以字节为单位的 I/O 缓冲区。

[**MmGetMdlByteOffset** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)返回在一个物理页的 I/O 缓冲区开头的偏移量。

你可以分配与 MDL [ **IoAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)例程。 若要释放 MDL，使用[ **IoFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)例程。 或者，可以分配的非分页内存块，然后通过调用格式该块的内存设置为 MDL [ **MmInitializeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)例程。

既不**IoAllocateMdl**也不**MmInitializeMdl**初始化紧随 MDL 结构的数据数组。 对于 MDL 驱动程序分配的非分页内存块中，使用[ **MmBuildMdlForNonPagedPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)用于初始化此数组来描述 I/O 的缓冲区所驻留的物理内存。

对于可分页内存，虚拟和物理内存之间的对应关系是临时的因此遵循 MDL 结构的数据数组是仅在某些情况下有效。 调用[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)到位锁定的可分页内存和用于初始化当前布局此数据数组。 内存将不会调出之前调用方将使用[ **MmUnlockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)例程，此时数据数组的内容将不再有效。

[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)例程会映射到系统地址空间中的虚拟地址指定 MDL 描述的物理页如果它们未已映射到系统地址空间。 此虚拟地址是有用的驱动程序，可能需要查看页执行 i/o 操作，因为原始虚拟地址可能是可以使用仅在其原始上下文中，可以在任何时候删除的用户地址。

请注意，当使用生成部分 MDL [ **IoBuildPartialMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)例程，则应使用调用方**MmGetMdlVirtualAddress**而不是**MmGetSystemAddressForMdlSafe**例程时确定要传入的虚拟地址。 **IoBuildPartialMdl**使用的地址， **MmGetMdlVirtualAddress**返回源 MDL 来确定目标 MDL 的偏移量。 如果地址不同 （例如，用户地址的第一个地址时），将地址传递**MmGetSystemAddressForMdlSafe**返回可能导致数据损坏或错误检查。

当驱动程序调用**IoAllocateMdl**，它可以使用新分配 MDL 来指定指向作为 IRP 的关联 IRP *Irp*参数**IoAllocateMdl**。 IRP 可以具有一个或多个 MDLs 与之关联。 IRP 是否有与之关联，IRP 的单个 MDL **MdlAddress**成员指向该 MDL。 如果 IRP 具有与其关联的多个 MDLs **MdlAddress**指向 MDLs IRP，称为与关联的链接列表中的第一个 MDL *MDL 链*。 由链接 MDLs 他们**下一步**成员。 **下一步**链中的最后一个 MDL 成员设置为**NULL**。

如果当驱动程序调用**IoAllocateMdl**，它指定**FALSE**有关*SecondaryBuffer*参数，IRP **MdlAddress**成员设置为指向新 MDL。 如果*SecondaryBuffer*是**TRUE**，该例程在 MDL 链的末尾插入新 MDL。

完成 IRP 后，系统将解锁并释放与 IRP 相关联的所有 MDLs。 系统解锁 MDLs 之前进行排队 I/O 完成例程和 I/O 完成例程执行后释放它们。

驱动程序可以通过遍历 MDL 链**下一步**的每个 MDL 访问链中的下一步 MDL 成员。 驱动程序可以手动插入 MDLs 链通过更新**下一步**成员。

MDL 链通常用于管理与单个 I/O 请求相关联的缓冲区的数组。 （例如，网络驱动程序可以使用一个缓冲区的每个 IP 数据包中的网络操作。）数组中的每个缓冲区链中具有其自己 MDL。 该驱动程序完成请求，它将缓冲区合并到单个大型缓冲区。 系统然后会自动清理请求的所有已分配 MDLs。

[I/O 管理器](windows-kernel-mode-i-o-manager.md)经常会导致的 I/O 请求。 I/O 管理器完成的 I/O 请求，I/O 管理器释放 IRP，并释放任何附加到 IRP 的 MDLs。 这些 MDLs 的一些可能已附加到 IRP 设备堆栈中的 I/O 管理器下的驱动程序。 同样，如果您的驱动程序是一个 I/O 请求的源，您的驱动程序必须清理 IRP 和 I/O 请求完成时附加到 IRP 任何 MDLs。

### <a name="example"></a>示例

下面的代码示例是释放从 IRP MDL 链的驱动程序实现的函数：

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

如果通过 MDL 链中所述的物理页处于锁定状态，该示例函数将调用[ **MmUnlockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)例程，以调用之前解除锁定页[ **IoFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)来释放 MDL。 但是，示例函数不需要显式调用之前取消映射页**IoFreeMdl**。 相反， **IoFreeMdl**时释放 MDL 自动取消映射页。

分配、 释放，并管理 MDLs 系统例程的摘要，请参阅[地址映射和 MDLs](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

 

 




