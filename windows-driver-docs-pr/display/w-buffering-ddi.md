---
title: W 缓冲 DDI
description: W 缓冲 DDI
ms.assetid: eb1270c3-0eaa-47a4-8fc6-53aea981b597
keywords:
- Direct3D WDK Windows 2000 显示，w-缓冲
- w-缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc049f000df0f55cf8b891e35a646d6b2a5b1fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825233"
---
# <a name="w-buffering-ddi"></a>W 缓冲 DDI


## <span id="ddk_w_buffering_ddi_gg"></span><span id="DDK_W_BUFFERING_DDI_GG"></span>


该驱动程序通过在[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwRasterCaps**成员中启用 D3DPRASTERCAPS\_WBUFFER cap 来支持 w 缓冲。 D3DRENDERSTATE\_ZENABLE render 状态将传递给驱动程序，以启用或禁用 w 缓冲或 z 缓冲。

[**D3DHAL\_DP2VIEWPORTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo)结构支持与世界空间正面和反面扣平面（分别为 hither 和你）对应的字段。 此信息也可用于调整雾化表。

 

 





