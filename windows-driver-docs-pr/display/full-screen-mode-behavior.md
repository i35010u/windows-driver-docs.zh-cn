---
title: 全屏模式行为
description: 全屏模式行为
ms.assetid: 43e7fec0-4e4d-401c-80c7-3e0710313214
keywords:
- 全屏幕旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ba8a6d3c42648501cfa28cff7ee93d0a9cdda3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356366"
---
# <a name="full-screen-mode-behavior"></a>全屏模式行为


用户模式显示驱动程序可以确定在全屏幕模式下是渲染设备：

-   如果**全屏**中设置了位域标志**标志**的成员[ **D3DDDIARG\_OPENRESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)结构该*pResource*参数，驱动程序的调用中指向[ **OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数。

-   如果**主**中设置了位域标志**标志**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构*pResource*参数，驱动程序的调用中指向[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数。

有关 Microsoft DirectX 9.0 或更早版本开发的应用程序将导致 Microsoft Direct3D 运行时调用*OpenResource*以打开共享主图面，然后*CreateResource*到创建任何其他后台缓冲区。 Microsoft DirectX 9 L 应用程序将导致调用 Direct3D 运行时*CreateResource* (而不调用*OpenResource*) 若要创建的所有交换链缓冲区。 Direct3D 运行时指定在主要的表面方向**旋转**的成员[ **D3DDDIARG\_OPENRESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)和[**D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构*pResource*参数指向对两者的调用中[ **OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)并[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数。

对于全屏幕设备，用户模式显示驱动程序必须锁定旋转的资源、 呈现到旋转的资源，并从旋转资源执行位块传输 (bitblt)。 通常情况下，用户模式显示驱动程序的旋转的方向 （所有锁、 bitblts 和呈现会都转到这些中间呈现器目标上） 和横向方向的主要分配中创建临时的呈现器目标 (即，方向，数字模拟转换器\[DAC\]使用扫描出)。 当用户模式显示驱动程序调用来对数据进行翻转时，它执行旋转 bitblt 从中间呈现目标横向缓冲区调用之前[ **pfnPresentCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)到的问题函数翻转命令。

每当用户模式显示驱动程序必须执行涉及到旋转的资源和非旋转资源 bitblt，Direct3D 运行时指定**旋转**中的位域标志**标志**的成员[ **D3DDDIARG\_BLT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_blt)驱动程序的调用中的结构[ **Blt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)函数以指示bitblt 必须进行适当的旋转的驱动程序。

DirectX 9 L 应用程序可以是旋转注意，这意味着它们将会呈现正确的方向中的所有内容，并且正确地处理旋转缓冲区的锁。 当 Direct3D 运行时创建的旋转感知应用程序的交换链时，运行时始终指定旋转为 D3DDDI\_旋转\_中的标识**旋转**的成员[**D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构，因为用户模式显示驱动程序不需要执行旋转感知应用程序中，若要运行的任何特殊操作。

 

 





