---
title: 创建驱动程序端图面结构
description: 创建驱动程序端图面结构
ms.assetid: d5e2e6ee-8853-4a17-b1c6-48c75474b2b7
keywords:
- 上下文 WDK Direct3D，驱动程序端图面上结构
- 驱动程序端面结构 WDK Direct3D
- D3dCreateSurfaceEx
- WDK DirectDraw，驱动程序端结构的图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d715e7c1e46d59516eec7283a5360db4c74d409e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387248"
---
# <a name="creating-driver-side-surface-structures"></a>创建驱动程序端图面结构


## <span id="ddk_creating_driver_side_surface_structures_gg"></span><span id="DDK_CREATING_DRIVER_SIDE_SURFACE_STRUCTURES_GG"></span>


DirectDraw 运行时调用的驱动程序[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)后已调用的入口点[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)条目点和分配的内存图面。 运行时调用*D3dCreateSurfaceEx*仅对于使用 DDSCAPS 标记这些图面\_纹理、 DDSCAPS\_EXECUTEBUFFER、 DDSCAPS\_3DDEVICE，或 DDSCAPS\_ZBUFFER 标志。

然后再调用[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)，运行时将一个整数值分配为句柄在图面。 此值存储在**dwSurfaceHandle** DDRAWI 成员\_DDSURFACE\_更多结构 (如指向**lpSurfMore** DDRAWI 成员\_DDSURFACE\_LCL 结构)。 请参阅[ **DD\_面\_详细**](https://msdn.microsoft.com/library/windows/hardware/ff551737)并[ **DD\_面\_本地**](https://msdn.microsoft.com/library/windows/hardware/ff551733)，这是别名 DDRAWI\_DDSURFACE\_更和 DDRAWI\_DDSURFACE\_LCL 结构。

这些整数值 1 开始，并保留越小越好。 （零是有保证的图面上的句柄值无效。）目的是驱动程序可以为其自身结构保留的指针的数组。 一旦收到一个句柄 (时*D3dCreateSurfaceEx*调用)，超过数组末尾，它可以重新分配数组并继续。 Direct3D 运行时没有句柄将值传递给驱动程序之前向驱动程序通过显示该句柄*D3dCreateSurfaceEx*。 但是，该驱动程序应该足够可靠，为句柄值超出范围或已释放句柄表中的槽的引用 (即为其句柄[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)已调用）。 请注意，由于零是有保证的无效值，句柄表中的零个项可以重复使用用于其他目的。 *Perm3*示例驱动程序使用的零个项来存储数组的当前长度。

**请注意**   Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia3 示例显示器驱动程序 (*Perm3.h*)。 你可以获取从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载此示例驱动程序。

 

 

 





