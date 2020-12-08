---
title: 分配用法跟踪
description: 删除分配列表后，视频内存管理器不再能够查看特定命令缓冲区中所引用的分配。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64ecde66e3994196137d724ca62971dd8b14c64a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810511"
---
# <a name="allocation-usage-tracking"></a>分配用法跟踪


删除分配列表后，视频内存管理器不再能够查看特定命令缓冲区中所引用的分配。 因此，视频内存管理器不再位于跟踪分配使用情况和处理相关同步的位置。 此责任现在会落在用户模式驱动程序中。 特别是，用户模式驱动程序必须处理与对分配的直接 CPU 访问以及重命名相关的同步。

对于分配销毁，视频内存管理器将以一种安全的方式对其进行异步延迟，这是调用线程的非阻塞和非常高性能。 由于此类用户模式驱动程序不必担心需要延迟分配销毁。 接收到分配析构请求时，默认情况下，视频内存管理器会假定在析构请求之前排入队列的命令可能会访问被销毁的分配并延迟销毁操作，直到队列中的命令完成。 如果用户模式驱动程序知道挂起的命令不能访问正在销毁的分配，则它可以指示视频内存管理器处理请求，而无需在调用 [*Deallocate2*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocate2cb)或 [**DestroyAllocation2**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtdestroyallocation2)时设置 **AssumeNotInUse** 标志来处理请求。

## <a name="span-idlock2spanspan-idlock2spanspan-idlock2spanlock2"></a><span id="Lock2"></span><span id="lock2"></span><span id="LOCK2"></span>Lock2


用户模式驱动程序将负责处理与直接 CPU 访问有关的适当同步。 具体而言，需要使用用户模式驱动程序来支持以下各项：

1.  支持非覆盖和丢弃锁语义。 这意味着用户模式驱动程序必须实现自己的重命名方案。
2.  对于需要同步的映射操作 (即不是上述非覆盖或放弃) ，用户模式驱动程序将需要：

    -   如果尝试访问当前正忙的分配，并且调用方已请求 **锁定** 操作不会阻止调用线程 (**D3D11 \_ 映射 \_ 标志不 \_ \_ \_ 等待**) ，则返回 **WasStillDrawing** 。
    -   或者，如果未 **设置 \_ D3D11 \_ 地图 \_ 标志 \_ not \_ wait** 标记，请等待分配可用于 CPU 访问。 需要使用用户模式驱动程序来实现非轮询等待。 用户模式驱动程序将使用新的上下文监视机制。

目前，用户模式驱动程序将继续需要调用 [*LockCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb) / [*UnlockCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockcb) ，以请求视频内存管理器设置 CPU 访问的分配。 在大多数情况下，用户模式驱动程序将能够使分配在整个生存期内进行映射。 然而，在将来， *LockCb* 和 *UnlockCb* 将被弃用，以支持新的 [*Lock2Cb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb) 和 [*Unlock2Cb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock2cb) 调用。 这些新回调的目标是使用一组新的参数和标志提供全新的全新实现。

Swizzling 范围从 Windows 显示器驱动程序模型 (WDDM) v2 中删除，而驱动程序开发人员负责从对 [*LockCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb) 的调用移到基于 [*Lock2Cb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb)的实现时，删除对 Swizzling 范围的依赖关系。

[*Lock2Cb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb) 作为一种简单方法公开，用于获取分配的虚拟地址。 根据分配的类型以及当前驻留在其中的当前段，有一些限制。

以下内容适用于 *CPUVisible* 分配：

