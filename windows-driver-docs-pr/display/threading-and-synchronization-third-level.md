---
title: 线程处理和同步第三个级别
description: 线程处理和同步第三个级别
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- 线程处理 WDK 显示，第三个级别
- 同步 WDK 显示、 第三个级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 647c5fd9bae10c25aa7f6dedcef25d2e3a0214ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554949"
---
# <a name="threading-and-synchronization-third-level"></a>线程处理和同步第三个级别


Windows 显示驱动程序模型 (WDDM) 保证的线程处理和同步的第三个级别下执行到显示微型端口驱动程序的以下调用。 这可确保只有一个线程 （即，调用线程） 是在驱动程序中。 此外，图形硬件是空闲状态，不直接内存访问 (DMA) 缓冲区当前处理由驱动程序或通过 GPU 计划程序，并且完全逐出的视频内存来承载 CPU 内存。

-   [*DxgkDdiAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559586)

-   [*DxgkDdiQueryChildRelations*](https://msdn.microsoft.com/library/windows/hardware/ff559750)

-   [*DxgkDdiRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559789)

-   [*DxgkDdiResetFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559815)

-   [*DxgkDdiRestartFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559820)

-   [*DxgkDdiSetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff560764)

-   [*DxgkDdiStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560775)

-   [*DxgkDdiStopDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560781)

-   [*DxgkDdiUnload*](https://msdn.microsoft.com/library/windows/hardware/ff560801)

 

 





