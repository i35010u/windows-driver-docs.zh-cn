---
title: 设置呈现交换间隔
description: 设置呈现交换间隔
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，报告功能
- D3DCAPS8
- 演示交换间隔 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a16411bf76bf78bfa0397db87ddbb77c9d1e65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826593"
---
# <a name="setting-presentation-swap-intervals"></a>设置呈现交换间隔


## <span id="ddk_setting_presentation_swap_intervals_gg"></span><span id="DDK_SETTING_PRESENTATION_SWAP_INTERVALS_GG"></span>


当驱动程序报告其 Direct3D 硬件的功能时，该驱动程序应始终将 D3DCAPS8 结构的 **PresentationIntervals** 成员设置为零。 然后，运行时将 D3DPRESENT \_ 时间间隔指定 \_ 为默认值。 此外，运行时根据驱动程序在 D3DCAPS8 的 **Caps2** 成员中指定功能位的方式，分配以下表示交换间隔：

-   如果驱动程序指定 DDCAPS2 \_ FLIPNOVSYNC 位，则运行时还会将 **PresentationIntervals** 设置为 " \_ 立即" \_ 。

-   如果驱动程序指定 DDCAPS2 \_ FLIPINTERVAL 位，则运行时还会将 **PresentationIntervals** 设置为 D3DPRESENT \_ INTERVAL \_ 2、D3DPRESENT \_ interval \_ 3 和 D3DPRESENT \_ interval \_ 4。

 

 





