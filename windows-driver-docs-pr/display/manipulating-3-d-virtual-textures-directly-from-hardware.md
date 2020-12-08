---
title: 直接在硬件上处理 3-D 虚拟纹理
description: 直接在硬件上处理 3-D 虚拟纹理
keywords:
- 三维纹理 WDK 显示
- 纹理 WDK 显示
- 三维纹理 WDK 显示
- 直接操作3-D 纹理显示 WDK
- 硬件三维纹理操作 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 537c7e4ad0b9f3e8de7c90e7dd4968903dc842b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793889"
---
# <a name="manipulating-3-d-virtual-textures-directly-from-hardware"></a>直接在硬件上处理 3-D 虚拟纹理


## <span id="ddk_manipulating_3_d_virtual_textures_directly_from_hardware_gg"></span><span id="DDK_MANIPULATING_3_D_VIRTUAL_TEXTURES_DIRECTLY_FROM_HARDWARE_GG"></span>


用户模式显示驱动程序可以在现有虚拟地址 (上创建分配，例如，三维 (三维) 纹理文件) 的视图的虚拟地址。 在现有虚拟地址之上创建分配使3D 纹理可用于系统内存副本的硬件操作。 但是，在这种情况下，用户模式显示驱动程序的 *锁定* 功能必须始终将页面从本地视频内存中逐出回系统内存，因为该分配的虚拟地址不是由视频内存管理器分配的。 因此，视频内存管理器无法以透明方式将纹理的虚拟地址重新映射到视频内存，反之亦然。 换句话说，具有此属性的虚拟地址不能为映射视图。

 

 





