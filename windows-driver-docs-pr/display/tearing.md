---
title: 撕裂现象
description: 撕裂现象
ms.assetid: b4c21592-cbdf-4dd6-9457-71d53b9f7b32
keywords:
- 消除 WDK DirectDraw
- 绘制翻转页面 WDK DirectDraw、 撕裂现象
- DirectDraw 翻转 WDK Windows 2000 显示、 撕裂现象
- 页翻转 WDK DirectDraw、 撕裂现象
- 翻转 WDK DirectDraw、 撕裂现象
- 显示 WDK DirectDraw 翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3108ef2a8f3125ed4faf83f41fbefc56c7cf114f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526451"
---
# <a name="tearing"></a>撕裂现象


## <span id="ddk_tearing_gg"></span><span id="DDK_TEARING_GG"></span>


如中所述[Flipping](flipping.md)部分中，翻转实质上是更改的内存指针，以使其指向到新的显示内存区域 （请参阅 Permedia2 示例代码）。 必须是正在离开翻转的面完成应用程序可以锁定 blt，或更改该内存，或 （如在下图中所示），可能会导致拆解之前显示。

![关系图阐释撕裂现象和不撕裂现象](images/ddfig8.png)

在翻转到图面出现在翻转期间写入的数据，也可能出现拆解。 撕裂现象是通用，可能会发生任何时候，只要映像是会绘制并显示在同一时间。 更快的帧速率不解决此问题。 主图面、 覆盖和纹理是所有 DirectDraw 图面，因为它们可以翻转的相同方式以防止脱节。

拆解翻页或发生 blt 发生在错误的时间。 例如，如果页面翻转而监视器扫描行是中间显示图面上，由在上图中的虚线表示，会发生拆解。 计时反向地 （较低如示例所示的图） 中显示的整个图面后，才会发生，可以避免拆解。 在的过程中显示的平面闪到图面，也可能发生拆解。

 

 





