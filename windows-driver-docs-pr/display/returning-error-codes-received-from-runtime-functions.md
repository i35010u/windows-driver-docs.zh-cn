---
title: 返回从运行时函数收到的错误代码
description: 返回从运行时函数收到的错误代码
ms.assetid: 4a2384e8-407f-4248-8b31-7c4e836b15dc
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，运行时函数错误代码
- 运行时函数错误代码 WDK 显示
- 错误代码 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 951b29698a54d65b6ebd4e1d67b76d88b80d9b34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825821"
---
# <a name="returning-error-codes-received-from-runtime-functions"></a>返回从运行时函数收到的错误代码


调用 direct3d[版本9用户模式显示驱动程序的函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)时，必须返回它们在调用[Direct3D 运行时提供的、访问函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)时所收到的错误代码。 例如，运行时可能会调用用户模式显示驱动程序函数，如[**CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数。 这进而会调用运行时提供的函数（如[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数）来执行特定操作，在本例中为资源分配内存。 如果用户模式显示驱动程序接收到对运行时提供的函数的调用中的错误代码，则必须将该错误代码返回给运行时。

**请注意**   此规则有一个例外，驱动程序必须将运行时错误代码传递回运行时。 当驱动程序调用[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)运行时提供的函数时，若要为可选资源分配视频内存（如果已分配了视频内存），则不会应用规则。 如果**pfnAllocateCb**未能为仅需优化性能的可选资源分配此视频内存，驱动程序不应将内存不足错误（E\_OUTOFMEMORY）报告回运行时。

 

 

 





