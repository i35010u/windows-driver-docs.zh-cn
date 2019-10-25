---
title: 纹理位图传送
description: 纹理位图传送
ms.assetid: 5a2e49c1-e99d-4b0d-a46c-b22b3dcefaf8
keywords:
- blt WDK Direct3D
- 纹理管理 WDK Direct3D，blitting
- blitting WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6d4b49923cdfc75a2b12c9f3a400db5add5f89d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829331"
---
# <a name="texture-blitting"></a>纹理位图传送


## <span id="ddk_texture_blitting_gg"></span><span id="DDK_TEXTURE_BLITTING_GG"></span>


在 DirectX 7.0 中引入的 Direct3D DDI 的一项重要变化是，通过在[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)命令流中嵌入令牌来 blitted 纹理。 此令牌是 D3DDP2OP\_TEXBLT，它指示驱动程序必须将纹理从后备表面传输到本地或非本地视频内存。

此外，运行时还会将句柄号分配给每个 DirectDrawSurface 对象，而不是负责创建纹理的内部句柄的驱动程序 *，而不*是负责在 Direct3D 上下文中创建。 该驱动程序通过[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)回调发送此句柄编号的信号。

每个硬件抽象层（HAL） [*DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))调用完成后，将调用*D3dCreateSurfaceEx* 。 每个内部硬件仿真层（HEL） **CreateSurface**调用完成后，也会调用*D3dCreateSurfaceEx* 。 创建后备 DirectDrawSurface 对象时通常会发生 HEL 调用。 这些调用可能会在使用[**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)创建 Direct3D 上下文之前和之后发生。

此外，在应用程序运行时，对[**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)进行调用，以清理并销毁为这些图面显式创建的任何驱动程序数据。 此调用也在创建 Direct3D 上下文之前进行。 这样做是为了确保没有与未清理的任何上下文关联的脏句柄。 这只是一种预防措施，在使用后正确清理上下文时，不应实际销毁任何内容。

 

 





