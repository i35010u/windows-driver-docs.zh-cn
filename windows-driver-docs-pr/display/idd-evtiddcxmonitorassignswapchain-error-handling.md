---
title: EvtIddCxMonitorAssignSwapChain 错误处理
description: 与 EvtIddCxMonitorAssignSwapChain 关联的错误处理
ms.assetid: 68e5f3cd-2551-4e36-85dc-5bc42e0e48a6
ms.date: 09/28/2020
keywords:
- EvtIddCxMonitorAssignSwapChain，错误处理
- EvtIddCxMonitorAssignSwapChain 错误处理，间接显示驱动程序
- EvtIddCxMonitorAssignSwapChain 错误处理，IDD
ms.localizationpriority: medium
ms.openlocfilehash: 4e97f5629c62da65627aa41a9de8d60503385ec7
ms.sourcegitcommit: a32079f3cc5d564d3b12576f832ed442a6b1a918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92793484"
---
# <a name="evtiddcxmonitorassignswapchain-error-handling"></a>EvtIddCxMonitorAssignSwapChain 错误处理

## <a name="change-in-evtiddcxmonitorassignswapchain-error-handling"></a>EvtIddCxMonitorAssignSwapChain 错误处理中的更改

在 Windows 10 版本1903之前的版本中，桌面组合的其余部分不能识别 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) 是否失败。 它继续呈现并显示间接显示适配器未处理的帧，导致 IddCx 在一段时间后终止间接显示驱动程序 (IDD) 。

从 Windows 10 版本1903开始，针对所有驱动程序版本更改了此回调的 IddCx 错误处理，并引入了 **STATUS_GRAPHICS_INDIRECT_DISPLAY_ABANDON_SWAPCHAIN** 状态代码。 有关详细信息，请参阅 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) 。

## <a name="handling-errors-in-the-frame-processing-loop-thread"></a>处理帧处理循环线程中的错误

IDD 成功从 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) 返回后，它拥有 **hSwapChain** 对象。
如果驱动程序遇到错误，导致无法继续处理该帧，它可以调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 来释放所有权。 OS 将检测删除并导致创建新的存在。

如果驱动程序知道无法从此错误中恢复，则它应调用 [**IddCxReportCriticalError**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxreportcriticalerror) 来停止设备。

## <a name="suggested-approach-to-handle-swapchain-errors"></a>处理存在错误的建议方法

在 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) 回调或处理帧时出现故障的原因有多种。 故障分类包括：

* 特定于解决方案的暂时性问题，如硬件的暂时性问题。 这种类型的问题可以通过轻型恢复机制解决，这种恢复机制不会对用户体验造成影响，因为恢复速度通常会在一秒的时间内 () ，并不会影响屏幕上的视觉内容 (例如，不) 闪烁。  
* 特定于您的解决方案的永久性问题，如驱动程序中的死锁或硬件的严重问题。 通常，这种类型的问题无法快速恢复。
* 由于驱动程序外部的事件而导致的 DirectX API 错误。 例如，你的驱动程序无法控制事件，例如，当你的 D3D 设备用于处理桌面映像的适配器被 PnpStopped 或发生 GPU 范围的故障并被重置时。
* 驱动程序导致的 DirectX API 错误。 驱动程序 bug 会导致 D3D 设备出错或挂起。 例如，在边界边界外使用坐标调用 **CopySubResource** 时，会将设备置于错误状态。
* 其他 IHV GPU 驱动程序导致的 DirectX API 错误。 这些错误可能是由于 IDD 中用于触发 IHV GPU 驱动程序 bug 的正确调用模式而导致的。

驱动程序很难准确区分不同的 DirectX 错误。 主要区别在于，外部 DirectX 组件导致的错误可能是暂时性的，系统将恢复到稳定状态;然而，如果错误是由间接显示或 GPU 驱动程序引起的，则可能会再次出现 bug。

请参阅 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) ，了解有关如何将这些错误传播回操作系统以便操作系统重试的详细信息。

下面是有关如何处理驱动程序中各种类型的错误的一些指导。

### <a name="transient-issues-specific-to-your-solution"></a>特定于解决方案的暂时性问题

驱动程序应在处理帧时解决问题。 此操作可能会导致在处理帧时出现较小的延迟。 如果错误定期发生，则驱动程序可以考虑将错误抢占为永久性问题。

### <a name="permanent-issues-specific-to-your-solution"></a>专用于解决方案的永久性问题

驱动程序应使用等于或高于0x100 的主要代码调用 [**IddCxReportCriticalError**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxreportcriticalerror) ，并使用唯一的主要/次要代码来表示错误类型，以帮助客户/遥测调查。

### <a name="directx-error"></a>DirectX 错误

处理 DirectX 错误的最简单方法是将其传播回操作系统，以便重试。 驱动程序应从 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain)返回 **STATUS_GRAPHICS_INDIRECT_DISPLAY_ABANDON_SWAPCHAIN** ，如果在处理帧时出现错误，驱动程序应通过调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)来释放存在。

这种简单的方法可处理由外部事件触发的错误，因为 OS 将稳定，并在新的 Dxgi 适配器) 上创建新的存在 (。 如果驱动程序的 DirectX 使用受到限制，则此方法很有效。

对于更复杂的驱动程序，这些驱动程序可能会遇到 IDD 中的 bug 导致的 DirectX 错误，或在旧/有问题的 DirectX 驱动程序上运行的驱动程序，这种方法可能会导致 ID 存在失败的无限循环。 若要避免无穷循环，IDD 可以监视这些错误的频率，并在给定阶段达到足够的错误周期时，在恢复阶段中进行移动。 如果遇到 DirectX 错误，驱动程序会销毁 DX 设备并创建新的错误，这一点很重要，因为 DX 设备处于错误状态时，它将永远不会恢复并需要重新创建。

| 当前阶段 | 如果检测到过多的连续存在 DirectX 错误，则为驱动程序操作 |
| ------------- | ------------------------------------------------------------------------- |
| [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain)提供的呈现器适配器 LUID 为硬件适配器 | 使用 Dxgi 查找软件适配器的 LUID，并调用 [**IddCxAdapterSetRenderAdapter**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadaptersetrenderadapter) 来请求操作系统使用软件适配器来呈现桌面。 |
| **EvtIddCxMonitorAssignSwapChain** 提供的呈现器适配器 LUID 为软件适配器 | 驱动程序应使用等于或高于0x100 的主要代码调用 [**IddCxReportCriticalError**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxreportcriticalerror) ，并使用唯一的主要/次要代码来表示错误类型，以帮助客户/遥测调查 |

例如，在处理帧时，驱动程序可能会在 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) 或5个故障中考虑5次连续的 DirectX 故障，同时将1分钟的帧作为条件进行处理，以在上表中执行当前阶段的恢复操作。
