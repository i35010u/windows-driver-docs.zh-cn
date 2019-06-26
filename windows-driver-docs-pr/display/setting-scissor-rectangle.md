---
title: 设置裁切矩形
description: 设置裁切矩形
ms.assetid: e85b4987-26b7-4005-b8eb-81ca36a9a777
keywords:
- 剪刀矩形 WDK DirectX 9.0
- 矩形的剪辑区域 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09cbd39d49a2b0acebbd8159c8e877f42ee39a99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365562"
---
# <a name="setting-scissor-rectangle"></a>设置裁切矩形


## <span id="ddk_setting_scissor_rectangle_gg"></span><span id="DDK_SETTING_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 版本驱动程序必须支持设置矩形的剪辑区域，即剪刀矩形。 设置此剪刀矩形呈现后，限制为只需通过剪刀矩形指定在呈现器目标的部分。 若要设置剪刀矩形，该驱动程序必须处理 D3DDP2OP\_SETSCISSORRECT 操作代码中其[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数。 指定的矩形的剪辑区域的 RECT 结构遵循中的操作代码[命令流](command-stream.md)。

 

 





