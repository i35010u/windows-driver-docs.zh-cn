---
title: WDDM 驱动程序和功能上限
description: 本主题介绍 Windows 显示器驱动程序模型 (WDDM) 驱动程序功能 (cap)。
ms.assetid: 452ADF64-A5CC-4694-BE31-FBED29B32DC1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4829321bd5a4ec2b63aa300a3c55198b3f2591d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380523"
---
# <a name="wddm-driver-and-feature-caps"></a>WDDM 驱动程序和功能上限


本主题介绍 Windows 显示器驱动程序模型 (WDDM) 驱动程序功能 (cap)。

此表列出了指定到 Windows WDDM 驱动程序类型和版本的驱动程序的要求。

**WDDM 1.2 驱动程序要求**

| WDDM 驱动程序类型 | DDI 要求                                                                                                                                                                                                                                           |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 所有的图形    | 实现所有呈现器特定于和显示特定于所需设备驱动程序接口 (DDIs)                                                                                                                                                            |
| 仅显示     | 实现所有显示特定于 DDIs 并为所有特定于呈现的 DDIs 返回 null 指针                                                                                                                                                         |
| 仅呈现器      | 实现所有特定于呈现的 DDIs 并为所有特定于显示的 DDIs 返回 null 指针或实现的完全 WDDM 驱动程序的所有 DDIs 但报告显示\_适配器\_信息。NumVidPnSources = 0 和显示\_适配器\_信息。NumVidPnTargets = 0。 |

 

此表列出了所有可见 WDDM 1.2 驱动程序所需设置的 Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 功能。 "M"表示一个必需的功能，"O"表示可选的并"NA"指示不适用。 若要阅读有关每个功能的详细信息，请在左侧列中的链接。

**WDDM 1.2 功能 cap**

| 功能                                                                                                                                          | 完整的图形驱动程序 | 仅呈现驱动程序 | 仅显示驱动程序 | 功能 cap                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|--------------------|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WDDM 版本                                                                                                                                     | M                    | M                  | M                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**WDDMVersion**                                                                                                                                                                |
| [即插即用 (PnP) 开始和停止](plug-and-play--pnp--start-and-stop-cases.md):Bug 检查和即插即用停止对非 VGA 的支持                   | M                    | NA                 | M                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps).**SupportNonVGA**                                                                                                                                                              |
| [优化的屏幕旋转支持](optimized-screen-rotation-support.md)                                                                       | M                    | NA                 | M                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps).**SupportSmoothRotation**                                                                                                                                                      |
| [GPU 抢占](gpu-preemption.md)                                                                                                             | M                    | M                  | NA                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps).**PreemptionCaps**                                                                                                                                                             |
| [**DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps).**FlipOnVSyncMmIo**                                                                                  | M                    | M                  | NA                  | [**DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)。**FlipOnVSyncMmIoFlipOnVSyncMmIo**已从 Windows Vista 开始提供; 从 Windows 8 开始的要求是设置**FlipOnVSyncMmIo**上限。                       |
| [在 Windows 8 中 TDR 更改](tdr-changes-in-windows-8.md)                                                                                         | M                    | M                  | NA                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps).**SupportPerEngineTDR**                                                                                                                                                        |
| [备用休眠优化](standby-hibernate-optimizations.md):优化图形堆栈来提高睡眠的性能和恢复 | O                    | O                  | NA                  | [**DXGK\_SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)。**标志**                                                                                                                                                      |
| [立体 3D](stereoscopic-3d.md):新的基础结构到进程并显示立体内容                                           | O                    | NA                 | NA                  | [**D3DKMDT\_VIDPN\_源\_模式\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_source_mode_type)                                                                                                                                               |
| [Direct 翻转的视频内存](direct-flip-of-video-memory.md)                                                                                   | M                    | NA                 | NA                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps).**SupportDirectFlip**                                                                                                                                                          |
| [GDI 硬件加速](gdi-hardware-acceleration.md):所需的功能开始 WDDM 1.1                                            | M                    | M                  | NA                  | [**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps).**SupportKernelModeCommandBuffer**                                                                                                                                 |
| [GPU 电源管理的空闲状态和活动的电源](gpu-power-management-of-idle-and-active-power.md)                                        | O                    | O                  | O                   | 如果支持此功能，则[ *DxgkDdiSetPowerComponentFState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)并[ *DxgkDdiPowerRuntimeControlRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)函数必须支持。 |

 

 

 





