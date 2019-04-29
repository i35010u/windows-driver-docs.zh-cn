---
title: 指向 DirectDraw 图面的指针
description: 指向 DirectDraw 图面的指针
ms.assetid: 5d7c8b22-d2d3-4e40-b7b2-7277e051812c
keywords:
- 上下文 WDK Direct3D，DirectDraw 图面指针
- DirectDraw 图面指针 WDK Direct3D
- 为 DirectDraw WDK Direct3D 图面指针
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8486c612054cf5e7f54bbf659bc173f57f9663e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352213"
---
# <a name="pointers-to-directdraw-surfaces"></a>指向 DirectDraw 图面的指针


## <span id="ddk_pointers_to_directdraw_surfaces_gg"></span><span id="DDK_POINTERS_TO_DIRECTDRAW_SURFACES_GG"></span>


驱动程序编写人员可能想要将一个指针保留在其专用的驱动程序端图面上结构内的 DirectDrawSurface 数据结构。 但是，这种做法不会不成功，Microsoft Windows 2000 及更高版本因为对 DirectDraw 内核端数据结构的访问间接通过隔离这些结构从用户模式和驱动程序的管理方案。 [**EngLockDirectDrawSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564966)提供了指向之前有效的结构的指针[ **EngUnlockDirectDrawSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff565042)调用例程。

此锁定/解锁对中，外部结构不保证驻留，或即使存在，在同一位置。 此外，这些锁定/取消锁定对影响性能。 如果该驱动程序保持其自身副本的图面上的结构，则不需要锁。 在低频率调用，如期间进行端驱动程序的图面上结构中的数据的更新[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)。 结果是更少的代码，必须执行期间高频率调用，如[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)。

 

 





