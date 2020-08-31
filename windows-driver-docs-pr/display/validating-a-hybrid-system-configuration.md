---
title: 验证混合系统配置
ms.assetid: 9DB53DAB-0A3D-48A4-84C0-8D60F56B64E8
description: 验证混合系统的过程的 decription。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2691dc4522ee9433f7c81be07e9d3b11bf13d0a1
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067056"
---
# <a name="validating-a-hybrid-system-configuration"></a>验证混合系统配置


此过程从 Windows 8.1 开始，用于验证显示适配器的 [混合系统](using-cross-adapter-resources-in-a-hybrid-system.md) 的配置：

1.  系统启动时，会将其中一个显示适配器标记为当前的 POST 适配器。 如果此 POST 适配器支持 Windows 显示驱动程序模型 (WDDM) 1.3 并且具有集成的显示面板，则会将其视为 *集成的混合* 适配器。
2.  混合系统中的离散适配器被视为 *混合离散* 适配器。 条件为：
    -   设置 [**DXGK \_ DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**HybridDiscrete** 成员。
    -   支持 WDDM 1.3。
    -   支持跨适配器资源。
    -   没有显示输出。

3.  系统中只允许有一个 WDDM 混合离散适配器。
4.  检测到集成的混合适配器时：
    -   任何新的 WDDM 1.3 显示适配器 (不包括匹配 (2) 或 (3) 的适配器，或者不会加载基本的显示或基本渲染驱动程序) 。
    -   任何加载的 WDDM 1.3 显示适配器 (不包括与 (2) 或 (3) 匹配的适配器，或者是不是混合离散适配器的基本显示或基本呈现器驱动程序) 。

5.  即使存在集成的混合适配器，支持1.3 之前的 WDDM 版本的驱动程序也能加载。

 

