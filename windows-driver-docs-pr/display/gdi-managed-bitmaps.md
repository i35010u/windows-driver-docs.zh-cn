---
title: GDI 管理的位图
description: GDI 管理的位图
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 渲染引擎 WDK GDI
- GDI WDK Windows 2000 显示，位图
- 图形驱动程序 WDK Windows 2000 显示，位图
- 绘制 WDK GDI，位图
- 位图 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25e771c92a67839ec22fde49100047a758f27cdc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796287"
---
# <a name="gdi-managed-bitmaps"></a>GDI 管理的位图


## <span id="ddk_gdi_managed_bitmaps_gg"></span><span id="DDK_GDI_MANAGED_BITMAPS_GG"></span>


GDI 以所有 *DIB* 格式管理位图，包括1、4、8、16、24和32位/像素。 GDI 可以执行所有行绘图、填充、文本输出和位块传输 (bitblt 对这些位图执行) 操作。 这使得驱动程序可以让 GDI 完成所有图形呈现，或实现其硬件提供特殊支持的功能。

如果设备的 *帧缓冲区* 采用 DIB 格式，则 GDI 可以直接执行任何或所有图形输出到帧缓冲区，从而减小驱动程序的大小。 如果设备使用非标准格式的帧缓冲区，则驱动程序必须实现所有必需的 [绘图函数](optional-display-driver-functions.md)。 GDI 仍可以模拟大多数绘制功能，但会导致性能开销：必须先将像素复制到标准格式位图，然后才能通过 GDI 进行操作，然后在绘图完成后将其复制回原始格式。

 

 





