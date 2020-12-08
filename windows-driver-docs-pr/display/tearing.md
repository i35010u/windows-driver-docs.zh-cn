---
title: 解除
description: 解除
keywords:
- 泪水 WDK DirectDraw
- 绘图页翻转 WDK DirectDraw，撕裂
- DirectDraw 翻转 WDK Windows 2000 显示，撕裂
- 页面翻转 WDK DirectDraw，撕裂
- 翻转 WDK DirectDraw，撕裂
- surface DirectDraw，翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df327400f92a75e4041460506eeef451c827f7ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839575"
---
# <a name="tearing"></a>解除


## <span id="ddk_tearing_gg"></span><span id="DDK_TEARING_GG"></span>


如 " [翻转](flipping.md) " 一节中所述，翻转实质上是更改内存指针，使其指向显示内存的新区域 (参阅 Permedia2 示例代码) 。 要翻转的表面必须已完成显示，然后应用程序才能锁定、blt 或更改该内存，或者可能产生 (，如下图所示) 。

![说明撕裂和无撕裂的示意图](images/ddfig8.png)

如果要翻转到的图面在反向时向其中写入数据，则也可能会出现一种情况。 撕裂是通用的，可能会在同一时间同时绘制和显示图像。 帧速度越快，就不能解决此问题。 由于主表面、叠加和纹理均为 DirectDraw 表面，因此可以通过相同的方式翻转它们来防止撕裂。

当页翻转或 blt 在错误的时间发生时，会发生一种撕。 例如，如果页面翻转，而监视器扫描线条处于显示图面（如上图中的虚线所示），则会出现一条撕。 只有在显示了整个表面后，才可以使用此方法进行切换， (如图) 的示例中所示。 当 blitting 正在显示的图面上时，也会发生一种情况。

 

 





