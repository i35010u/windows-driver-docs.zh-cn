---
title: 线程处理和同步的第一个级别
description: 线程处理和同步的第一个级别
ms.assetid: 9fce6a18-2a66-4518-b05b-e85bdaa3951f
keywords:
- 线程处理 WDK 显示，首先级别
- 同步 WDK 显示，第一个级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac8e9c989ca46fcfd84b15c3ec2e414bdd6f63eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533808"
---
# <a name="threading-and-synchronization-first-level"></a>线程处理和同步的第一个级别


Windows 显示驱动程序模型 (WDDM) 对显示微型端口驱动程序的线程处理的第一个级别下所做的调用和同步到以下 nonreentrancy 类进行分类。 没有可重入性允许特定的类中。 也就是说，只有一个线程可以输入特定的类; 中的驱动程序但是，调用从多个类和[零级](threading-and-synchronization-zero-level.md)可以同时输入调用。

**请注意**  尽管两个或多个线程从不同的类，从线程[零级](threading-and-synchronization-zero-level.md)调用可以在驱动程序运行在同一时间，没有两个线程可以属于单个进程。

 

**请注意**  子设备 （即，同时调用允许到多个子设备） 的每次同步子 I/O 类函数。 但是，如果子设备之间存在内部的依赖项，显示微型端口驱动程序必须阻止所需的调用。

 

-   [指针类](pointer-class.md)

-   [GPU 计划程序类](gpu-scheduler-class.md)

-   [Swizzling 范围类](swizzling-range-class.md)

-   [覆盖类](overlay-class.md)

-   [子 I/O 类](child-i-o-class.md)

-   [显示类](display-class.md)

 





