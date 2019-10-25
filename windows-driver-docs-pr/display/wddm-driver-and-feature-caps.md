---
title: WDDM 驱动程序和功能上限
description: 本主题介绍 Windows 显示驱动程序模型（WDDM）驱动程序功能（cap）。
ms.assetid: 452ADF64-A5CC-4694-BE31-FBED29B32DC1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984f74aeccd52c71c7c0906b1a9eeca2c6056e0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825198"
---
# <a name="wddm-driver-and-feature-caps"></a>WDDM 驱动程序和功能上限


本主题介绍 Windows 显示驱动程序模型（WDDM）驱动程序功能（cap）。

下表列出了驱动程序为 Windows WDDM 驱动程序类型和版本指定的要求。

**WDDM 1.2 驱动程序要求**

| WDDM 驱动程序类型 | DDI 要求                                                                                                                                                                                                                                           |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 完整图形    | 实现所有特定于呈现器和特定于显示的所需设备驱动程序接口（DDIs）                                                                                                                                                            |
| 仅显示     | 实现所有显示特定的 DDIs，并为所有特定于呈现器的 DDIs 返回空指针。                                                                                                                                                         |
| 仅呈现      | 实现所有特定于呈现的 DDIs，并为所有特定于显示的 DDIs 返回 null 指针，或为完整的 WDDM 驱动程序实现所有 DDIs，但报表显示\_适配器\_信息。NumVidPnSources = 0 并显示\_适配器\_信息。NumVidPnTargets = 0。 |

 

此表列出了需要设置 WDDM 1.2 驱动程序的 Microsoft DirectX 图形内核子系统（Dxgkrnl）所可见的所有功能。 "M" 指示必需功能，"O" 表示可选，"NA" 指示不适用。 若要阅读有关每个功能的详细信息，请单击左侧列中的链接。

**WDDM 1.2 功能上限**

| 功能                                                                                                                                          | 完整图形驱动程序 | 仅限呈现的驱动程序 | 仅显示驱动程序 | 功能上限                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|--------------------|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WDDM 版本                                                                                                                                     | M                    | M                  | M                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**WDDMVersion**                                                                                                                                                                |
| [即插即用（PnP）启动和停止](plug-and-play--pnp--start-and-stop-cases.md)：对非 VGA 的 Bug 检查和 PnP 停止支持                   | M                    | NA                 | M                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**SupportNonVGA**                                                                                                                                                              |
| [优化屏幕旋转支持](optimized-screen-rotation-support.md)                                                                       | M                    | NA                 | M                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**SupportSmoothRotation**                                                                                                                                                      |
| [GPU 抢占](gpu-preemption.md)                                                                                                             | M                    | M                  | NA                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**PreemptionCaps**                                                                                                                                                             |
| [**DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)。**FlipOnVSyncMmIo**                                                                                  | M                    | M                  | NA                  | [**DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)。**FlipOnVSyncMmIoFlipOnVSyncMmIo**已从 Windows Vista 开始使用;从 Windows 8 开始的要求是设置**FlipOnVSyncMmIo** cap。                       |
| [Windows 8 中的 TDR 更改](tdr-changes-in-windows-8.md)                                                                                         | M                    | M                  | NA                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**SupportPerEngineTDR**                                                                                                                                                        |
| [备用休眠优化](standby-hibernate-optimizations.md)：优化图形堆栈以提高睡眠和恢复性能 | O                    | O                  | NA                  | [**DXGK\_SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)。**标志**                                                                                                                                                      |
| [Stereoscopic 3d](stereoscopic-3d.md)：用于处理和呈现 Stereoscopic 内容的新基础结构                                           | O                    | NA                 | NA                  | [**D3DKMDT\_VIDPN\_源\_模式\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_source_mode_type)                                                                                                                                               |
| [视频内存的直接翻转](direct-flip-of-video-memory.md)                                                                                   | M                    | NA                 | NA                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**SupportDirectFlip**                                                                                                                                                          |
| [GDI 硬件加速](gdi-hardware-acceleration.md)：从 WDDM 1.1 开始的必需功能                                            | M                    | M                  | NA                  | [**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)。**SupportKernelModeCommandBuffer**                                                                                                                                 |
| [空闲状态和活动电源的 GPU 电源管理](gpu-power-management-of-idle-and-active-power.md)                                        | O                    | O                  | O                   | 如果支持此功能，则必须支持[*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)和[*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)函数。 |

 

 

 





