---
title: 纹理图阵
description: 纹理图阵
ms.assetid: 5a2e49c1-e99d-4b0d-a46c-b22b3dcefaf8
keywords:
- blt WDK Direct3D
- 纹理管理 WDK Direct3D，平面闪
- 平面闪 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b37648cfed2fee5928f777bd88386f1ac682fd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554685"
---
# <a name="texture-blitting"></a>纹理图阵


## <span id="ddk_texture_blitting_gg"></span><span id="DDK_TEXTURE_BLITTING_GG"></span>


为 Direct3D DDI，DirectX 7.0 中引入了重大改变是纹理通过嵌入令牌中的是以位块传输[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)命令流。 此令牌是 D3DDP2OP\_TEXBLT，并且它表明纹理具有后备图面中传输到本地或非本地的视频内存的驱动程序。

此外，而不是驱动程序负责创建内部句柄，以通过旧的纹理*D3dTextureCreate*并*D3dTextureDestroy*回调，运行时现在将分配一个句柄为 Direct3D 上下文中创建的每个 DirectDrawSurface 对象数。 有关通过此句柄数，驱动程序发出信号[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)回调。

*D3dCreateSurfaceEx*每个硬件抽象层 (HAL) 之后，将调用[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)调用完成。 *D3dCreateSurfaceEx*每个内部硬件仿真层 (HEL) 之后，还将调用**用于 CreateSurface**调用完成。 创建后备 DirectDrawSurface 对象时，通常会出现 HEL 调用。 这些调用可能会发生之前和之后使用创建 Direct3D 上下文[ **D3dContextCreate**](https://msdn.microsoft.com/library/windows/hardware/ff542178)。

此外，当运行该应用程序时，调用[ **D3dDestroyDDLocal** ](https://msdn.microsoft.com/library/windows/hardware/ff544685)清理并破坏这些图面为显式创建的所有驱动程序数据。 创建 Direct3D 上下文之前，还会进行此调用。 这样做是为了确保不存在任何与不清理任何上下文关联的脏句柄。 这是只需一预防措施，就不实际上会销毁任何如果上下文正确清理后使用。

 

 





