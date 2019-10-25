---
title: 支持二维操作
description: 支持二维操作
ms.assetid: 09611bba-5b36-4b7d-8d93-a99590eb5bbe
keywords:
- 二维操作 WDK DirectX 9。0
- 2D 操作 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c432e018a9b0238f7c2282f763971b7838d369c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829389"
---
# <a name="supporting-two-dimensional-operations"></a>支持二维操作


## <span id="ddk_supporting_two_dimensional_operations_gg"></span><span id="DDK_SUPPORTING_TWO_DIMENSIONAL_OPERATIONS_GG"></span>


DirectX 9.0 运行时指示驱动程序根据运行时检测到的驱动程序的版本，以不同的方式执行二维（2D）像素复制操作。 对于 DirectX 8.1 和更早版本的驱动程序，运行时调用驱动程序的[*DdBlt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数，并将此调用与[命令流](command-stream.md)同步。 对于 DirectX 9.0 和更高版本的驱动程序，运行时将传递 D3DDP2OP\_BLT、D3DDP2OP\_SURFACEBLT 或 D3DDP2OP\_COLORFILL 操作代码以及[**D3DHAL\_DP2BLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2blt)、 [**D3DHAL\_DP2SURFACEBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2surfaceblt)或[**D3DHAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2colorfill)在命令流中分别\_DP2COLORFILL 结构。 DirectX 9.0 和更高版本的驱动程序必须支持这些2D 操作代码。

如果运行时在对 DirectX 8.1 或更早的驱动程序的*DDBLT*函数的调用中指定 DDBLT\_COLORFILL 标志，则只要运行时识别目标图面，运行时会将 D3DCOLOR 填充颜色类型转换为显式像素值格式（即，格式的代码是 D3DFORMAT 枚举类型中的代码之一）。 如果格式由供应商提供且不被运行时识别，则运行时将 D3DCOLOR 填充颜色类型直接传递到驱动程序进行处理。 但是，运行时将转换为显式像素值、由 DirectShow 使用的特定颜色格式的 D3DCOLOR 填充颜色类型，但对于该驱动程序是专用的。

 

 





