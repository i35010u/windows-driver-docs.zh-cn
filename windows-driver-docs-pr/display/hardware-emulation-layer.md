---
title: 硬件仿真层
description: 硬件仿真层
keywords:
- 绘制 WDK DirectDraw，硬件仿真层
- DirectDraw WDK Windows 2000 显示，硬件仿真层
- 硬件仿真层 WDK DirectDraw
- HEL WDK DirectDraw
- 仿真 WDK DirectDraw
- 透明 blts WDK DirectDraw
- 功能位 WDK DirectDraw
- cap bits WDK DirectDraw
- 表面 WDK DirectDraw，功能位
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24f7c51d964fb0b4361d20736f75a2f8c8bb2db8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830665"
---
# <a name="hardware-emulation-layer"></a>硬件仿真层


## <span id="ddk_hardware_emulation_layer_gg"></span><span id="DDK_HARDWARE_EMULATION_LAYER_GG"></span>


DirectDraw 硬件仿真层 (HEL) 执行 DirectDraw 驱动程序的仿真。 HEL 作为 DirectDraw 的一部分写入的 () 在用户模式下执行此仿真。

例如，如果 DirectDraw 驱动程序具有 (*cap*) 设置为 blts 的位，而不是透明的 blts，则会为 blts 和用于透明 BLTS 的 HEL 调用 DirectDraw 驱动程序。 如果是透明的 blt，则会向 HEL 传递显示内存指针，并将每个字节从一个后备面到颜色键进行比较。 如果字节与颜色键不匹配，则 HEL 会将其复制到使用 CPU 的目标表面。 对于其他不受支持的操作也会发生此模拟，或者卡显示内存不足的情况。

DirectDraw 不会将失败的 DirectDraw 驱动程序操作传递到 HEL。 如果 HEL 或 DirectDraw 驱动程序未能满足特定操作，则会将错误代码返回到应用程序。

 

 





