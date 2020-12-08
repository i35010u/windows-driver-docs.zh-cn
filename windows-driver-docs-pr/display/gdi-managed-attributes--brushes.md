---
title: GDI-Managed 属性画笔
description: GDI-Managed 属性画笔
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 渲染引擎 WDK GDI
- GDI WDK Windows 2000 显示，模式
- 图形驱动程序 WDK Windows 2000 显示，模式
- 模式 WDK GDI
- 画笔 WDK GDI
- 实现画笔 WDK GDI
- 绘制 WDK GDI，画笔
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d16a7e38feb0734ca00526ff4e344e8898492058
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783263"
---
# <a name="gdi-managed-attributes-brushes"></a>GDI 管理的属性：画笔


## <span id="ddk_gdi_managed_attributes_brushes_gg"></span><span id="DDK_GDI_MANAGED_ATTRIBUTES_BRUSHES_GG"></span>


GDI 还管理所有属性。 GDI 将属性作为画笔传递给驱动程序; *驱动程序* 通过将这些画笔转换为有用的内部形式来将其识别出来。 GDI 将为驱动程序保留这一转换后的信息。 GDI 还会保留画笔的所有状态，包括边界、相关、当前位置和线条样式。 驱动程序可以缓存信息，但不会将其视为维护任何状态。 除初始化和画笔实现外，GDI 仅调用驱动程序以在设备上进行绘制。 GDI 在调用驱动程序之前，会对转换、区域锁定和 *指针排除* 进行处理。

每当驱动程序需要使用尚未实现的画笔时，它都会回调到 GDI。 GDI 为画笔分配内存，并调用驱动程序来实现它，如有必要，请仿色。

 

 





