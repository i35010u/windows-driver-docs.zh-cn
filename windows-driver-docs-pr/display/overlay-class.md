---
title: 覆盖类
description: 覆盖类
ms.assetid: 698eb8af-ff9a-4c11-b764-6e5773886aaa
keywords:
- 覆盖类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec3b75dd407f3fe4a253a724de87f7110c98885
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826087"
---
# <a name="overlay-class"></a>覆盖类


Windows 显示驱动程序模型（WDDM）不允许以可重入方式调用某个覆盖类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

-   [*DxgkDdiCreateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createoverlay)

-   [*DxgkDdiDestroyOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyoverlay)

-   [*DxgkDdiFlipOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_flipoverlay)

-   [*DxgkDdiUpdateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateoverlay)

 

 





