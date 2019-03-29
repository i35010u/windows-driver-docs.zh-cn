---
title: 优化的屏幕旋转支持
description: Windows 8 可确保通过确保从图形适配器输出旋转模式更改期间保持已启用的闪烁屏幕旋转体验。
ms.assetid: CFDB4713-EC90-4FAB-B379-742C52888BB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5daba1898d782332cd91d0a7922a3215128ffad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568007"
---
# <a name="optimized-screen-rotation-support"></a>优化的屏幕旋转支持


Windows 8 可确保通过确保从图形适配器输出旋转模式更改期间保持已启用的闪烁屏幕旋转体验。 此功能需要对所有 Windows 显示器驱动程序模型 (WDDM) 1.2 驱动程序的支持旋转的模式。

**请注意**  从 Windows 8.1 更新开始，设备驱动程序接口 (DDIs) 经过更新以支持最大可能的解决方法克隆的监视器上旋转主显示器时。 请参阅[支持独立于路径的旋转](supporting-path-independent-rotation.md)。

 

|                                                      |           |
|------------------------------------------------------|-----------|
| WDDM 的最低版本                                 | 1.2       |
| 最大 Windows 版本                              | 8         |
| 驱动程序实现 — 仅完全图形和显示 | 强制 |

 

## <a name="span-idsmoothrotationddispanspan-idsmoothrotationddispanspan-idsmoothrotationddispansmooth-rotation-ddi"></a><span id="Smooth_rotation_DDI"></span><span id="smooth_rotation_ddi"></span><span id="SMOOTH_ROTATION_DDI"></span>顺畅旋转 DDI


显示微型端口驱动程序必须支持更新路径旋转时调用这些驱动程序实现的函数：

-   [*DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)
-   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://msdn.microsoft.com/library/windows/hardware/ff560803)

该驱动程序必须指示支持对的调用中顺畅旋转[ *DxgkDdiUpdateActiveVidPnPresentPath* ](https://msdn.microsoft.com/library/windows/hardware/ff560803)通过设置[ **DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062)结构的**SupportSmoothRotation**成员，它是从 Windows 8 开始提供。
该驱动程序必须始终为可以设置在调用期间路径旋转[ *DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)。

## <a name="span-idsmoothrotationscenariosspanspan-idsmoothrotationscenariosspanspan-idsmoothrotationscenariosspansmooth-rotation-scenarios"></a><span id="Smooth_rotation_scenarios"></span><span id="smooth_rotation_scenarios"></span><span id="SMOOTH_ROTATION_SCENARIOS"></span>顺畅旋转方案


在传统桌面和便携式计算机系统上，屏幕旋转不常用的方案。 但在移动设备屏幕旋转通常是主流方案。 Windows 8 启用优化，显示基础结构，确保在屏幕旋转过程监视同步始终启用。 当满足以下条件时，最终用户可以体验平稳旋转转换：

-   该平台正在运行 WDDM 1.2。
-   桌面组合管理器已打开并主动撰写。
-   模式更改请求确定为不符合平稳旋转模式转换。 两种模式都兼容，如果它们具有相同维度 （宽度和高度），拓扑，刷新率、 像素格式和 stride，和的区别只在于屏幕方向 （即，被旋转）。

 

 





