---
title: 全屏幕模式行为
description: 全屏幕模式行为
ms.assetid: 43e7fec0-4e4d-401c-80c7-3e0710313214
keywords:
- 全屏幕旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 468ebbc7574205809a59e973cce23b1f37d0fe5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554890"
---
# <a name="full-screen-mode-behavior"></a>全屏幕模式行为


用户模式显示驱动程序可以确定在全屏幕模式下是渲染设备：

-   如果**全屏**中设置了位域标志**标志**的成员[ **D3DDDIARG\_OPENRESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff543232)结构该*pResource*参数，驱动程序的调用中指向[ **OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)函数。

-   如果**主**中设置了位域标志**标志**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)结构*pResource*参数，驱动程序的调用中指向[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)函数。

有关 Microsoft DirectX 9.0 或更早版本开发的应用程序将导致 Microsoft Direct3D 运行时调用*OpenResource*以打开共享主图面，然后*CreateResource*到创建任何其他后台缓冲区。 Microsoft DirectX 9 L 应用程序将导致调用 Direct3D 运行时*CreateResource* (而不调用*OpenResource*) 若要创建的所有交换链缓冲区。 Direct3D 运行时指定在主要的表面方向**旋转**的成员[ **D3DDDIARG\_OPENRESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff543232)和[**D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)结构*pResource*参数指向对两者的调用中[ **OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)并[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)函数。

对于全屏幕设备，用户模式显示驱动程序必须锁定旋转的资源、 呈现到旋转的资源，并从旋转资源执行位块传输 (bitblt)。 通常情况下，用户模式显示驱动程序的旋转的方向 （所有锁、 bitblts 和呈现会都转到这些中间呈现器目标上） 和横向方向的主要分配中创建临时的呈现器目标 (即，方向，数字模拟转换器\[DAC\]使用扫描出)。 当用户模式显示驱动程序调用来对数据进行翻转时，它执行旋转 bitblt 从中间呈现目标横向缓冲区调用之前[ **pfnPresentCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568916)到的问题函数翻转命令。

每当用户模式显示驱动程序必须执行涉及到旋转的资源和非旋转资源 bitblt，Direct3D 运行时指定**旋转**中的位域标志**标志**的成员[ **D3DDDIARG\_BLT** ](https://msdn.microsoft.com/library/windows/hardware/ff542884)驱动程序的调用中的结构[ **Blt** ](https://msdn.microsoft.com/library/windows/hardware/ff538251)函数以指示bitblt 必须进行适当的旋转的驱动程序。

DirectX 9 L 应用程序可以是旋转注意，这意味着它们将会呈现正确的方向中的所有内容，并且正确地处理旋转缓冲区的锁。 当 Direct3D 运行时创建的旋转感知应用程序的交换链时，运行时始终指定旋转为 D3DDDI\_旋转\_中的标识**旋转**的成员[**D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)结构，因为用户模式显示驱动程序不需要执行旋转感知应用程序中，若要运行的任何特殊操作。

 

 





