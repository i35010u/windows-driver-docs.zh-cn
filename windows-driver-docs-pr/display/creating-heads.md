---
title: 创建头
description: 创建头
ms.assetid: 0b6d4aa0-e3c9-45df-998d-d6dfca5ab720
keywords:
- 磁头 WDK DirectX 9.0
- 多个头硬件 WDK DirectX 9.0 中，创建头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67e358921c652b2219a77caecbb3e6468c6b33e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564994"
---
# <a name="creating-heads"></a>创建头


## <span id="ddk_creating_heads_gg"></span><span id="DDK_CREATING_HEADS_GG"></span>


Microsoft DirectX 9.0 驱动程序在每个多头卡片上创建一个 Microsoft Direct3D 上下文，为每个多头卡和每个头部的 Microsoft DirectDraw 对象。 因此，多个头卡在创建过程具有每个头部分和跨头部分。 每个头部分大致对应于 DirectDraw DDI 调用，到 Direct3D DDI 调用的跨头部分。

跨各种磁头的连接点是由驱动程序的创建的 Direct3D 句柄[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)函数。 驱动程序组中的所有头跨将唯一的 Direct3D 句柄分配给每个面。 主标头的 Direct3D 上下文管理所有这些句柄，并且可以面向任何头创建任何呈现器目标最值得注意的是在翻转后缓冲链接从属头上。 **D3dCreateSurfaceEx**函数为每个从属头必须能够更新由主头句柄查找表。 随后，在对驱动程序的调用中仅使用这些句柄[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)主头节点的函数。

该驱动程序仅在主头上创建纹理和其他资源

该驱动程序创建并使用头按以下顺序中所述：

1.  对于每个头部，会执行以下操作来设置显示模式和主翻转图面：
    -   在运行时设置的显示模式。
    -   在运行时创建 DirectDraw 对象。
    -   在运行时创建主翻转链和可能的 Z 缓冲区。 在运行时指定**DDSCAPS2\_ADDITIONALPRIMARY**位 (0x80000000) 功能**dwCaps2**隶属[ **DDSCAPS2**](https://msdn.microsoft.com/library/windows/hardware/ff550292)结构 （包括 Z 缓冲区） 每个面的，以指示多个头卡的其他主图面。 运行时调用的驱动程序[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)函数。
    -   运行时调用的驱动程序[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)函数，首先为 master 和按照定义顺序**AdapterOrdinalInGroup**下属。 在此调用，Direct3D 处理运行时传递保证是唯一的组中的所有头。 该驱动程序可以插入从属 head 的句柄查找表的引用。 但是，因为在不创建 Direct3D 上下文的从属头、 否[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)到任何从属头发出命令。 因此，插入此引用是不必要的。
    -   运行时调用后[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)的所有头 （包括 master），进一步[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)进行调用对于每个从属头部的对 master 头 DirectDraw 对象翻转链。 驱动程序创建条目，并在主头句柄查找表中每个前端、 后向和深度/模具缓冲区的每个从属的头部。

2.  运行时调用的驱动程序[ *D3dContextCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff542178)仅对主标头的 DirectDraw 对象的函数。 这是应用程序运行时使用的唯一上下文。

3.  当应用程序请求时创建的纹理和资源时，运行时调用的驱动程序[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)并[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)函数通过主头。

4.  当应用程序进行呈现的调用时，运行时调用的驱动程序[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) master 头使用相应的操作代码的函数。

    当应用程序执行其他操作时，下面的调用路由到主和从属头：

    -   第一步中所述[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)调用都是为每个从属头部的翻转链提供驱动程序和句柄。 通常用于这些句柄**D3DDP2OP\_SETRENDERTARGET**操作代码令牌时应用程序将帧呈现到的其中一个从属头交换链后台缓冲区。
    -   运行时调用的驱动程序[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)每个标头 （主和从属项） 提供到主表面这些头的后台缓冲区的函数。 此调用永远不会显示从一个 head 的后台缓冲区到另一个头主图面。 每个标头的翻转链是完全独立的。
    -   在运行时可能会调用驱动程序的[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数将后台缓冲区复制到任何头前台缓冲区。 永远不会，此调用将从一个 head 后台缓冲区复制到另一个头前台缓冲区中。
    -   在运行时可调用的驱动程序[ *DdGetScanLine* ](https://msdn.microsoft.com/library/windows/hardware/ff549497)函数任何标头，因为此调用关联到监视器而不是 Direct3D 上下文的状态。
    -   在运行时可调用的驱动程序[ *DdLock* ](https://msdn.microsoft.com/library/windows/hardware/ff549599)上任何头的后台缓冲区的函数。

    应用程序可以分配与每个头部 Z 缓冲区或分配一个 Z 缓冲区按顺序使用每个头部。 在前一种情况，运行时调用的驱动程序[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)每个标头 （主和从属项） 的函数中所述第一步。 在后一种情况下，运行时调用的驱动程序*DdCreateSurface*函数只能在主头上的。 在任一情况下，运行时调用的驱动程序[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)函数来提供对所有在组中的所有头中是唯一的 Z 缓冲区句柄。

 

 





