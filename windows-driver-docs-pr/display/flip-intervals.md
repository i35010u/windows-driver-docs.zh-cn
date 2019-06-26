---
title: 交替间隔
description: 交替间隔
ms.assetid: 9372d63c-e2a7-4f70-a4f0-c50df9183f75
keywords:
- 绘图页上翻转 WDK DirectDraw，时间间隔
- DirectDraw 翻转 WDK Windows 2000 显示，时间间隔
- 页翻转 WDK DirectDraw，时间间隔
- 翻转 WDK DirectDraw，时间间隔
- 已发布的投掷 WDK DirectDraw
- 已停用翻转 WDK DirectDraw
- DDCAPS2_FLIPNOVSYNC
- DDCAPS2_FLIPINTERVAL
- DDFLIP_NOVSYNC
- DDFLIP_INTERVAL2
- DDFLIP_INTERVAL3
- DDFLIP_INTERVAL4
- DDERR_WASSTILLDRAWING
- 挂起的翻转 WDK DirectDraw
- 绘制翻转页面 WDK DirectDraw、 计时
- DirectDraw 显示翻转 WDK Windows 2000，计时
- 页面翻转 WDK DirectDraw 计时
- 翻转 WDK DirectDraw、 计时
- 计时翻转 WDK DirectDraw
- 显示 WDK DirectDraw 翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec1adc97d066142edc35ba40ead06b1c85c8629
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385815"
---
# <a name="flip-intervals"></a>交替间隔


## <span id="ddk_flip_intervals_gg"></span><span id="DDK_FLIP_INTERVALS_GG"></span>


DirectDraw 从 DirectX 6.0 开始，添加应用程序可以确定翻转命令执行操作时的功能。 支持这些功能，可以添加到现有的驱动程序，具体取决于硬件功能。

描述计时相关的应用程序的调用时使用了以下术语**翻转**:

<span id="Posted"></span><span id="posted"></span><span id="POSTED"></span>**发布**  
在该应用程序调用的时间**翻转**DirectDraw 调用驱动程序的[ *DdFlip* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)入口点。

<span id="Retired"></span><span id="retired"></span><span id="RETIRED"></span>**已停用**  
硬件开始新的图面中显示的时间得到。

在以前版本的 DirectDraw，投掷了始终停用或其附近垂直同步以下时发布。 使用 DirectX 6.0 和更高版本，应用程序可以指定的翻转停用设备立即，即完全发布时，或在某些设置数垂直同步后发布翻转。 有两个功能位 (DDCAPS2\_FLIPNOVSYNC 和 DDCAPS2\_中的 FLIPINTERVAL [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构) 和四个标志 (DDFLIP\_NOVSYNC，DDFLIP\_INTERVAL2、 DDFLIP\_INTERVAL3 和 DDFLIP\_中的 INTERVAL4 [ **DD\_FLIPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_flipdata)结构) 若要启用这些功能功能。

如果您的驱动程序设置 DDCAPS2\_FLIPNOVSYNC，它接收 DDFLIP\_NOVSYNC 标志**dwFlags** DD 成员\_FLIPDATA 结构。 DDFLIP\_NOVSYNC 标志指示翻转应停用，只要它发布。 但是，在这种情况下，您的硬件必须能够至少在每个扫描行的基础上切换缓冲区。 该驱动程序不应指定支持 DDCAPS2\_FLIPNOVSYNC 如果显示不会实际注销翻转直到下一步的垂直同步，即使驱动程序将立即返回。

末尾的 DDFLIP 数\_INTERVAL2、 DDFLIP\_INTERVAL3 和 DDFLIP\_INTERVAL4 标志表示多少硬件停用已发布之前应等待的垂直同步翻转。 例如，DDFLIP\_INTERVAL2 意味着硬件应计算两个垂直同步，然后停用翻转或其附近的第二个垂直同步。

如果您的驱动程序将公开 DDCAPS2\_FLIPINTERVAL，然后 DirectDraw 放置垂直同步延迟到的最高有效字节，翻转的数字**dwFlags**的成员[ **DD\_FLIPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_flipdata)结构。 因为 DDFLIP\_INTERVAL2、 DDFLIP\_INTERVAL3 和 DDFLIP\_INTERVAL4 标志定义了要将此项，则返回 true，该驱动程序不应作为位标志将这三个标识。 此外，如果该驱动程序将公开 DDCAPS2\_FLIPINTERVAL，DirectDraw 可确保的最高有效字节**dwFlags**时在相应地设置成员 DDFLIP\_INTERVAL2，DDFLIP\_INTERVAL3 和 DDFLIP\_INTERVAL4 标志未设置。 DDFLIP\_NOVSYNC 导致零，无法放置在最高有效字节，并且最高有效字节的默认值将成为一个原因是，调用翻转的默认行为是一旦发布停用翻转或其附近第一个垂直同步。

从 DirectX 1.0 开始，驱动程序要求返回 DDERR\_WASSTILLDRAWING 每当翻转正在等待 （即，当翻转有已发布但尚不支持停用）。 此要求扩展为 flip 的时间间隔。 因为 DDFLIP\_NOVSYNC 投掷将停用时它们会发布，并且因此永远不会挂起，则该驱动程序应永远不会返回 DDERR\_WASSTILLDRAWING 作为此类投掷结果。 相反，使用其中一个 DDFLIP\_INTERVAL2、 DDFLIP\_INTERVAL3 或 DDFLIP\_INTERVAL4 标志意味着该驱动程序必须返回 DDERR\_WASSTILLDRAWING 长的时间，因为段发布和停用翻转之间进行扩展。

DirectDraw 不会阻止与覆盖图面，这些标志使用，但驱动程序不需要遵循它们，即使它们执行设置 DDCAPS2\_FLIPINTERVAL 或 DDCAPS2\_FLIPNOVSYNC 功能位。 驱动程序可以选择遵守覆盖这些标志，如果它们具有的功能，但应用程序不太可能要利用此功能。

**请注意**   DDFLIP\_INTERVAL2、 DDFLIP\_INTERVAL3 和 DDFLIP\_INTERVAL4 标志旨在利用硬件功能。 驱动程序不应尝试通过循环在驱动程序，直到翻转可以停用的请求模拟这些标志。 因为重要的操作系统互斥锁持有调用 DirectDraw 驱动程序时，此类实现可能会影响系统性能。

 

 

 





