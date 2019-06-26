---
title: 重排范围类
description: 重排范围类
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- swizzling 范围类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8a4babc427745f13fe736227da9cd6a53f877c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372055"
---
# <a name="swizzling-range-class"></a>重排范围类


Windows 显示器驱动程序模型 (WDDM) 不允许为一个 swizzling 调用范围类函数以可重入的方式。 它最，一个线程可以运行中的以下函数之一在给定时间：

-   [*DxgkDdiAcquireSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)

-   [*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)

 

 





