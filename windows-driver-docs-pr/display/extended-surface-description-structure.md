---
title: 扩展图面描述结构
description: 扩展图面描述结构
ms.assetid: 51936b15-590c-4113-a393-1a8306c24e7f
keywords:
- 绘制扩展 surface 功能 WDK DirectDraw，说明结构
- DirectDraw 扩展 surface 功能 WDK Windows 2000 显示，说明结构
- 扩展 surface 功能 WDK DirectDraw，说明结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1212cef3492cb5f8b4d2c8befa09129e0335e237
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064272"
---
# <a name="extended-surface-description-structure"></a>扩展图面描述结构


## <span id="ddk_extended_surface_description_structure_gg"></span><span id="DDK_EXTENDED_SURFACE_DESCRIPTION_STRUCTURE_GG"></span>


扩展 DirectDraw 表面说明结构 [**DDSURFACEDESC2**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))与 [**DDSURFACEDESC**](/previous-versions/windows/hardware/drivers/ff550339(v=vs.85)) 结构相同，不同之处在于，指向结构末尾处的 [**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85)) 结构的指针已替换为指向 [**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85)) 结构的指针。

[*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))和[*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))驱动程序调用的数据块都包含指向 DDSURFACEDESC 结构的指针。 从 DirectX 6.0 开始，这些指针实际上可能指向 DDSURFACEDESC2 结构，即使指针保持类型为 LPDDSURFACEDESC 也是如此。 如果驱动程序选择，则它可以检查[**DDSURFACEDESC**](/previous-versions/windows/hardware/drivers/ff550339(v=vs.85))指针的**dwSize**成员，从而决定指针是否确实指向[**DDSURFACEDESC2**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构。 如果你的驱动程序必须在预 DirectX 6.0 安装上运行，则必须进行此检查。

如果返回的大小为 sizeof (DDSURFACEDESC2) ，则驱动程序可以检查[**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构的**dwCaps2**、 **dwCaps3**和**dwCaps4**成员。

 

