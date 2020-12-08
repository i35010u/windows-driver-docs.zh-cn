---
title: 全屏模式行为
description: 全屏模式行为
keywords:
- 全屏旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98bd75c3d6154a80627008a3e9b1b2ff513c2fd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840765"
---
# <a name="full-screen-mode-behavior"></a>全屏模式行为


用户模式显示驱动程序可以确定呈现设备是否处于全屏模式：

-   如果在 [**D3DDDIARG \_ OPENRESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)结构的 **Flags** 成员中设置了 **全屏** 位域标志，则 *pResource* 参数在调用驱动程序的 [**OPENRESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数时指向该结构。

-   如果在 [**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的 **Flags** 成员中设置了 **主** 位域标志，则 *pResource* 参数在调用驱动程序的 [**CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数时指向该结构。

为 Microsoft DirectX 9.0 或更早版本开发的应用程序将导致 Microsoft Direct3D 运行时调用 *OpenResource* 来打开共享的主表面，然后 *CreateResource* 创建任何其他后台缓冲区。 Microsoft DirectX 9L 应用程序将导致 Direct3D 运行时在不调用 *OpenResource*) 的情况下调用 *CreateResource* (来创建所有交换链缓冲区。 Direct3D 运行时在 [**D3DDDIARG \_ OPENRESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)和 [**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的 **旋转** 成员中指定主表面方向， *pResource* 参数分别指向 [**OPENRESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)和 [**CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数的调用。

对于全屏设备，用户模式显示驱动程序必须锁定旋转的资源、呈现到旋转的资源，以及执行从旋转的资源 (bitblt) 的位块传输。 通常情况下，用户模式显示驱动程序会在旋转方向上创建过渡渲染目标 (所有锁定、bitblts 和呈现都将按横向方向访问这些过渡渲染目标) 和主要分配 (也就是说，数字到模拟转换器 \[ DAC \] 用来扫描) 的方向。 当调用用户模式显示驱动程序来翻转数据时，它会在调用 [**pfnPresentCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb) 函数发出 flip 命令之前，执行从过渡呈现目标到环境缓冲区的旋转 bitblt。

每当用户模式显示驱动程序必须执行涉及旋转资源和非旋转资源的 bitblt 时，Direct3D 运行时会在调用驱动程序的 [**BLT**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)函数的 [**D3DDDIARG \_ BLT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_blt)结构的 **Flags** 成员中指定 **旋转** 位字段标志，以向驱动程序指示必须为 bitblt 正确旋转。

DirectX 9L 应用程序可以是旋转感知型，这意味着它们将以正确的方向呈现一切，并正确地处理锁定到旋转缓冲器的情况。 当 Direct3D 运行时为旋转感知的应用程序创建交换链时，运行时始终将旋转指定为 \_ \_ [**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的 **旋转** 成员中的 D3DDDI 旋转标识，因为用户模式显示驱动程序无需执行任何特殊操作即可使旋转感知应用程序正常工作。

 

