---
title: 假定的状态信息的驱动程序
description: 假定的状态信息的驱动程序
ms.assetid: c4dfb701-c547-4e94-8fd8-05571508137c
keywords:
- WDK DirectDraw 图阵的图面
- 绘制 blt WDK DirectDraw，状态信息
- DirectDraw 图阵 WDK Windows 2000 显示，状态信息
- 平面闪 WDK DirectDraw，状态信息
- blt WDK DirectDraw，状态信息
- 指出 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8389c49c4763282bb684e23e66a320e30bf3a0e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543151"
---
# <a name="drivers-that-assume-state-information"></a>假定的状态信息的驱动程序


## <span id="ddk_drivers_that_assume_state_information_gg"></span><span id="DDK_DRIVERS_THAT_ASSUME_STATE_INFORMATION_GG"></span>


大多数显示驱动程序设置 blitter 的状态，当他们做的操作。 但是，某些显示驱动程序希望 blitter 处于已知状态。 例如，某些显示驱动程序假定源设置为执行标准 blt 而不是透明的 blt，依次类推。 在这些情况下，必须在后 DirectDraw 将其重置状态。

具有固定的起始位置或具有单独的起始位置的源和目标的图面，可以完成 Blts 之间两个图面。 如果显示驱动程序需要其保持不变，并将其以访问辅助面 DirectDraw 更改，必须保存并在操作完成时，还原旧的指针。

如果这会强制 DirectDraw 等待操作可以被完成，因此它可以还原到其以前的状态的寄存器，性能将受到影响。 这是因为正在异步来自 DirectDraw 的速度。

在这些情况下必须格外小心，以最小化到的显示状态所做的更改。 在此方案中移动源还可能要使用用于将参数传递到堆栈上浪费空间。

 

 





