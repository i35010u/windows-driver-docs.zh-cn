---
title: 支持二维操作
description: 支持二维操作
ms.assetid: 09611bba-5b36-4b7d-8d93-a99590eb5bbe
keywords:
- 二维操作 WDK DirectX 9.0
- 2D 操作 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6505a53bf1babc51253a4be6791e432ec28848d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522649"
---
# <a name="supporting-two-dimensional-operations"></a>支持二维操作


## <span id="ddk_supporting_two_dimensional_operations_gg"></span><span id="DDK_SUPPORTING_TWO_DIMENSIONAL_OPERATIONS_GG"></span>


DirectX 9.0 运行时将定向驱动程序以执行以不同的方式根据运行时检测到的驱动程序版本的二维 (2D) 像素的复制操作。 有关 DirectX 8.1 和早期的驱动程序，则运行时调用的驱动程序[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数，并同步使用此调用[命令流](command-stream.md)。 有关 DirectX 9.0 和更高版本的驱动程序，运行时将传递 D3DDP2OP\_BLT、 D3DDP2OP\_SURFACEBLT 或 D3DDP2OP\_COLORFILL 操作代码，连同[ **D3DHAL\_DP2BLT** ](https://msdn.microsoft.com/library/windows/hardware/ff545426)， [ **D3DHAL\_DP2SURFACEBLT**](https://msdn.microsoft.com/library/windows/hardware/ff545858)，或[ **D3DHAL\_DP2COLORFILL**](https://msdn.microsoft.com/library/windows/hardware/ff545450)分别中命令流的结构。 DirectX 9.0 和更高版本的驱动程序必须支持这些 2D 操作代码。

如果在运行时指定 DDBLT\_中对 DirectX 8.1 或更早的驱动程序的调用 COLORFILL 标志*DdBlt*函数，运行时将 D3DCOLOR 填充颜色文字转换为一个显式的像素值，只要运行时识别目标图面上格式 （即格式的代码是一个 D3DFORMAT 枚举类型中的代码）。 如果格式是由供应商提供，并且无法识别由运行时，运行时 D3DCOLOR 填充颜色类型将直接传递到处理的驱动程序。 但是，在运行时，将转换为显式的像素值，使用 DirectShow 的但除此之外，专用于该驱动程序的特定颜色格式的 D3DCOLOR 填充颜色类型。

 

 





