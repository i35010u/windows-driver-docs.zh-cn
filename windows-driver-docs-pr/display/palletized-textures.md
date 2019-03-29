---
title: 堆砌纹理
description: 堆砌纹理
ms.assetid: 031739fe-32ee-46f1-a32a-de84f17eb528
keywords:
- 显示说明 WDK Windows 2000，DirectX 8.0 版本调色板的纹理
- 纹理 WDK DirectX 8.0
- 托盘化的纹理 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05ba64d33f781c76d6424e580e866251f85a18e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566547"
---
# <a name="palletized-textures"></a>堆砌纹理


## <span id="ddk_palettized_textures_gg"></span><span id="DDK_PALETTIZED_TEXTURES_GG"></span>


虽然托盘化纹理的 API 支持已更改为 DirectX 8.0，这是不会反映在 DDI 中。 现有的面向调色板的 DP2 令牌继续用于通知的调色板和纹理之间的绑定和调色板的更新的驱动程序。

不能假定，因为与 D3DDP2OP 建立一个面和调色板之间的关联\_SETPALETTE，， **lpPalette**字段的图面上结构指向有效的调色板。 调色板和建立 DP2 流图面之间的关联不反映在实际的外围应用和调色板数据结构。

此外，为这些调色板不调用 DirectDraw 的调色板 DDI 入口点。 所有 DDI 通知的纹理调色板操作是都通过实现 DP2 流。

 

 





