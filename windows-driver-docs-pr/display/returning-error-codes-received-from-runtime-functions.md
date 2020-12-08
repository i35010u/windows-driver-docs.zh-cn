---
title: 返回从运行时函数收到的错误代码
description: 返回从运行时函数收到的错误代码
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，运行时函数错误代码
- 运行时函数错误代码 WDK 显示
- 错误代码 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2680cccd02d455958a1bd5e222a7f9dcd83799fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831871"
---
# <a name="returning-error-codes-received-from-runtime-functions"></a>返回从运行时函数收到的错误代码


调用 direct3d [版本9用户模式显示驱动程序的函数](/windows-hardware/drivers/ddi/d3dumddi/index) 时，必须返回它们在调用 [Direct3D 运行时提供的、访问函数](/windows-hardware/drivers/ddi/index)时所收到的错误代码。 例如，运行时可能会调用用户模式显示驱动程序函数，如 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 函数。 这进而会调用运行时提供的函数（如 [**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb) 函数）来执行特定操作，在本例中为资源分配内存。 如果用户模式显示驱动程序接收到对运行时提供的函数的调用中的错误代码，则必须将该错误代码返回给运行时。

**注意**   此规则有一个例外，驱动程序必须将运行时错误代码传递回运行时。 当驱动程序调用 [**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb) 运行时提供的函数时，若要为可选资源分配视频内存（如果已分配了视频内存），则不会应用规则。 如果 **pfnAllocateCb** 未能为仅用于优化性能的可选资源分配此视频内存，驱动程序将不会报告内存不足错误 (E \_ OUTOFMEMORY) 返回到运行时。

 

 

