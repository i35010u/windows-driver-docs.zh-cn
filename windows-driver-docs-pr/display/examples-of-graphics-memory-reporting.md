---
title: 示例图形内存报告
description: 示例图形内存报告
ms.assetid: 3dc0e7ae-db6f-4440-8c9c-7227f409f81f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7eadc4a6ffe397cd7b06a63c7568c8271795371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534528"
---
# <a name="examples-of-graphics-memory-reporting"></a>示例图形内存报告


下面的示例不同的适配器和内存配置为与 Windows XP 的 Windows Vista 报告的数字进行比较。 示例演示**显示**应用程序和 WinSAT 小程序报告的可用内存。

### <a name="span-idexample1256mbdedicatedonboardgraphicsmemoryonadesktopspanspan-idexample1256mbdedicatedonboardgraphicsmemoryonadesktopspanexample-1-256-mb-dedicated-on-board-graphics-memory-on-a-desktop"></a><span id="example_1__256_mb_dedicated_on_board_graphics_memory_on_a_desktop"></span><span id="EXAMPLE_1__256_MB_DEDICATED_ON_BOARD_GRAPHICS_MEMORY_ON_A_DESKTOP"></span>示例 1:在桌面上的 256 MB 专用板载图形内存

以下屏幕截图显示具有 256 MB 的专用集成 （载入） 图形内存的 ATI 离散图形适配器。 ATI 离散图形适配器还会与图形目的的系统内存 (511 MB)。

以下屏幕截图显示通过的可用内存的报表**显示**上 Windows Vista 应用程序。

![windows vista 的屏幕截图显示应用程序](images/reportmem1.png)

下面的屏幕截图显示在 Windows Vista 上通过 WinSAT 小程序的可用内存的报表。

![windows vista 性能信息和工具应用程序的屏幕截图](images/reportmem2.png)

以下屏幕截图显示通过的可用内存的报表**显示**应用程序在 Windows XP 上。

![windows xp 的屏幕截图显示应用程序](images/reportmemxp1.png)

**请注意**  上面的屏幕截图显示了一个"内存大小"数字是只是专用板载图形内存，这不是可用的图形内存总量的准确表示形式。

 

### <a name="span-idexample232mbdedicatedonboardgraphicsmemoryonamobilecomputspanspan-idexample232mbdedicatedonboardgraphicsmemoryonamobilecomputspanexample-2-32-mb-dedicated-on-board-graphics-memory-on-a-mobile-computer"></a><span id="example_2__32_mb_dedicated_on_board_graphics_memory_on_a_mobile_comput"></span><span id="EXAMPLE_2__32_MB_DEDICATED_ON_BOARD_GRAPHICS_MEMORY_ON_A_MOBILE_COMPUT"></span>示例 2:移动计算机上的 32 MB 专用板载图形内存

以下屏幕截图显示在移动计算机中存在的 NVIDIA TurboCache 技术离散适配器。 此适配器都具有一些专用板载图形内存。 但是，适配器大多共享图形目的的系统内存。

以下屏幕截图显示通过的可用内存的报表**显示**上 Windows Vista 应用程序。

![windows vista 的屏幕截图显示应用程序](images/reportmemmob1.png)

下面的屏幕截图显示在 Windows Vista 上通过 WinSAT 小程序的可用内存的报表。

![windows vista 性能信息和工具应用程序的屏幕截图](images/reportmemmob2.png)

以下屏幕截图显示通过的可用内存的报表**显示**应用程序在 Windows XP 上。

![windows xp 的屏幕截图显示应用程序](images/reportmemmobxp1.png)

**请注意**  为 TurboCache 计算机，如在上面的屏幕截图，显示"内存大小"是一个数字组合，但不是总数的专用图形内存，并且共享系统内存。 同样，这不是可用的图形内存总量的准确表示形式。

 

### <a name="span-idexample3256mbsharedgraphicsmemoryonamobilecomputerspanspan-idexample3256mbsharedgraphicsmemoryonamobilecomputerspanexample-3-256-mb-shared-graphics-memory-on-a-mobile-computer"></a><span id="example_3__256_mb_shared_graphics_memory_on_a_mobile_computer"></span><span id="EXAMPLE_3__256_MB_SHARED_GRAPHICS_MEMORY_ON_A_MOBILE_COMPUTER"></span>示例 3:256 MB 的共享移动计算机上的图形内存

以下屏幕截图显示母板有没有专用的图形内存的 Intel UMA （统一内存体系结构） 移动适配器。 相反，该适配器的所有图形目的共享系统内存。

以下屏幕截图显示通过的可用内存的报表**显示**上 Windows Vista 应用程序。

![windows vista 的屏幕截图显示应用程序 ](images/reportmemmob3.png)

下面的屏幕截图显示在 Windows Vista 上通过 WinSAT 小程序的可用内存的报表。

![windows vista 性能信息和工具应用程序的屏幕截图](images/reportmemmob4.png)

以下屏幕截图显示通过的可用内存的报表**显示**应用程序在 Windows XP 上。

![windows xp 的屏幕截图显示应用程序](images/reportmemmobxp2.png)

 

 





