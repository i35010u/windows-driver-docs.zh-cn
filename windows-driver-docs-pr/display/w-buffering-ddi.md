---
title: W 缓冲 DDI
description: W 缓冲 DDI
keywords:
- Direct3D WDK Windows 2000 显示，w-缓冲
- w-缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81103b85b4c1d8af903cd7cb9eef7d532e897ed8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806319"
---
# <a name="w-buffering-ddi"></a>W 缓冲 DDI


## <span id="ddk_w_buffering_ddi_gg"></span><span id="DDK_W_BUFFERING_DDI_GG"></span>


驱动程序通过 \_ 在 [**D3DPRIMCAPS**](/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的 **DWRASTERCAPS** 成员中启用 D3DPRASTERCAPS WBUFFER cap 来支持 w-缓冲。 D3DRENDERSTATE \_ ZENABLE 呈现状态将传递给驱动程序，以启用或禁用 w 缓冲或 z 缓冲。

[**D3DHAL \_ DP2VIEWPORTINFO**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo)结构支持与世界空间正面和背面剪裁平面分别 (hither 和你) 的字段。 此信息也可用于调整雾化表。

 

