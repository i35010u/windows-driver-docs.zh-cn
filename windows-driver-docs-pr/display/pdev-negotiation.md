---
title: PDEV 协商
description: PDEV 协商
ms.assetid: d3172dd2-ecf1-4ad8-ba52-776bf712ab7c
keywords:
- GDI WDK Windows 2000 显示，PDEV 协商
- 图形驱动程序 WDK Windows 2000 显示，PDEV 协商
- 绘制 WDK GDI，PDEV 协商
- 协商 WDK GDI
- PDEV WDK GDI
- DrvEnablePDEV
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16663bffc5f33a671dd0bb15a0d8e0c82a666261
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554635"
---
# <a name="pdev-negotiation"></a>PDEV 协商


## <span id="ddk_pdev_negotiation_gg"></span><span id="DDK_PDEV_NEGOTIATION_GG"></span>


任何图形驱动程序的主要职责之一是能够*PDEV*在驱动程序初始化过程中。 PDEV 是物理设备的逻辑表示形式。 这种表示形式由驱动程序定义，通常是一种专用的数据结构。 请参阅[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)启用 PDEVs 有关详细信息。

通过*DrvEnablePDEV*函数，该驱动程序必须提供信息，向 GDI 描述所需的设备和其功能。 一种驱动程序提供了 GDI 的重要信息是组的图形功能标志 (GCAPS\_Xxx 和 GCAPS2\_Xxx 标志) 在**flGraphicsCaps**和**flGraphicsCaps2**的成员[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构。

功能标志允许 GDI 来确定 PDEV 支持哪些操作。 例如，GDI 测试的功能标志，指示是否 PDEV 之前可以处理贝塞尔曲线和几何宽线条尝试调用 GDI [ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)函数来绘制路径这些基元类型。 如果功能标志指示 PDEV 无法处理这些基元类型，GDI 将分解的直线或曲线以便它可以进行更简单调用向驱动程序。

从驱动程序的端，只要该驱动程序从 GDI，获取与路径相关的高级的调用它可返回**FALSE**如果路径或剪辑太过复杂，要处理的设备。

该驱动程序不能返回**FALSE**从*DrvStrokePath*处理时[修饰的行](cosmetic-lines.md)因为驱动程序必须处理任何复杂的剪辑或修饰线样式。 但是， *DrvStrokePath*可以返回**FALSE**如果该路径包含贝塞尔曲线或几何行。 当发生这种情况时，GDI 将中断该层更简单调用会将调用，如果未设置容量位一样。 例如，如果*DrvStrokePath*返回**FALSE**收到几何行，简化了的行和调用 GDI [ **DrvFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556220)函数。

如果*DrvStrokePath*将报告错误，它必须返回 DDI\_错误。

这种协商之间 GDI 和驱动程序，依赖于 PDEV，函数允许 GDI 和驱动程序以生成高质量的输出，而无需过多的通信。

 

 





