---
title: 硬件仿真层
description: 硬件仿真层
ms.assetid: 79ca4e7f-f335-4e71-8abb-811d98976cc9
keywords:
- 绘制 WDK DirectDraw，硬件仿真层
- DirectDraw WDK Windows 2000 显示，硬件仿真层
- 硬件仿真层 WDK DirectDraw
- HEL WDK DirectDraw
- 仿真 WDK DirectDraw
- 透明 blts WDK DirectDraw
- 功能的位将 WDK DirectDraw
- 限制 bits WDK DirectDraw
- 显示 WDK DirectDraw，功能位
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6030bbe421152dad292196fadfff694bc6a5342f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541880"
---
# <a name="hardware-emulation-layer"></a>硬件仿真层


## <span id="ddk_hardware_emulation_layer_gg"></span><span id="DDK_HARDWARE_EMULATION_LAYER_GG"></span>


DirectDraw 硬件仿真层 (HEL) 执行仿真 DirectDraw 驱动程序。 （由 Microsoft 编写 DirectDraw 的一部分） HEL 在用户模式下执行这种模拟。

例如，如果 DirectDraw 驱动程序具有功能 (*caps*) 位设置为 blts 但不是为透明 blts DirectDraw 驱动程序将其称为 blts 和透明 blts HEL。 对于透明 blt HEL 传递显示内存指针，它将支持图面中每个字节设置为的颜色键进行比较。 如果字节不匹配的颜色键，HEL 将其复制到使用 CPU 目标图面。 对于其他不受支持的操作也会发生这种模拟或卡是否显示内存不足。

DirectDraw HEL 到未通过失败的 DirectDraw 驱动程序操作。 如果 HEL 或 DirectDraw 驱动程序失败的特定操作，错误代码返回到应用程序。

 

 