-   缓存的 *CPUVisible* 分配必须驻留在一个口径段内，或者不是常驻，因此无法锁定。 我们无法保证在图形处理单元上的 CPU 和内存段之间进行缓存的一致性)  (GPU。
-   位于完全 *CPUVisible* 内存段中的 *CPUVisible* 分配 (使用可调整大小的条大小调整，) 确保可锁定并且能够返回虚拟地址。 此方案不需要任何特殊约束。
-   *CPUVisible* 在！由于各种原因， *CPUVisible* 内存段 (有或不能访问 *CPUHostAperture*) 可能无法映射到 CPU 虚拟地址。 如果 *CPUHostAperture* 的可用空间不足，或者分配未指定口径段，则无法获取虚拟地址。 出于此原因，我们需要在 *CPUVisible* ！*CPUVisible* 内存段必须在其受支持的段集内包含一个口径段，以确保能够在系统内存中放置分配并提供虚拟地址。
-   *CPUVisible* 分配已位于系统内存中 (和/或映射到一个口径段) 确保工作正常。

以下内容适用于！*CPUVisible* 分配：

-   *CPUVisible* 分配由无法直接指向 gpu 帧缓冲区的节对象进行支持。 为了锁定！*CPUVisible* 分配，我们要求分配支持支持段集中的口径段，或已在系统内存中 (不得驻留在设备) 上。

如果在分配不在设备上的情况下成功锁定分配，但不支持口径段，则必须确保在锁的持续时间内不会将分配提交到内存段。

**Lock2** 当前不包含任何标志，并且 **保留** 标志位必须全部为0。

## <a name="span-idcpuhostaperturespanspan-idcpuhostaperturespanspan-idcpuhostaperturespancpuhostaperture"></a><span id="CPUHostAperture"></span><span id="cpuhostaperture"></span><span id="CPUHOSTAPERTURE"></span>CPUHostAperture


为了更好地支持锁定，请！调整条大小时， *CPUVisible* 内存段失败，PCI 口径中提供了 *CPUHostAperture* 。 *CPUHostAperture* 的行为类似于基于页面的管理器，然后可以通过 [*DxgkDdiMapCpuHostAperture*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)设备驱动程序接口 (DDI) 函数，将该管理器直接映射到视频内存区域。 这样，我们就可以将一定范围的虚拟地址空间直接映射到 *CPUHostAperture* 的非连续范围，然后将 *CPUHostAperture* 映射到视频内存，而无需使用 swizzling 范围。

中的 CPU 可引用的最大可锁定内存量！*CPUVisible* 内存段限制为 *CPUHostAperture* 的大小。 可在 [CPU 主机口径](cpu-host-aperature.md)主题中找到向 Microsoft DirectX 图形内核公开 *CPUHostAperture* 的详细信息。

## <a name="span-idi_o_coherencyspanspan-idi_o_coherencyspanspan-idi_o_coherencyspanio-coherency"></a><span id="I_O_coherency"></span><span id="i_o_coherency"></span><span id="I_O_COHERENCY"></span>I/o 一致性


目前，在 x86/x64 上，我们要求所有 Gpu 都支持基于 PCIe 的 i/o 一致性，以允许 GPU 读取或写入可缓存的系统内存面并维护与 CPU 的一致性。 当图面从 GPU 的角度映射为缓存相关时，GPU 需要在访问图面时，snoop CPU 缓存。 这种形式的一致性通常用于 CPU 预计要从中进行读取的资源，例如某些过渡面。

在某些 ARM 平台上，硬件不直接支持 i/o 一致性。 在这些平台上，i/o 一致性需要通过手动使 CPU 缓存层次结构失效来进行模拟。 现在，视频内存管理器通过跟踪从 GPU (分配列表读取/写入操作) 以及 CPU (映射操作的分配来实现此操作。读/写) 并发出缓存失效，在确定缓存时，可能会包含需要写回的数据 (CPU 写入、GPU 读取) 或包含需要在 (GPU 写入时失效的陈旧数据) 的 CPU 读取。

在无 i/o 一致性的平台上，跟踪对分配的 CPU 和 GPU 访问权限的责任将降到用户模式驱动程序中。 Graphics 内核公开了新的 *无效缓存* DDI，用户模式驱动程序可以使用它来写回，并使与可缓存分配关联的虚拟地址范围无效。 在不支持 i/o 一致性的平台上，用户模式驱动程序将需要在 CPU 写入后、在读取 GPU 之前以及 CPU 读取之前和读取后调用此函数。 后一种情况可能会 unintuitive，但由于 CPU 可能在 GPU 写入数据之前将数据读取到内存中，因此必须使所有 CPU 缓存失效，以确保 CPU 从 RAM 重新读取数据。

 

