---
title: 重排范围类
description: 重排范围类
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- swizzling 范围类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc6ffabc3a670520d5aa889f70f1a33a4b1936b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829539"
---
# <a name="swizzling-range-class"></a>重排范围类


Windows 显示驱动程序模型（WDDM）不允许以可重入方式调用 swizzling 范围类中的一个函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

-   [*DxgkDdiAcquireSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)

-   [*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)

 

 





