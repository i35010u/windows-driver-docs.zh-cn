---
title: 直接在硬件上处理 3-D 虚拟纹理
description: 直接在硬件上处理 3-D 虚拟纹理
ms.assetid: 5390f62d-3359-4f19-ab6c-07239e598b20
keywords:
- 三维纹理 WDK 显示
- 纹理 WDK 显示
- 三维纹理 WDK 显示
- 操作三维纹理直接 WDK 显示
- 硬件三维纹理操作 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac13da25f91a0590623def4866f44f0d83e62869
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330607"
---
# <a name="manipulating-3-d-virtual-textures-directly-from-hardware"></a>直接在硬件上处理 3-D 虚拟纹理


## <span id="ddk_manipulating_3_d_virtual_textures_directly_from_hardware_gg"></span><span id="DDK_MANIPULATING_3_D_VIRTUAL_TEXTURES_DIRECTLY_FROM_HARDWARE_GG"></span>


用户模式显示驱动程序可以创建基于现有的虚拟地址 （例如，三维 (3-D) 纹理文件的视图的虚拟地址） 的分配。 创建基于现有的虚拟地址的分配使三维纹理对硬件操作的系统内存副本可用。 但是，在此方案中，用户模式显示驱动程序的*锁*函数必须始终会逐出页从本地的视频内存返回到系统内存，因分配的虚拟地址未分配的视频内存管理器。 因此，视频内存管理器不能以透明方式重新映射从系统内存为视频内存，反之亦然纹理的虚拟地址。 换而言之，使用此属性的虚拟地址不能为映射的视图。

 

 





