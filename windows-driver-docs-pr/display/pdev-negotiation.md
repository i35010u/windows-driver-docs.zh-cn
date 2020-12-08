---
title: PDEV 协商
description: PDEV 协商
keywords:
- GDI WDK Windows 2000 显示，PDEV 协商
- 图形驱动程序 WDK Windows 2000 显示，PDEV 协商
- 绘制 WDK GDI，PDEV 协商
- 协商 WDK GDI
- PDEV WDK GDI
- DrvEnablePDEV
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0b960cf68976d1958128946de91ad0fcdaba669
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838067"
---
# <a name="pdev-negotiation"></a>PDEV 协商

任何图形驱动程序的主要职责之一就是在驱动程序初始化过程中启用 *PDEV* 。 PDEV 是物理设备的逻辑表示形式。 此表示形式由驱动程序定义，通常是专用数据结构。 有关启用 PDEVs 的详细信息，请参阅 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 。

通过 *DrvEnablePDEV* 函数，驱动程序必须向 GDI 提供信息，用于描述请求的设备及其功能。 驱动程序提供 GDI 的一小部分重要信息是一组图形功能标志 (GCAPS_Xxx 并 GCAPS2_Xxx 标志) 在 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构的 **flGraphicsCaps** 和 **flGraphicsCaps2** 成员中。

功能标志允许 GDI 确定 PDEV 支持的操作。 例如，GDI 测试了一些功能标志，这些标志指示 PDEV 是否可以处理贝塞尔曲线和几何宽线条，然后，GDI 会尝试调用 [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath) 函数来绘制具有这些基元类型的路径。 如果功能标志指示 PDEV 无法处理这些基元类型，则 GDI 将分解这些线条或曲线，以便可以更轻松地调用驱动程序。

从驱动程序的端来看，每当驱动程序从 GDI 获取与高级路径相关的调用时，如果路径或剪辑太复杂而无法处理，则它可能会返回 **FALSE** 。

当处理 [修饰线条](cosmetic-lines.md)时，驱动程序无法从 *DrvStrokePath* 返回 **FALSE** ，因为驱动程序必须处理修饰线的任何复杂剪裁或样式。 但是，如果路径具有贝塞尔曲线或几何线条，则 *DrvStrokePath* 可以返回 **FALSE** 。 发生这种情况时，GDI 会将调用分解为更简单的调用，就像在未设置功能位时那样。 例如，如果 *DrvStrokePath* 在发送几何线条时返回 **FALSE** ，则 GDI 将简化该行并调用 [**DrvFillPath**](/windows/win32/api/winddi/nf-winddi-drvfillpath) 函数。

如果 *DrvStrokePath* 要报告错误，则它必须返回 DDI_ERROR。

GDI 和驱动程序之间的这种协商（对于依赖于 PDEV 的函数）允许 GDI 和驱动程序生成高质量的输出，而无需过度通信。
