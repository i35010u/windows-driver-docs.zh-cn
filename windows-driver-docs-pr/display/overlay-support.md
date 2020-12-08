---
title: 覆盖支持
description: 覆盖支持
keywords:
- 绘图页反向 WDK DirectDraw，覆盖面
- DirectDraw 翻转 WDK Windows 2000 显示，覆盖面
- 页面翻转 WDK DirectDraw，覆盖面
- 翻转 WDK DirectDraw，覆盖面
- 覆盖面 WDK DirectDraw
- 表面 WDK DirectDraw，覆盖
- surface DirectDraw，翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3ea75d59b65888718aca2d95c9a42c4a705cf75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813793"
---
# <a name="overlay-support"></a>覆盖支持


## <span id="ddk_overlay_support_gg"></span><span id="DDK_OVERLAY_SUPPORT_GG"></span>


DirectDraw 还支持覆盖。 *覆盖面* 是指可以在主表面上显示的曲面，而不会更改其下表面的物理位。 对于叠加，会设置在包含覆盖图面的主图面上定义矩形的寄存器。 数字到模拟转换器 (DAC) 更改矩形的位置。 扫描行读取主表面内存中的数据，直到到达为覆盖设置的矩形。 它从覆盖面中读取，直到覆盖区中的那一行完成，然后再继续执行原始的主表面图像。 这种从主表面切换到叠加，并在每次扫描行时进行切换，然后继续，直到覆盖完全显示为止。

覆盖面可以与主表面具有不同的像素深度。 例如，虽然8位/像素 (bpp) 对于主要表面可能看起来很正常，但视频剪辑可能需要 16 bpp 才能显示可接受。 像素深度在主要表面与覆盖区之间无缝切换。 有关带有 DirectDraw 的覆盖的详细信息，请参阅 [视频端口扩展到 DirectX](video-port-extensions-to-directx.md) 部分。

叠加翻转的方式与主表面完全相同。 DirectDraw surface 对象交换指针，以便在扫描行到达边界覆盖的矩形时，读取新的覆盖图面。 [计时反向](timing-a-flip.md)所述的相同翻转算法会阻止撕裂。

 

 





