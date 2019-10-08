---
title: 验证混合系统配置
ms.assetid: 9DB53DAB-0A3D-48A4-84C0-8D60F56B64E8
description: 要验证的混合系统的过程的 description。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89920a5759876e703358a0a271006c022a357e54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374367"
---
# <a name="validating-a-hybrid-system-configuration"></a>验证混合系统配置


此过程是从开始使用 Windows 8.1 中验证的配置[混合系统](using-cross-adapter-resources-in-a-hybrid-system.md)的显示适配器：

1.  在系统引导时，显示适配器之一被标记为当前的 POST 适配器。 如果此 POST 适配器支持 Windows 显示驱动程序模型 (WDDM) 1.3，并且具有集成的显示面板，它被视为*集成的混合*适配器。
2.  在混合系统中的离散适配器被视为*混合离散*适配器。 该数据库必须：
    -   设置[ **DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**HybridDiscrete**成员。
    -   支持 WDDM 1.3。
    -   支持跨适配器资源。
    -   没有显示输出。

3.  只有一个 WDDM 混合离散适配器允许在系统上。
4.  检测到集成的混合适配器时：
    -   任何新的 WDDM 1.3 显示适配器 (不包括适配器相匹配 (2) 或 (3) 或者是基本显示或基本呈现驱动程序) 将不会加载。
    -   任何加载的 WDDM 1.3 显示适配器 (不包括适配器相匹配 (2) 或 (3) 或者是基本显示或基本呈现驱动程序) 的不是混合离散适配器将被停止。

5.  支持 1.3 之前的版本中 WDDM 驱动程序可以加载即使集成的混合适配器不存在。

 

 





