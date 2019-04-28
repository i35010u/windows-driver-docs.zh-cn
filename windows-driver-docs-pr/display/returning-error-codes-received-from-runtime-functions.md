---
title: 返回从运行时函数收到的错误代码
description: 返回从运行时函数收到的错误代码
ms.assetid: 4a2384e8-407f-4248-8b31-7c4e836b15dc
keywords:
- 用户模式显示驱动程序 WDK Windows Vista 中，运行时函数错误代码
- 运行时函数错误代码 WDK 显示
- 错误代码 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8f8bf3d417216376c35262629a9190dc64fa477
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351143"
---
# <a name="returning-error-codes-received-from-runtime-functions"></a>返回从运行时函数收到的错误代码


调用[Direct3D 版本 9 用户模式显示驱动程序提供的函数](https://msdn.microsoft.com/library/windows/hardware/ff552927)必须返回它们在调用时，接收的错误代码[Direct3D 运行时提供内核的服务访问函数](https://msdn.microsoft.com/library/windows/hardware/ff552870). 例如，运行时可能会调用用户模式显示驱动程序函数，如[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)函数。 此操作，请依次调用运行时提供的函数，如[ **pfnAllocateCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568893)函数，以执行特定操作，在这种情况下为资源分配内存。 如果用户模式显示驱动程序运行时提供的函数调用收到一个错误代码，它必须返回到运行时返回该错误代码。

**请注意**  没有驱动程序必须将运行时错误代码传递回运行时规则的例外。 当驱动程序调用[ **pfnAllocateCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568893)运行时提供的函数，当已分配的视频内存，为可选资源分配的视频内存规则不适用。 如果**pfnAllocateCb**无法为仅需要该项以优化性能，该驱动程序的可选资源分配此视频内存不应报告内存不足错误 (E\_OUTOFMEMORY) 返回到运行时。

 

 

 





