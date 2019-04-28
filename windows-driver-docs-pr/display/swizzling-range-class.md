---
title: 重排范围类
description: 重排范围类
ms.assetid: 2f5d5b91-ebd8-4242-8719-8a21bc3e9888
keywords:
- swizzling 范围类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7216397e9518a45acb06d289c7d9f777e37efdd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345504"
---
# <a name="swizzling-range-class"></a>重排范围类


Windows 显示器驱动程序模型 (WDDM) 不允许为一个 swizzling 调用范围类函数以可重入的方式。 它最，一个线程可以运行中的以下函数之一在给定时间：

-   [*DxgkDdiAcquireSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559582)

-   [*DxgkDdiReleaseSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559786)

 

 





