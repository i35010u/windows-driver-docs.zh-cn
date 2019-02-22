---
title: 覆盖支持
description: 覆盖支持
ms.assetid: 325a08b2-c357-49b7-a9c3-878c44bc2d26
keywords:
- 绘图页上翻转 WDK DirectDraw，覆盖面
- DirectDraw 翻转 WDK Windows 2000 显示覆盖图面
- 页面翻转 WDK DirectDraw，覆盖面
- 翻转 WDK DirectDraw，覆盖面
- 覆盖面 WDK DirectDraw
- WDK DirectDraw 表面覆盖
- 显示 WDK DirectDraw 翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bfb67c70958b55682303b6bc4b7e723d9eb6e68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547916"
---
# <a name="overlay-support"></a>覆盖支持


## <span id="ddk_overlay_support_gg"></span><span id="DDK_OVERLAY_SUPPORT_GG"></span>


DirectDraw 还支持覆盖层。 *覆盖面*是指可以在顶部显示主面而不会改变其下面的图面中的物理位。 使用一个覆盖区，寄存器是设置包含覆盖面主图面上定义一个矩形。 矩形的位置更改为数字模拟转换器 (DAC)。 扫描行读取主图面上的内存中的数据，直到它达到留出供在覆盖区上的矩形。 它从覆盖面读取直到该行在覆盖层中的已完成，然后继续在原始主图面上的映像。 这主图面中切换到在覆盖区上并返回上扫描行的每个阶段发生的情况并将继续，直到完全显示在覆盖区。

覆盖面可以具有与主表面的不同的像素深度。 例如，虽然 8 位 / 像素 (bpp) 可能看起来相当不错的主图面，视频剪辑可能需要以接受显示的 16 bpp。 像素深度主表面和覆盖层之间无缝切换。 有关使用 DirectDraw 叠加的详细信息，请参阅[DirectX 的视频端口扩展](video-port-extensions-to-directx.md)部分。

覆盖翻转方式与主表面完全相同。 DirectDraw 图面上对象交换指针，以便在新的覆盖面读取扫描线在到达边界在覆盖区上的矩形。 相同的翻转算法中所述[计时翻转](timing-a-flip.md)阻止撕裂现象。

 

 





