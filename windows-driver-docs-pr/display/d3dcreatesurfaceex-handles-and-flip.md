---
title: D3dCreateSurfaceEx 句柄和交替
description: D3dCreateSurfaceEx 句柄和交替
ms.assetid: b87762fd-444d-437a-b076-189f51cc6dd1
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 翻转 WDK Direct3D
- DdFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d2fb024d700610bdd7ac6423f41444ac23f53b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371504"
---
# <a name="d3dcreatesurfaceex-handles-and-flip"></a>D3dCreateSurfaceEx 句柄和交替


## <span id="ddk_d3dcreatesurfaceex_handles_and_flip_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_FLIP_GG"></span>


DirectDraw 图面上结构旨在表示概念图面，视频内存中不一定是特定位置。 这种抽象的主要用法是在主要的翻转链，其中应用程序使用一个常量的图面上对象来表示后台缓冲区，即使后台缓冲区可能是围绕为视频内存中移动[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)函数。

[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)函数采用一个环图面，并按顺序重新分配此通道周围的视频内存指针。 在两个图面上对象的特定情况下，该过程减少到贸易的视频内存指针。 此外，DirectDraw 运行时还会轮换[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)每个面和驱动程序拥有的内容与关联句柄**dwReserved1**每个面上的成员。 此行为具有一些有趣结果的 DirectX 7.0 驱动程序，并有效地出指向 DirectDraw 图面上结构内部的驱动程序自己的图面上结构的指针的嵌入的规则。

考虑两个图面上，A 和 B 的对象具有关联的句柄 H<sub>A</sub>和高<sub>B</sub>，并**fpVidMem** (隶属[ **DD\_面\_GLOBAL** ](https://msdn.microsoft.com/library/windows/hardware/ff551726)结构) 的 F 值<sub>一个</sub>和 F<sub>B</sub>。 此外，假设应用程序使用图面上结构 A 来指代翻转链的后台缓冲区。 在[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)时，句柄**fpVidMem**值将交换，因此该图面上一个具有 H<sub>B</sub>和 F<sub>B</sub>，和面 B 具有 H<sub>A</sub>和 F<sub>A</sub>。 现在，应用程序尝试绘制到后台缓冲区，出现 A，应当为 F 的视频内存<sub>B</sub> (因为该应用程序启动对调用*DdFlip*)。

绘制命令颁发给驱动程序，它会查找与该图面关联的句柄 (即现在 H<sub>B</sub>，不是小时<sub>A</sub>)。 如果该驱动程序只是将存储指向 DirectDraw 图面上结构的指针，则会发生什么情况？ 该驱动程序查找 H<sub>B</sub>，然后遵循存储的指针到图面 B，现在具有**fpVidMem** F 的值<sub>一个</sub>。 在 F 的视频内存开始绘制<sub>A</sub>。 这是不什么应用程序需要。 如果手动，驱动程序将图面上的数据存储在其自己的结构，而不是遵循指针到 DirectDraw 图面结构，然后 H<sub>B</sub>仍将解析为 F<sub>B</sub>，并且上出现了绘图正确的图面。 这后一种情况下是当前 DDI 的实现的方式。

 

 





