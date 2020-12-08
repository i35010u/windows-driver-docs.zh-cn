---
title: 控制台和远程 IDD 的 IddCx 1.4 更新
description: 适用于控制台和远程间接显示驱动程序的 IddCx 版本1.4 更新
ms.date: 09/28/2020
keywords:
- 控制台和远程间接显示驱动程序，IddCx 版本1.4 及更高版本
- 控制台和远程 IDD，IddCx 版本1.4 及更高版本
- 控制台间接显示驱动程序
- 控制台 IDD
- 远程间接显示驱动程序
- 远程 IDD
ms.localizationpriority: medium
ms.openlocfilehash: aa090da09e06298656368b3ac48362789f2420d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808445"
---
# <a name="iddcx-14-updates-for-console-and-remote-idds"></a>控制台和远程 IDD 的 IddCx 1.4 更新

以下 IddCx 版本1.4 更新适用于控制台和远程间接显示驱动程序 (IDDs) 。

远程 IDDs 的开发人员还应参阅用于 [远程 IDDs 的 IddCx 1.4 更新](iddcx1.4-updates-for-remote-idds.md) 以获取更多远程特定的更新。

## <a name="update-iddcxgetversion-version"></a>更新 IddCxGetVersion 版本

Windows 10 上的 [**IddCxGetVersion**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxgetversion) 返回的 IddCx 版本1903已更新为 IDDCX_VERSION_19H1 (0x1400) 。

## <a name="provide-a-preferred-rendering-adapter-used-to-render-the-desktop-into-the-swapchain"></a>提供用于将桌面渲染到存在的首选渲染适配器

IddCx 1.4 之前的 IddCx 版本使用开机自检 [ (POST) 适配器](plug-and-play--pnp--start-and-stop-cases.md) 来呈现传递到 IDD 的桌面图像（如果它未 PnpStopped）。 如果 PnpStopped 了 POST 适配器，则改为使用系统提供的 Windows 高级光栅化平台 (弯曲) 。 但是，有一些配置和方案，使用 POST 适配器并不能提供最佳的用户体验。

IddCx 1.4 包含可选的 [**IddCxAdapterSetRenderAdapter**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadaptersetrenderadapter) OS 回调。 IDD 可以调用 **IddCxAdapterSetRenderAdapter** 来设置要用于该适配器上的所有交换链的呈现适配器。

Windows 的 "设置" 应用程序中还提供了 "图形设置" 页，该页面允许用户设置节能或高性能 GPU 的首选项。 下表介绍了如何将这两项功能合并到具有 Intel 集成和 Nvidia 离散 GPU 的 Surface Book 设备上。

| IDD 的 GPU pref\* | 用户/OS pref\*\* | DWM 的枚举\+ | 应用的枚举\+\+ | Intel 路径 ~ | Nvidia 路径 ~ ~ | 存在 GPU ^ |
| ----------------- | ------ | ------ | ------ | -------------------- | -------------------- | ------ |
| **无或 Intel** | 系统 | Intel  | Intel  | 同一适配器         | 混合跨适配器 | Intel  |
| **无或 Intel** | 强力  | Intel  | Intel  | 同一适配器         | 混合跨适配器 | Intel  |
| **无或 Intel** | 性能   | Intel  | Nvidia | 同一适配器         | 混合跨适配器 | Intel  |
| **Nvidia**        | 系统 | Nvidia | Nvidia | 混合跨适配器 | 同一适配器         | Nvidia |
| **Nvidia**        | 强力  | Nvidia | Intel  | 混合跨适配器 | 同一适配器         | Nvidia |
| **Nvidia**        | 性能   | Nvidia | Nvidia | 混合跨适配器 | 同一适配器         | Nvidia |

其中：

* \*IDD 的 GPU pref = IDD 的首选 GPU
* \*\*User/OS pref = 用户 (应用程序) 或操作系统的 GPU 首选项
* \+DWM 的枚举 = DX 运行时枚举桌面 Windows Manager 上的 ID 监视器的 GPU (DWM) 
* \+\+应用的枚举 = DX 运行时枚举应用程序上的 ID 监视器的 GPU
* 当应用程序在 Intel 上时，~ intel 路径 = 应用程序到 DWM 的演示路径
* 约为 nvidia 路径 = 应用程序在 Nvidia 上时的应用程序到 DWM 显示路径
* ^ 存在 GPU = 在其上创建间接显示的存在的 GPU

## <a name="update-evtiddcxmonitorassignswapchain-error-handling-for-windows-10-version-1903-and-later"></a>更新 Windows 10 版本1903及更高版本的 EvtIddCxMonitorAssignSwapChain 错误处理

从 Windows 10 开始，版本1903，针对所有驱动程序版本的 [**EvtIddCxMonitorAssignSwapChain**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain) 回调的 IddCx 错误处理已更改，并引入了新的状态代码。 有关详细信息，请参阅 [ **EvtIdCxMonitorAssignSwapChain** 错误处理](idd-evtiddcxmonitorassignswapchain-error-handling.md)。

## <a name="for-edid-less-scenarios-add-evt_idd_cx_monitor_get_physical_size-to-provide-the-physical-width-and-height-of-the-monitor"></a>对于无 EDID 方案，请添加 EVT_IDD_CX_MONITOR_GET_PHYSICAL_SIZE 以提供监视器的物理宽度和高度

有时，IDD 需要提供物理监视器大小（即使在监视器说明不可用时） (例如，在将非 Windows 平台用作监视器) 时也是如此。 与其他桌面配置属性不同，监视器的物理大小是监视器的一个功能，因此，一旦添加监视器，就无法更改。 如果 IDD 提供了监视器说明，则操作系统将从该说明中获取物理大小。 如果 IDD 无法提供说明，操作系统将调用可选的 [**EVT_IDD_CX_MONITOR_GET_PHYSICAL_SIZE**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_get_physical_size) 驱动程序回调来检索物理大小。 此回调作为 [**IddCxMonitorArrival**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival) 调用的一部分进行调用。

## <a name="build-iddcx-v14-drivers-that-run-on-multiple-versions-of-iddcx"></a>生成在多个版本的 IddCx 上运行的 IddCx 1.4 驱动程序

由于在 IddCx 1.3 for Windows 10 版本1809中所做的更改，以及在 IddCx 1.4 中所做的更改，因此可以生成单个 IDD，以便在 Windows 10 版本1809和更高版本上运行。 有关详细信息，请参阅 [生成 IddCx 1.4 驱动程序](building-iddcx1.4-drivers.md) 。
