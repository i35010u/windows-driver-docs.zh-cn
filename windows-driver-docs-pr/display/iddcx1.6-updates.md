---
title: IddCx 版本1.6 及更高版本的更新
description: 适用于控制台和远程间接显示驱动程序的 IddCx 版本1.6 更新
ms.date: 10/20/2020
keywords:
- 控制台和远程间接显示驱动程序，IddCx 版本1.6 及更高版本
- 控制台和远程 IDD，IddCx 版本1.6 及更高版本
- 控制台间接显示驱动程序
- 控制台 IDD
- 远程间接显示驱动程序
- 远程 IDD
ms.localizationpriority: medium
ms.openlocfilehash: cd494663277f55a12af225f0db6abdd3c7a09615
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839601"
---
# <a name="updates-for-iddcx-versions-16-and-later"></a>IddCx 版本1.6 及更高版本的更新

IddCx 版本1.6 中的以下更新适用于控制台和远程间接显示驱动程序 (IDDs) 。

IddCx 版本1.6 之前的版本1.4。 IddCx 版本1.5 只包含内部更改，这些更改不会影响外部间接显示驱动程序 (IDDs) 。 有关版本1.4 的详细信息，请参阅 [IddCx 1.4 updates](iddcx1.4-updates.md)。

## <a name="updated-iddcxgetversion-version"></a>更新的 IddCxGetVersion 版本

Windows 10 上的 [**IddCxGetVersion**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxgetversion) 返回的 IddCx 版本已更新到 IDDCX_VERSION_MANGANESE (0x1600) 。

## <a name="wpp-information-in-public-iddcx-symbols"></a>公共 IddCx 符号中的 WPP 信息

从 IddCx 版本1.6 开始，公共 IddCx 符号文件包含所有 Windows 软件跟踪处理器 (WPP) 信息。 这意味着， [**！ wmitrace**](../debugger/-wmitrace-logdump.md) 调试程序命令在内核调试器中进行解码并显示 WPP 消息。

## <a name="ability-to-access-buffers-allocated-in-system-memory"></a>能够访问系统内存中分配的缓冲区

在某些情况下，存在缓冲区驻留在系统内存中;例如，使用的呈现适配器是 (Windows 高级光栅化平台的弯曲，系统提供的软件呈现器) 。 IddCx 1.6 添加了以下 OS 回调，它们允许驱动程序访问系统内存中的缓冲区，同时避免子资源副本：

* [**IddCxSwapChainInSystemMemory**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchaininsystemmemory) 允许 IDD 检查存在的缓冲区是否驻留在系统内存中。 此回调的结果在存在的整个生存期内保持不变。 驱动程序应在其 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) 回调中检查此回调的值，并设置状态以释放和获取缓冲区。

* [**IddCxSwapChainReleaseAndAcquireSystemBuffer**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchainreleaseandacquiresystembuffer) 允许 IDD 释放和获取缓冲区，并获取访问缓冲区 (的信息，例如系统内存指针、缓冲区的间距/跨距、表面格式和尺寸) 。 直到下一次成功调用此函数时，返回的缓冲区才有效。

  在分配新的存在时，驱动程序必须决定 IddCxSwapChainReleaseAndAcquireBuffer IddCxSwapChainReleaseAndAcquireSystemBuffer 的哪一种 **IddCxSwapChainReleaseAndAcquireBuffer** / **IddCxSwapChainReleaseAndAcquireSystemBuffer** ，并在该存在的其余部分继续使用该变体。 若要确定，驱动程序应考虑其特定要求和调用 [**IddCxSwapChainInSystemMemory**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchaininsystemmemory)的结果。 如果驱动程序发生以下情况，则驱动程序将导致操作系统错误检测 UMDF 进程：

  * 调用 **IddCxSwapChainReleaseAndAcquireSystemBuffer** IddCxSwapChainReleaseAndAcquireBuffer 的其他变体 / **IddCxSwapChainReleaseAndAcquireBuffer**。
  * 当 **IddCxSwapChainInSystemMemory** 返回 false 时调用 **IddCxSwapChainReleaseAndAcquireSystemBuffer** 。

建议但不要求驱动程序使用这些回调函数。 IddCx 1.6 之前的行为仍然受支持。

## <a name="ability-to-access-buffers-in-physically-contiguous-memory"></a>能够在物理上连续的内存中访问缓冲区

从 IddCx 1.6 开始，添加了 [**IDDCX_ADAPTER_FLAGS_PREFER_PHYSICALLY_CONTIGUOUS**](/windows-hardware/drivers/ddi/iddcx/ne-iddcx-iddcx_adapter_flags) 标志和 [**IddCxSwapChainGetPhysicallyContiguousAddress**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchaingetphysicallycontiguousaddress) OS 回调函数，以便能够在物理上连续的内存中访问缓冲区。

显示驱动程序可以通过在 [**IDDCX_ADAPTER_CAPS**](/windows-hardware/drivers/ddi/iddcx/ns-iddcx-iddcx_adapter_caps)中设置 [**IDDCX_ADAPTER_FLAGS_PREFER_PHYSICALLY_CONTIGUOUS**](/windows-hardware/drivers/ddi/iddcx/ne-iddcx-iddcx_adapter_flags)标志来请求在物理上连续的系统内存中分配主要表面。 这样，驱动程序便可直接在不使用中间副本的情况下扫描表面。

不保证在初始化期间驱动程序的请求已成功。 如果请求未成功，则对 [**IddCxAdapterInitAsync**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync) 的调用将失败。 相反，一旦驱动程序执行了 [**IddCxSwapChainReleaseAndAcquireBuffer**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchainreleaseandacquirebuffer) (或 [**IddCxSwapChainReleaseAndAcquireSystemBuffer**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchainreleaseandacquirebuffer)) ，它应调用 [**IddCxSwapChainGetPhysicallyContiguousAddress**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchaingetphysicallycontiguousaddress) 来检索图面的物理地址。 **IddCxSwapChainGetPhysicallyContiguousAddress** 将首先等待任何挂起的 render 命令，然后刷新并使与存储图面的地址范围关联的 CPU 缓存失效。 但是，如果在物理上连续的内存中分配的图面的初始请求失败，则 **IddCxSwapChainGetPhysicallyContiguousAddress** 将返回 E_NOINTERFACE。
