---
title: 全屏模式行为
description: 全屏模式行为
ms.assetid: 43e7fec0-4e4d-401c-80c7-3e0710313214
keywords:
- 全屏旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2853d61a753e1b6811ed46cf1cdca9643c8160e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839689"
---
# <a name="full-screen-mode-behavior"></a>全屏模式行为


用户模式显示驱动程序可以确定呈现设备是否处于全屏模式：

-   如果在[**D3DDDIARG\_OPENRESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)结构的**Flags**成员中设置了**全屏**位字段标志，则*PResource*参数在调用驱动程序的[**OPENRESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数时指向该结构。

-   如果在[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**Flags**成员中设置了**主**位域标志，则*PResource*参数在调用驱动程序的[**CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数时指向该结构。

为 Microsoft DirectX 9.0 或更早版本开发的应用程序将导致 Microsoft Direct3D 运行时调用*OpenResource*来打开共享的主表面，然后*CreateResource*创建任何其他后台缓冲区。 Microsoft DirectX 9L 应用程序将导致 Direct3D 运行时调用*CreateResource* （不调用*OpenResource*）以创建所有交换链缓冲区。 Direct3D 运行时在[**D3DDDIARG\_OPENRESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)和 D3DDDIARG 的**旋转**成员中指定*pResource*参数指向的[ **\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的主表面方向分别调用[**OpenResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)和[**CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数。

对于全屏设备，用户模式显示驱动程序必须锁定旋转的资源，呈现到旋转的资源，并从旋转的资源执行位块传输（bitblt）。 通常情况下，用户模式显示驱动程序以旋转方向创建过渡渲染目标（所有锁、bitblts 和呈现都将转换为这些过渡渲染目标），并以横向方向（即数字到模拟转换器 \[DAC\] 使用进行扫描）。 当调用用户模式显示驱动程序来翻转数据时，它会在调用[**pfnPresentCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)函数发出 flip 命令之前，执行从过渡呈现目标到环境缓冲区的旋转 bitblt。

每当用户模式显示驱动程序必须执行涉及旋转资源和非旋转资源的 bitblt 时，Direct3D 运行时将在[**D3DDDIARG\_BLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_blt)的**Flags**成员中指定**旋转**位字段标志。对驱动程序的[**Blt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)函数的调用中的结构，以向驱动程序指示 bitblt 必须进行正确的旋转。

DirectX 9L 应用程序可以是旋转感知型，这意味着它们将以正确的方向呈现一切，并正确地处理锁定到旋转缓冲器的情况。 当 Direct3D 运行时为旋转感知的应用程序创建交换链时，运行时始终将旋转指定为 D3DDDI\_旋转\_标识在[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)的**旋转**成员中。结构，因为用户模式显示驱动程序无需执行任何特殊操作即可使旋转感知应用程序正常工作。

 

 





