---
title: 驱动程序管理的纹理
description: 驱动程序管理的纹理
ms.assetid: 7ec56b86-dc29-41c3-91f4-2a30e9116b61
keywords:
- 纹理管理 WDK Direct3D，驱动程序管理
- 驱动程序管理纹理 WDK Direct3D
- 可管理纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 964d58b0ef90b9287513ddd21712cbee552e0d3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391506"
---
# <a name="driver-managed-textures"></a>驱动程序管理的纹理


## <span id="ddk_driver_managed_textures_gg"></span><span id="DDK_DRIVER_MANAGED_TEXTURES_GG"></span>


该驱动程序可以管理已标记为可托管的纹理。 这些 DirectDrawSurface 对象都被标记为可使用 DDSCAPS2\_TEXTUREMANAGE 标志**dwCaps2**引用结构成员**lpSurfMore-&gt;ddCapsEx**. (**lpSurfMore**并**ddCapsEx**属于[ **DD\_面\_本地**](https://msdn.microsoft.com/library/windows/hardware/ff551733)和[ **DD\_图面\_详细**](https://msdn.microsoft.com/library/windows/hardware/ff551737)结构，分别。)

该驱动程序支持通过设置驱动程序管理的纹理**dwCaps2**的成员[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)结构 DDCAPS2\_CANMANAGETEXTURE 位。 该驱动程序指定在此 DDCORECAPS 结构**ddCaps**的成员[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构。 DD\_返回 HALINFO [ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)响应 DirectDraw 组件的驱动程序的初始化。

该驱动程序然后可以在以"迟缓"方式的视频或非本地内存中创建必要的图面。 也就是说，驱动程序会使后备图面，直到它需要它们，但之前光栅化基元，可使用的纹理中的纹理。

应主要由其优先级分配逐出图面。 该驱动程序响应 D3DDP2OP\_SETPRIORITY 操作代码中[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)命令流。 此操作的代码对于给定表面的优先级设置。 作为辅助措施，该驱动程序应使用的最早使用 (LRU) 方案中收回图面。 在特定方案完全相同的两个或多个纹理的优先级时，驱动程序将使用此方案。 在逻辑上，应该不会在所有逐出正在使用中的任何图面。

如果驱动程序支持托管图面，则该驱动程序可能会收到一个特殊[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)为托管的图面中的视频内存丢失，如模式切换发生时的情况下调用。 在本例中，DRAWISURF\_设置无效标志和驱动程序只需逐出的此托管的图面则视频内存的副本，并保留其他结构保持不变。 否则，该驱动程序执行正则表达式销毁图面上的调用。

该驱动程序应处理[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)并[ *DdLock* ](https://msdn.microsoft.com/library/windows/hardware/ff549599)管理纹理时相应调用。 这是因为对后备图面上图像的任何更改必须传播到表面的视频内存副本，然后再次使用纹理。 该驱动程序应确定它是否更好的做法更新只需在图面或所有它的一部分。 例如，如果驱动程序的*DdLock*函数调用以修改仅为一部分的图面上，则视频内存的副本的备份 （系统内存） 映像，然后当驱动程序的*DdBlt*调用函数驱动程序可以通过只是平面闪表面从系统内存到视频内存以下需要优化更新。

允许驱动程序以便对纹理执行优化转换或位置和时间确定为自身执行纹理管理传输内存中的纹理。

 

 





