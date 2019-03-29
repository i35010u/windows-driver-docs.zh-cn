---
title: 扩展图面描述结构
description: 扩展图面描述结构
ms.assetid: 51936b15-590c-4113-a393-1a8306c24e7f
keywords:
- 绘制扩展表面功能 WDK DirectDraw 描述结构
- DirectDraw 扩展表面功能 WDK Windows 2000 显示，描述结构
- 扩展表面功能 WDK DirectDraw 描述结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 895c160190a21daacc954a0c2e71fe5285a7a786
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568506"
---
# <a name="extended-surface-description-structure"></a>扩展图面描述结构


## <span id="ddk_extended_surface_description_structure_gg"></span><span id="DDK_EXTENDED_SURFACE_DESCRIPTION_STRUCTURE_GG"></span>


扩展的 DirectDraw 表面描述结构[ **DDSURFACEDESC2**](https://msdn.microsoft.com/library/windows/hardware/ff550340)，等同于[ **DDSURFACEDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff550339)结构，只不过指向指针[ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)结构末尾的结构已替换为指向[ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)结构。

数据块[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)并[ *DdCanCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549213)驱动程序调用每个包含指向 DDSURFACEDESC结构。 从 DirectX 6.0 开始，这些指针可能实际指向的 DDSURFACEDESC2 结构，即使指针保持 LPDDSURFACEDESC 作为类型化。 如果选择了驱动程序，它可以检查**dwSize**的成员[ **DDSURFACEDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff550339)指针，从而决定指针如果实际指向[ **DDSURFACEDESC2** ](https://msdn.microsoft.com/library/windows/hardware/ff550340)结构。 如果您的驱动程序必须在预 DirectX 6.0 安装上运行，它必须进行此检查。

如果返回的大小，sizeof(DDSURFACEDESC2) 驱动程序然后可以检查**dwCaps2**， **dwCaps3**，并**dwCaps4**的成员[ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)结构。

 

 





