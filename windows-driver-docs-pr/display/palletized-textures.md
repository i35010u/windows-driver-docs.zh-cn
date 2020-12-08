---
title: 堆砌纹理
description: 堆砌纹理
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，托盘化纹理
- 纹理 WDK DirectX 8。0
- 托盘化纹理 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36f699061e4e8dfb82e2382f181fc1f3a803159e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841267"
---
# <a name="palletized-textures"></a>堆砌纹理


## <span id="ddk_palettized_textures_gg"></span><span id="DDK_PALETTIZED_TEXTURES_GG"></span>


尽管托盘化纹理的 API 支持已针对 DirectX 8.0 进行了更改，但这不会反映在 DDI 中。 将继续使用现有的基于调色板的 DP2 令牌通知调色板和调色板之间的绑定的驱动程序。

不能假定它是因为 surface 和调色板之间的关联已与 D3DDP2OP \_ SETPALETTE 建立，surface 结构的 **lpPalette** 字段指向有效调色板。 调色板和由 DP2 流建立的图面之间的关联不会反映在实际的表面和调色板数据结构中。

此外，不会为这些调色板调用 DirectDraw 的调色板 DDI 入口点。 纹理调色板操作的所有 DDI 通知都通过 DP2 流完成。

 

 





