---
title: 显示微型端口驱动程序的线程和同步模型
description: 显示微型端口驱动程序的线程和同步模型
keywords:
- 线程 WDK 显示，微型端口驱动程序
- 同步 WDK 显示，微型端口驱动程序
- 微型端口驱动程序 WDK 显示，同步
- 微型端口驱动程序 WDK 显示，线程
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 47952fe3ef3e28683ea907df98c59f00c5c589b9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792265"
---
# <a name="threading-and-synchronization-model-of-display-miniport-driver"></a>显示微型端口驱动程序的线程和同步模型

多个线程可以同时出现在显示微型端口驱动程序中。 这是通常的显示微型端口驱动程序可重入。 但是，对显示微型端口驱动程序的某些调用不应是可重入的，因为它们可以访问图形硬件或访问全局跨线程数据结构。 尽管不能在每次调用级别选择重入或 nonreentrancy，但 Windows 显示驱动程序模型 (WDDM) 预分配、每次调用，以及准确定义驱动程序预期的调用的同步级别：

-   [线程和同步第三级别](threading-and-synchronization-third-level.md)

-   [线程和同步第二级别](threading-and-synchronization-second-level.md)

-   [线程和同步第一级别](threading-and-synchronization-first-level.md)

-   [线程和同步零级别](threading-and-synchronization-zero-level.md)

-   [线程同步和 TDR](thread-synchronization-and-tdr.md)

 

 





