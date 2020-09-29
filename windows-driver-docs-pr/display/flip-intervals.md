---
title: 交替间隔
description: 交替间隔
ms.assetid: 9372d63c-e2a7-4f70-a4f0-c50df9183f75
keywords:
- 绘图页反向 WDK DirectDraw，时间间隔
- DirectDraw 翻转 WDK Windows 2000 显示，时间间隔
- 页面翻转 WDK DirectDraw，时间间隔
- 翻转 WDK DirectDraw，时间间隔
- 已发布翻转 WDK DirectDraw
- 已停用反向 WDK DirectDraw
- DDCAPS2_FLIPNOVSYNC
- DDCAPS2_FLIPINTERVAL
- DDFLIP_NOVSYNC
- DDFLIP_INTERVAL2
- DDFLIP_INTERVAL3
- DDFLIP_INTERVAL4
- DDERR_WASSTILLDRAWING
- 挂起翻转 WDK DirectDraw
- 绘图页反向 WDK DirectDraw，计时
- DirectDraw 翻转 WDK Windows 2000 显示、计时
- 页面翻转 WDK DirectDraw，计时
- 翻转 WDK DirectDraw，计时
- 计时反向 WDK DirectDraw
- surface DirectDraw，翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1517e430f362cd1b931e60c9c991b46cb44ab26f
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423748"
---
# <a name="flip-intervals"></a>交替间隔


## <span id="ddk_flip_intervals_gg"></span><span id="DDK_FLIP_INTERVALS_GG"></span>


从 DirectX 6.0 开始，DirectDraw 增加了应用程序确定何时执行翻转命令的功能。 根据硬件功能，可以将对这些功能的支持添加到现有的驱动程序中。

在描述与应用程序的 **反向**调用相关的计时时，将使用以下术语：

<span id="Posted"></span><span id="posted"></span><span id="POSTED"></span>**评论**  
应用程序调用 **Flip** 和 DirectDraw 的时间调用驱动程序的 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 入口点。

<span id="Retired"></span><span id="retired"></span><span id="RETIRED"></span>**退休**  
硬件从新表面开始显示的时间。

在以前版本的 DirectDraw 中，翻转始终在发布时，或接近垂直同步。 在 DirectX 6.0 和更高版本中，应用程序可以指定翻转立即停用，即，精确地发布时，或在发布反向后，按一定数量设置垂直同步。 DDCORECAPS 结构) 有两个功能位 (DDCAPS2 FLIPNOVSYNC 和 DDCAPS2 FLIPINTERVAL， (DDFLIP NOVSYNC、DDFLIP INTERVAL2、DDFLIP INTERVAL3、DDFLIP INTERVAL4、FLIPDATA、、、、、 \_ \_ [**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-ddcorecaps) \_ \_ \_ 和 \_) 。 [** \_ **](/windows/win32/api/ddrawint/ns-ddrawint-dd_flipdata)

如果驱动程序设置 DDCAPS2 \_ FLIPNOVSYNC，它将 \_ 在 DD dwFlags 结构的 **FLIPDATA** 成员中收到 DDFLIP NOVSYNC 标志 \_ 。 DDFLIP \_ NOVSYNC 标志指示翻转应在发布后立即停用。 但是，在这种情况下，你的硬件必须能够在至少每个扫描行的基础上切换缓冲区。 \_如果在下一垂直同步之前，即使驱动程序立即返回，驱动程序也不应为 DDCAPS2 FLIPNOVSYNC 指定支持。

DDFLIP \_ INTERVAL2、DDFLIP \_ INTERVAL3 和 DDFLIP INTERVAL4 标志末尾的数字 \_ 表示在停用已发布的翻转之前，该硬件应等待多少垂直同步。 例如，DDFLIP \_ INTERVAL2 表示硬件应计算两个垂直同步，然后停用或接近第二个垂直同步。

如果驱动程序公开 DDCAPS2 \_ FLIPINTERVAL，则 DirectDraw 会将垂直同步的数目延迟为延迟翻转，并将其放入[**DD \_ FLIPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_flipdata)结构的**dwFlags**成员的最高有效字节。 由于定义了 DDFLIP \_ INTERVAL2、DDFLIP \_ INTERVAL3 和 DDFLIP \_ INTERVAL4 标志来实现此 true，因此驱动程序不应将这三个标志视为位标志。 此外，如果驱动程序公开 DDCAPS2 \_ FLIPINTERVAL，DirectDraw 将确保在**dwFlags** \_ 未设置 DDFLIP INTERVAL2、DDFLIP \_ INTERVAL3 和 DDFLIP INTERVAL4 标志时，对 dwFlags 成员的最高有效字节进行相应的设置 \_ 。 DDFLIP \_ NOVSYNC 导致将零置于最有效的字节中，最高有效字节的默认值将变为一，因为反向调用的默认行为是在其发布后停用或接近第一个垂直同步。

从 DirectX 1.0 开始，每当 DDERR 翻转时，驱动程序都需要返回 \_ WASSTILLDRAWING (也就是说，翻转已发布但尚未停用) 。 此要求在反向间隔内进行扩展。 由于 DDFLIP \_ NOVSYNC 翻转在发布后将被停用，因而永远不会等待，因此，驱动程序绝不应返回 DDERR \_ WASSTILLDRAWING 作为此类反向的结果。 相反，使用其中一个 DDFLIP \_ INTERVAL2、DDFLIP \_ INTERVAL3 或 DDFLIP \_ INTERVAL4 标志意味着驱动程序需要 \_ 长时间返回 DDERR WASSTILLDRAWING，因为发布和停用之间的时间段会进行扩展。

DirectDraw 不会阻止将这些标志与覆盖曲面一起使用，但不需要驱动程序对它们进行处理，即使它们确实设置了 DDCAPS2 \_ FLIPINTERVAL 或 DDCAPS2 \_ FLIPNOVSYNC 功能位。 如果驱动程序有功能，驱动程序可能会选择使用这些标志来进行覆盖，但应用程序不太可能利用此功能。

**注意**   DDFLIP \_ INTERVAL2、DDFLIP \_ INTERVAL3 和 DDFLIP \_ INTERVAL4 标志旨在利用硬件功能。 驱动程序不应尝试通过在驱动程序中循环来模拟这些标志，直到可以根据请求停用。 由于在调用 DirectDraw 驱动程序时保持重要的操作系统互斥体，因此此类实现可能会影响系统性能。

 

 

