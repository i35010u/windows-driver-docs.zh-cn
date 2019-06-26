---
title: 纹理位图传送
description: 纹理位图传送
ms.assetid: 5a2e49c1-e99d-4b0d-a46c-b22b3dcefaf8
keywords:
- blt WDK Direct3D
- 纹理管理 WDK Direct3D，平面闪
- 平面闪 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 979ab81556882a84dfa4d65177184444428196e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353433"
---
# <a name="texture-blitting"></a>纹理位图传送


## <span id="ddk_texture_blitting_gg"></span><span id="DDK_TEXTURE_BLITTING_GG"></span>


为 Direct3D DDI，DirectX 7.0 中引入了重大改变是纹理通过嵌入令牌中的是以位块传输[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)命令流。 此令牌是 D3DDP2OP\_TEXBLT，并且它表明纹理具有后备图面中传输到本地或非本地的视频内存的驱动程序。

此外，而不是驱动程序负责创建内部句柄，以通过旧的纹理*D3dTextureCreate*并*D3dTextureDestroy*回调，运行时现在将分配一个句柄为 Direct3D 上下文中创建的每个 DirectDrawSurface 对象数。 有关通过此句柄数，驱动程序发出信号[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)回调。

*D3dCreateSurfaceEx*每个硬件抽象层 (HAL) 之后，将调用[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))调用完成。 *D3dCreateSurfaceEx*每个内部硬件仿真层 (HEL) 之后，还将调用**用于 CreateSurface**调用完成。 创建后备 DirectDrawSurface 对象时，通常会出现 HEL 调用。 这些调用可能会发生之前和之后使用创建 Direct3D 上下文[ **D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)。

此外，当运行该应用程序时，调用[ **D3dDestroyDDLocal** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)清理并破坏这些图面为显式创建的所有驱动程序数据。 创建 Direct3D 上下文之前，还会进行此调用。 这样做是为了确保不存在任何与不清理任何上下文关联的脏句柄。 这是只需一预防措施，就不实际上会销毁任何如果上下文正确清理后使用。

 

 





