---
title: 运动补偿
description: 运动补偿
keywords:
- 绘制 WDK DirectDraw，运动补偿
- DirectDraw WDK Windows 2000 显示，动作补偿
- 运动补偿 WDK
- 压缩的视频解码 WDK DirectDraw
- 视频解码 WDK DirectDraw
- 解码 WDK DirectDraw
- 数字视频解码 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5abddc601e74b22c128313783ac8a0cee68ca1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839593"
---
# <a name="motion-compensation"></a>运动补偿


## <span id="ddk_motion_compensation_gg"></span><span id="DDK_MOTION_COMPENSATION_GG"></span>


运动补偿是用于压缩数字视频解码过程的重要阶段的一项术语。 许多图形加速器设备都提供了一种加速功能，支持压缩的视频解码。 由于运动补偿过程是视频解码最常见的支持部分，因此，支持压缩视频解码的设备驱动程序接口称为运动补偿 DDI。 除了运动补偿，某些设备还可以执行 IDCT (反离散的余弦转换) 以及软件视频解码器可用于加速解码过程的其他硬件功能。 运动补偿 DDI 的灵活性足以处理同时提供这些其他功能的设备。

已正确定义软件 MPEG 解码器的输入数据。 如果解码器是为 MPEG-2 设计的，则输入采用 MPEG-2 格式。 解码器的输出也是定义完善的。 它是采用各种格式的未压缩帧。 不过，软件解码器与显示设备之间的过渡格式定义不完善，有许多设备需要其自己的专有数据格式。 因此，运动补偿设备驱动程序接口非常灵活，并且临时格式被描述为 Guid。 显示驱动程序报告表示其支持的功能的 Guid，软件解码器选择最符合其要求的 GUID。

若要启用动作补偿功能，驱动程序必须执行以下步骤：

-   在调用 [**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo)时，实现 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数并将 [**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构的 **GetDriverInfo** 成员设置为指向此函数。 驱动程序的 *DdGetDriverInfo* 函数必须分析 GUID \_ MotionCompCallbacks guid。

-   使用 GUID MOTIONCOMPCALLBACKS GUID 调用 *DdGetDriverInfo* 函数时，使用适当的驱动程序回调指针和回调类型标志来填充 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构 \_ 。 然后，该驱动程序必须将此初始化的结构复制到 Microsoft DirectDraw 分配的缓冲区，该缓冲区中 [**DD \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)结构的 **lpvData** 成员指向的位置，并返回写入缓冲区的 **dwActualSize** 中的字节数。

 

