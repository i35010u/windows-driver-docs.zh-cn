---
title: 采用状态信息的驱动程序
description: 采用状态信息的驱动程序
keywords:
- surface DirectDraw，blitting
- 绘制 blt WDK DirectDraw，状态信息
- DirectDraw blitting WDK Windows 2000 显示，状态信息
- blitting WDK DirectDraw，状态信息
- blt WDK DirectDraw，状态信息
- 状态 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c41639509a939cf2a7d6a58f98b2165c062ef2a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809119"
---
# <a name="drivers-that-assume-state-information"></a>采用状态信息的驱动程序


## <span id="ddk_drivers_that_assume_state_information_gg"></span><span id="DDK_DRIVERS_THAT_ASSUME_STATE_INFORMATION_GG"></span>


大多数显示驱动程序在执行操作时都设置 blitter 的状态。 但是，某些显示驱动程序希望 blitter 处于已知状态。 例如，某些显示驱动程序假定源设置为执行标准 blt 而不是透明 blt，依此类推。 在这些情况下，在 DirectDraw 使用状态之后，必须重置状态。

可以通过固定原点或为源和目标曲面使用单独原点来完成两个曲面之间的 Blts。 如果显示驱动程序要求源保持不变，并且 DirectDraw 将其更改为访问辅助图面，则必须在完成操作后保存和还原旧指针。

如果这会强制 DirectDraw 等待操作完成，使其可以将寄存器还原到其以前的状态，则性能会受到影响。 这是因为 DirectDraw 的速度是异步的。

在这些情况下，必须小心，以最大程度地减少对显示状态所做的更改。 在这种情况下移动源还会浪费堆栈上的空间，该空间可用于传递参数。

 

 





