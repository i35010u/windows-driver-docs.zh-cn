---
title: 图形内存报告示例
description: 图形内存报告示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf352c0d5350c411845469bfa9df492eda26507e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838313"
---
# <a name="examples-of-graphics-memory-reporting"></a>图形内存报告示例


下面的示例对 Windows Vista 与 Windows XP 上的不同适配器和内存配置报告的数字进行比较。 示例显示了 **显示** 应用程序以及 WinSAT 小程序的可用内存报告。

### <a name="span-idexample_1__256_mb_dedicated_on_board_graphics_memory_on_a_desktopspanspan-idexample_1__256_mb_dedicated_on_board_graphics_memory_on_a_desktopspanexample-1-256-mb-dedicated-on-board-graphics-memory-on-a-desktop"></a><span id="example_1__256_mb_dedicated_on_board_graphics_memory_on_a_desktop"></span><span id="EXAMPLE_1__256_MB_DEDICATED_ON_BOARD_GRAPHICS_MEMORY_ON_A_DESKTOP"></span>示例 1: 256-MB 专用板载图形内存在桌面上

以下屏幕截图显示了一个 ATI 离散图形适配器，该适配器具有 256 MB 专用集成 (板载) 图形内存。 为了图形目的，ATI 离散图形适配器还共享系统内存 (511 MB) 。

以下屏幕截图显示通过 Windows Vista 上的 **显示** 应用程序显示的可用内存的报表。

![显示 "显示" 窗口并选中 "适配器" 选项卡的屏幕截图。](images/reportmem1.png)

以下屏幕截图显示了通过 Windows Vista 上的 WinSAT 小程序提供的内存的报告。

![屏幕截图显示 "性能信息和工具"，其中显示了 "图形" 信息。](images/reportmem2.png)

以下屏幕截图显示通过 Windows XP 上的显示应用程序 **显示** 的可用内存的报表。

![屏幕截图，显示 "显示" 应用，其中包含在 Windows XP 中选择的 "适配器" 选项卡。](images/reportmemxp1.png)

**注意**   前面的屏幕截图所示的单个 "内存大小" 数字只是专用的板上图形内存，不是可用图形内存总量的准确表示。

 

### <a name="span-idexample_2__32_mb_dedicated_on_board_graphics_memory_on_a_mobile_computspanspan-idexample_2__32_mb_dedicated_on_board_graphics_memory_on_a_mobile_computspanexample-2-32-mb-dedicated-on-board-graphics-memory-on-a-mobile-computer"></a><span id="example_2__32_mb_dedicated_on_board_graphics_memory_on_a_mobile_comput"></span><span id="EXAMPLE_2__32_MB_DEDICATED_ON_BOARD_GRAPHICS_MEMORY_ON_A_MOBILE_COMPUT"></span>示例 2:32-移动计算机上的专用板载显存示例

以下屏幕截图显示了在移动计算机中存在的 NVIDIA TurboCache 技术离散适配器。 此适配器有一些专用的板上图形内存。 但是，适配器主要出于图形目的共享系统内存。

以下屏幕截图显示通过 Windows Vista 上的 **显示** 应用程序显示的可用内存的报表。

![windows vista 显示应用程序的屏幕截图](images/reportmemmob1.png)

以下屏幕截图显示了通过 Windows Vista 上的 WinSAT 小程序提供的内存的报告。

![windows vista 性能信息和工具应用程序的屏幕截图](images/reportmemmob2.png)

以下屏幕截图显示通过 Windows XP 上的显示应用程序 **显示** 的可用内存的报表。

![windows xp 显示应用程序的屏幕截图](images/reportmemmobxp1.png)

**注意**   对于 TurboCache 计算机（如上述屏幕截图所示），单个 "内存大小" 数字是专用图形内存和共享系统内存的组合，但不是总大小。 同样，这并不是可用图形内存总量的准确表示。

 

### <a name="span-idexample_3__256_mb_shared_graphics_memory_on_a_mobile_computerspanspan-idexample_3__256_mb_shared_graphics_memory_on_a_mobile_computerspanexample-3-256-mb-shared-graphics-memory-on-a-mobile-computer"></a><span id="example_3__256_mb_shared_graphics_memory_on_a_mobile_computer"></span><span id="EXAMPLE_3__256_MB_SHARED_GRAPHICS_MEMORY_ON_A_MOBILE_COMPUTER"></span>示例 3: 256-MB 共享图形内存在移动计算机上

以下屏幕截图显示了 Intel UMA (统一内存体系结构) 移动适配器，该适配器在主板上没有专用显存。 适配器会出于所有图形目的共享系统内存。

以下屏幕截图显示通过 Windows Vista 上的 **显示** 应用程序显示的可用内存的报表。

![屏幕截图显示 "显示" 窗口，其中选择了 "适配器" 选项卡和 256 M B 的可用内存。](images/reportmemmob3.png)

以下屏幕截图显示了通过 Windows Vista 上的 WinSAT 小程序提供的内存的报告。

![屏幕截图，显示 WinSAT 小程序中的 "性能信息和工具"，其中显示了 "图形" 信息。](images/reportmemmob4.png)

以下屏幕截图显示通过 Windows XP 上的显示应用程序 **显示** 的可用内存的报表。

![屏幕截图，显示 "显示" 应用程序，并选中 "适配器" 选项卡和 128 M B 内存。](images/reportmemmobxp2.png)

 

 





