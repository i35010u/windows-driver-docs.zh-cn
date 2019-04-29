---
title: 设置裁切矩形
description: 设置裁切矩形
ms.assetid: e85b4987-26b7-4005-b8eb-81ca36a9a777
keywords:
- 剪刀矩形 WDK DirectX 9.0
- 矩形的剪辑区域 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 321354cff24e2138e235288ea1b37a277ebfef95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390444"
---
# <a name="setting-scissor-rectangle"></a>设置裁切矩形


## <span id="ddk_setting_scissor_rectangle_gg"></span><span id="DDK_SETTING_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 版本驱动程序必须支持设置矩形的剪辑区域，即剪刀矩形。 设置此剪刀矩形呈现后，限制为只需通过剪刀矩形指定在呈现器目标的部分。 若要设置剪刀矩形，该驱动程序必须处理 D3DDP2OP\_SETSCISSORRECT 操作代码中其[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数。 指定的矩形的剪辑区域的 RECT 结构遵循中的操作代码[命令流](command-stream.md)。

 

 





