---
title: Swizzling 范围类
description: Swizzling 范围类
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- swizzling 范围类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7216397e9518a45acb06d289c7d9f777e37efdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554687"
---
# <a name="swizzling-range-class"></a>Swizzling 范围类


Windows 显示器驱动程序模型 (WDDM) 不允许为一个 swizzling 调用范围类函数以可重入的方式。 它最，一个线程可以运行中的以下函数之一在给定时间：

-   [*DxgkDdiAcquireSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559582)

-   [*DxgkDdiReleaseSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559786)

 

 





