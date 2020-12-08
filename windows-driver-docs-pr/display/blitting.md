---
title: 位图传送
description: 位图传送
keywords:
- blt WDK DirectDraw
- 绘制 blt WDK DirectDraw，关于 blitting
- DirectDraw blitting WDK Windows 2000 显示，关于 blitting
- blitting WDK DirectDraw，关于 blitting
- surface DirectDraw，blitting
- 绘制 blt WDK DirectDraw
- DirectDraw blitting WDK Windows 2000 显示
- blitting WDK DirectDraw
- blt WDK DirectDraw，关于 blitting
- DdBlt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0a6ecc11e2d470feabd45a4965f7f6c6c8d2472
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810443"
---
# <a name="blitting"></a>位图传送


## <span id="ddk_blitting_gg"></span><span id="DDK_BLITTING_GG"></span>


如果一个表面发生了 blt，而源区域和目标区域重叠，则必须确定正确的方向，以避免在复制源之前覆盖源的一部分。 只需在表面的对角有两个可能的起点即可实现此目的。 所有 blt 引擎都需要是每个映像的位置和维度。

应执行的所有操作都可以提高实际 blt 的速度。 例如，复制代码段以避免 IF 语句可以使驱动程序更快。 此方法的最佳实现可能是将代码放入一个宏中，并将其用于不同的位置，而不是进行函数调用。 有关详细信息，请参阅 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)。

 

