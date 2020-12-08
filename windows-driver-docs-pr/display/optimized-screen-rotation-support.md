---
title: 优化的屏幕旋转支持
description: Windows 8 通过确保图形适配器的输出在旋转模式发生变化时保持启用状态，从而确保无闪烁屏幕旋转体验。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e97bcc8fe26f69763d282245190c1bbd12a200
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794999"
---
# <a name="optimized-screen-rotation-support"></a>优化的屏幕旋转支持


Windows 8 通过确保图形适配器的输出在旋转模式发生变化时保持启用状态，从而确保无闪烁屏幕旋转体验。 支持旋转模式 (WDDM) 1.2 驱动程序的所有 Windows 显示器驱动程序模型都需要此功能。

**注意**  从 Windows 8.1 更新开始，会更新设备驱动程序接口 (DDIs) ，以便在旋转主显示器时支持克隆的监视器上可能的最高分辨率。 请参阅 [支持 Path-Independent 旋转](supporting-path-independent-rotation.md)。

 

**最小 WDDM 版本**：1。2

**最低 Windows 版本**：8

**驱动程序实现-完整图形和显示**：必需


 

## <a name="span-idsmooth_rotation_ddispanspan-idsmooth_rotation_ddispanspan-idsmooth_rotation_ddispansmooth-rotation-ddi"></a><span id="Smooth_rotation_DDI"></span><span id="smooth_rotation_ddi"></span><span id="SMOOTH_ROTATION_DDI"></span>平滑旋转 DDI


如果调用了这些驱动程序实现的函数，则显示微型端口驱动程序必须支持更新路径旋转：

-   [*DxgkDdiCommitVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)
-   [*DxgkDdiUpdateActiveVidPnPresentPath*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)

驱动程序必须通过设置 [**DXGK \_ DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)结构的 **SupportSmoothRotation** 成员（从 Windows 8 开始提供），指示对 [*DxgkDdiUpdateActiveVidPnPresentPath*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)的调用中的平滑旋转支持。
在对 [*DxgkDdiCommitVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)的调用过程中，驱动程序必须始终能够设置路径旋转。

## <a name="span-idsmooth_rotation_scenariosspanspan-idsmooth_rotation_scenariosspanspan-idsmooth_rotation_scenariosspansmooth-rotation-scenarios"></a><span id="Smooth_rotation_scenarios"></span><span id="smooth_rotation_scenarios"></span><span id="SMOOTH_ROTATION_SCENARIOS"></span>平滑旋转方案


在传统的台式机和便携式系统上，屏幕旋转并不是一种常用方案。 但在移动设备中，屏幕旋转通常是主流方案。 Windows 8 为显示基础结构启用优化，以确保在屏幕旋转过程中监视器同步保持启用状态。 如果满足以下条件，最终用户可能会遇到平滑的旋转过渡：

-   平台正在运行 WDDM 1.2。
-   桌面组合管理器处于打开状态，并且正在积极撰写。
-   确定模式更改请求与平滑旋转模式过渡兼容。 如果两种模式具有相同的尺寸（ (的宽度和高度) 、拓扑、刷新率、像素格式和步幅），并且仅在屏幕方向上不同，则这两种模式的兼容性 (也就是说，将) 旋转。

 

