---
title: 以追溯方式要求自由线程 CalcPrivate DDI
description: 以追溯方式要求自由线程 CalcPrivate DDI
ms.assetid: a25fbe8e-737a-4b47-8293-7cf13ebc8ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f86c42e4d48c676424e03faa050db1fa27839eff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367161"
---
# <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>以追溯方式要求自由线程 CalcPrivate DDI


以开头的 Direct3D 版本 11 以追溯方式要求用户模式显示驱动程序函数*pfnCalcPrivate*是自由线程的 Direct3D 版本 10 DDI 函数上。 此追溯要求匹配的 Direct3D 版本 11 行为 DDI 为总是要求*pfnCalcPrivate\** 并[ **pfnCalcDeferredContextHandleSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538272)是自由线程即使驱动程序表明它的函数不支持 DDI 线程处理。 有关如何指示驱动程序的线程支持，请参阅[支持线程处理，命令将列出，和三维管道](supporting-threading--command-lists--and-3-d-pipeline.md)。 这一影响以前的版本要求的原因是此类函数是通常非常简单作为它们返回即时值的大小。 更复杂的函数决定要返回的即时值基于传递给函数的参数。 以开头的函数的要求*pfnCalcPrivate*实际写入的位置的任何数据而不堆栈不存在。 这些函数来读取参数之外的任何数据的要求是罕见。 若要读取数据的任何要求不会产生争用问题。 这一事实允许 Direct3D 11 版 API 来执行很多所需的优化，并防止执行成本高昂的同步创建每两次 (例如，任何调用以创建一个对等对象[ **CreateResource(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540691)或[ **CreateGeometryShader**](https://msdn.microsoft.com/library/windows/hardware/ff540648))，而不是只需一次。

此追溯的自由线程要求值得注意的例外是[ **CalcPrivateDeviceSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538288)用于满足显示设备创建的函数。 *CalcPrivateDeviceSize*位于适配器函数表 ([**D3D10\_2DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541900)或[ **D3D10DDI\_ADAPTERFUNCS**](https://msdn.microsoft.com/library/windows/hardware/ff541811))。 *CalcPrivateDeviceSize*不在下面的遇到线程处理模型中的这样的函数组。 不需要为自由线程*CalcPrivateDeviceSize*函数。

 

 





