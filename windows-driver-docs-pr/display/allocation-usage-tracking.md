---
title: 分配用法跟踪
description: 分配列表中消失，使用的视频内存管理器不再具有到所引用的特定命令缓冲区中分配的可见性。
ms.assetid: F913C9A3-535F-4DA0-8895-7A05CBF4D4AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5a6e169b040825ac1d2ab84e086ef16c02054c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568809"
---
# <a name="allocation-usage-tracking"></a>分配用法跟踪


分配列表中消失，使用的视频内存管理器不再具有到所引用的特定命令缓冲区中分配的可见性。 因此，视频内存管理器将不再在位置来跟踪分配使用情况并处理相关的同步。 此职责现在将回退到用户模式驱动程序验证。 具体而言，用户模式驱动程序将需要处理同步相对于直接 CPU 访问权限分配以及重命名。

分配销毁的视频内存管理器将以异步方式将遵循这些将同时非阻止调用线程和性能非常高的安全方式。 这种情况下用户模式驱动程序无需担心有延迟分配析构。 视频内存管理器收到分配析构请求后，假定默认情况下，该命令排队的之前析构请求可能会潜在地访问正在销毁的分配和延迟直到已排队析构操作命令完成。 如果用户模式驱动程序知道挂起命令不访问正在销毁的分配，它可以通过设置指示视频内存管理器处理的请求而不等待**AssumeNotInUse**标记时调用[ *Deallocate2* ](https://msdn.microsoft.com/library/windows/hardware/dn906353)或[ **DestroyAllocation2**](https://msdn.microsoft.com/library/windows/hardware/dn906772)。

## <a name="span-idlock2spanspan-idlock2spanspan-idlock2spanlock2"></a><span id="Lock2"></span><span id="lock2"></span><span id="LOCK2"></span>Lock2


用户模式驱动程序将负责处理相对于 CPU 的直接访问正确的同步。 具体而言，用户模式驱动程序将需要支持以下功能：

1.  支持无覆盖并丢弃锁定语义。 这意味着用户模式驱动程序将需要实现自己的重命名方案。
2.  对于需要同步 （即不是上述 no-overwrite 或放弃） 的映射操作，用户模式驱动程序将需要：

    -   返回**WasStillDrawing**如果尝试访问分配，这是当前正忙，且调用方具有请求的**锁**操作不会阻止调用线程 (**D3D11\_地图\_标志\_做\_不\_等待**)。
    -   或者，如果**D3D11\_地图\_标志\_不要\_不\_等待**未设置标志，等待，直到分配变为可供 CPU 访问。 用户模式驱动程序将需要实现非轮询等待。 用户模式驱动程序将使用的监视机制的新上下文。

现在，用户模式驱动程序将继续需要调用[ *LockCb*](https://msdn.microsoft.com/library/windows/hardware/ff568914)/[*UnlockCb* ](https://msdn.microsoft.com/library/windows/hardware/ff569011)提出的视频内存若要设置的 CPU 访问分配的管理器。 在大多数情况下，用户模式驱动程序将无法保持其整个生存期内映射的分配。 但是，在将来， *LockCb*并*UnlockCb*将新的弃用[ *Lock2Cb* ](https://msdn.microsoft.com/library/windows/hardware/dn914483)和[ *Unlock2Cb* ](https://msdn.microsoft.com/library/windows/hardware/dn914484)调用。 这些新的回调的目标是提供一组全新干净的自变量和标志的新实现。

Swizzling 范围已从 Windows 显示器驱动程序模型 (WDDM) v2 和从调用中删除对 swizzling 范围的依赖关系，驱动程序开发人员负责[ *LockCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568914)作为它们进一步推动实现基于[ *Lock2Cb*](https://msdn.microsoft.com/library/windows/hardware/dn914483)。

[*Lock2Cb* ](https://msdn.microsoft.com/library/windows/hardware/dn914483)公开为获取分配的虚拟地址的简单方法。 有几个限制的分配，以及它是当前驻留在中的当前段的类型。

以下适用于*CPUVisible*分配：

-   缓存*CPUVisible*分配必须驻留在 aperture 段或不是常驻才能被锁定。 我们无法保证缓存 CPU 和图形处理单元 (GPU) 上的内存段之间的一致性。
-   *CPUVisible*分配位于完全*CPUVisible*保证 （调整大小时使用可调整大小的栏） 的内存段都是可锁定和无法返回虚拟地址。 在此方案中不需要任何特殊约束。
-   *CPUVisible*分配对位于 ！*CPUVisible*内存段 (具有或没有访问权限*CPUHostAperture*) 可能无法映射到 CPU 的虚拟地址出于各种原因。 如果*CPUHostAperture*不在可用空间或分配未指定 aperture 段，是不可能获取的虚拟地址。 出于此原因，我们需要的所有*CPUVisible*中的分配 ！*CPUVisible*段必须包含在其受支持的段集，以确保我们能够将放置在系统内存分配，并提供一个虚拟地址中的小孔段的内存。
-   *CPUVisible*分配已位于系统内存 （和/或映射到 aperture 段） 可保证。

以下适用于 ！*CPUVisible*分配：

-   *CPUVisible*分配受部分对象不能直接指向 Gpu 帧缓冲区。 若要锁定 ！*CPUVisible*分配，我们要求分配支持的受支持的段中的小孔段设置，或者已在系统内存 （不能驻留在设备上）。

如果在分配不是驻留在设备上，但不支持 aperture 段分配成功锁定，必须保证分配不被提交到一个内存段期间的锁的持续时间。

**Lock2**当前包含任何标志，并**保留**标志位必须为 0。

## <a name="span-idcpuhostaperturespanspan-idcpuhostaperturespanspan-idcpuhostaperturespancpuhostaperture"></a><span id="CPUHostAperture"></span><span id="cpuhostaperture"></span><span id="CPUHOSTAPERTURE"></span>CPUHostAperture


若要更好地支持使用锁定 ！*CPUVisible*调整栏的大小失败时的内存段*CPUHostAperture* PCI aperture 中提供。 *CPUHostAperture*表现为基于页的管理器，然后可以直接访问通过视频内存的区域映射[ *DxgkDdiMapCpuHostAperture*](https://msdn.microsoft.com/library/windows/hardware/dn906340)设备驱动程序接口 (DDI) 函数。 这使我们能够然后将虚拟地址空间的范围映射到非连续范围的直接*CPUHostAperture*，并且具有*CPUHostAperture*然后将映射到不需要的视频内存swizzling 范围。

最大 CPU 中，可以引用的可锁定内存量 ！*CPUVisible*内存段仅限于的大小*CPUHostAperture*。 公开的详细信息*CPUHostAperture*到 Microsoft DirectX 图形可以中找到内核[CPU 主机 aperture](cpu-host-aperature.md)主题。

## <a name="span-idiocoherencyspanspan-idiocoherencyspanspan-idiocoherencyspanio-coherency"></a><span id="I_O_coherency"></span><span id="i_o_coherency"></span><span id="I_O_COHERENCY"></span>I/O 一致性


在 x86/x64 上今天，我们要求所有 Gpu 都支持 I/O 一致性通过 PCIe 以便 GPU 进行读取或写入到可缓存的系统内存图面，维护，cpu 的一致性。 当为缓存从 GPU 的角度一致映射图面时，GPU 需要访问在图面时搜索 CPU 缓存。 这种形式的相干性通常用于资源 CPU 应读取，例如某些临时图面。

在某些 ARM 平台上，I/O 一致性不支持直接在硬件中。 在这些平台上，I/O 一致性需要通过手动使 CPU 缓存层次结构进行模拟。 视频内存管理器来实现此立即通过跟踪对来自 GPU （分配读/写操作） 的分配的操作，以及 CPU （映射操作，读/写） 和发出时我们确定缓存可以缓存失效包含需要写回的数据 （CPU 写 GPU 读取） 或包含需要失效的旧数据 （GPU 写 CPU 读取）。

在平台上用任何 I/O 一致性，负责跟踪对分配的 CPU 和 GPU 访问落到用户模式驱动程序。 公开一个新图形内核*使之无效的缓存*DDI 用户模式驱动程序可能使用写回并使相关联的可缓存分配的虚拟地址范围无效。 在平台上不具有对 I/O 一致性的支持，用户模式驱动程序将需要 CPU 写入后和 GPU 读取之前以及之后写入和 CPU 读取之前调用此函数。 后一种可能看起来不直观一开始，但由于 CPU 无法使其对内存之前 GPU 数据写入具有推测性读取，则必须使所有 CPU 缓存，以确保 CPU 重新从 RAM 读取数据都失效。

 

 





