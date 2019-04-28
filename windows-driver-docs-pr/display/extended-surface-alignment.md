---
title: 扩展图面对齐
description: 扩展图面对齐
ms.assetid: 3a91a826-7f57-4cad-b236-b41178ac3b17
keywords:
- 绘制扩展 WDK DirectDraw 图面上对齐
- DirectDraw 扩展图面上的对齐方式 WDK Windows 2000 显示
- WDK DirectDraw，扩展对齐方式的图面
- 扩展 WDK DirectDraw 图面上对齐
- 堆 WDK DirectDraw
- 对齐方式扩展的 WDK DirectDraw 图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7517b9a9019df36de76dd60474d2a58705963c8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353352"
---
# <a name="extended-surface-alignment"></a>扩展图面对齐


## <span id="ddk_extended_surface_alignment_gg"></span><span id="DDK_EXTENDED_SURFACE_ALIGNMENT_GG"></span>


Microsoft DirectDraw 支持在每个堆的基础上的图面上的对齐需求。 Microsoft DirectX 5.0 中引入了此支持。 该驱动程序可以指定 X 和 Y 的对齐方式，对于矩形堆和俯仰和线性堆的起始偏移量对齐方式。 这些对齐方式，可以因不同的图面类型而异。

某些显示硬件不能在原子操作中设置它显示开始的偏移量。 在显示周期开始时，就可以为此类硬件驱动程序时仅将值设置到一半的时候闩锁的新显示起始偏移量。 DirectDraw 现在允许指定的可见的后台缓冲区的对齐要求的驱动程序。 某些硬件可能能够表达可能会显示后台缓冲区，以强制要求只有一个注册写入的值的显示开始偏移量的对齐需求。 此技术可以帮助避免否则都是可见的当主表面翻转高频率偶尔闪烁。

 

 





