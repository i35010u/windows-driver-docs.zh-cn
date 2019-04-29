---
title: 设置呈现交换间隔
description: 设置呈现交换间隔
ms.assetid: 01626dbc-d7ac-482a-a07e-0f5ee3ffb05f
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，请报告功能
- D3DCAPS8
- 演示文稿交换间隔 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 805203a2b95eef4894411d6ac44becd1b5522dfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390445"
---
# <a name="setting-presentation-swap-intervals"></a>设置呈现交换间隔


## <span id="ddk_setting_presentation_swap_intervals_gg"></span><span id="DDK_SETTING_PRESENTATION_SWAP_INTERVALS_GG"></span>


驱动程序应始终将设置**PresentationIntervals**为零报告其 Direct3D 硬件的功能时 D3DCAPS8 结构中的成员。 然后，运行时将分配的 D3DPRESENT\_间隔\_为默认值。 此外，运行时分配以下演示文稿交换时间间隔，具体取决于驱动程序是如何指定功能中的位**Caps2** D3DCAPS8 的成员：

-   如果该驱动程序指定 DDCAPS2\_FLIPNOVSYNC 位，运行时还会设置**PresentationIntervals**到 D3DPRESENT\_间隔\_即时。

-   如果该驱动程序指定 DDCAPS2\_FLIPINTERVAL 位，运行时还会设置**PresentationIntervals**到 D3DPRESENT\_间隔\_两个，D3DPRESENT\_间隔\_三种类型和 D3DPRESENT\_间隔\_四个。

 

 





