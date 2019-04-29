---
title: GDI 托管属性画笔
description: GDI 托管属性画笔
ms.assetid: 8ca38ba1-824d-45be-9039-13222d3400c3
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 呈现引擎 WDK GDI
- GDI WDK Windows 2000 显示模式
- 图形驱动程序 WDK Windows 2000 显示模式
- WDK GDI 模式
- 画笔 WDK GDI
- 意识到 WDK GDI 画笔
- 绘制 WDK GDI，画笔
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57544d900f40aaf1a09b69a958edcd86ae9b04e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363795"
---
# <a name="gdi-managed-attributes-brushes"></a>GDI 管理的属性：画笔


## <span id="ddk_gdi_managed_attributes_brushes_gg"></span><span id="DDK_GDI_MANAGED_ATTRIBUTES_BRUSHES_GG"></span>


GDI 还可管理的所有属性。 GDI 将属性传递给驱动程序用作画笔;该驱动程序*意识到*这些画笔通过将它们转换为有用的内部格式。 GDI 维护驱动程序的此转换的信息。 GDI 还维护的所有状态的画笔，包括边界、 关联、 当前的位置和线条样式。 驱动程序可以缓存的信息，但未假定维护任何状态。 初始化和画笔实现，除了 GDI 调用驱动程序仅在设备上进行绘制。 GDI 负责的转换，区域锁定，并*指针排除*调用驱动程序之前。

每当一个驱动程序需要使用画笔尚未意识到，它可以回拨到 GDI。 GDI 画笔分配内存，并调用要意识到这一点，如有必要，抖动它的驱动程序。

 

 





