---
title: 支持多个处理器
description: 支持多个处理器
ms.assetid: 906d6b31-a447-4a94-b1a5-cd3028722db7
keywords:
- 用户模式显示驱动程序 WDK Windows Vista 中，多个处理器
- 多个处理器支持 WDK 显示
- 运行时处理多个处理器优化 WDK 显示
- 显示驱动程序处理多个处理器优化 WDK
- 多处理器优化 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9d2d04c42b662d4aa3688b27619a1cf964b86f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380552"
---
# <a name="supporting-multiple-processors"></a>支持多个处理器


在多处理器计算机上的用户模式显示驱动程序可以让 Microsoft Direct3D 运行时处理多个处理器优化或驱动程序可以执行其自己的多个处理器优化。

### <a name="span-idruntime-handledmultiple-processoroptimizationsspanspan-idruntime-handledmultiple-processoroptimizationsspanspan-idruntime-handledmultiple-processoroptimizationsspanruntime-handled-multiple-processor-optimizations"></a><span id="Runtime-Handled_Multiple-Processor_Optimizations"></span><span id="runtime-handled_multiple-processor_optimizations"></span><span id="RUNTIME-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>运行时处理多个处理器优化

仅在支持的驱动程序上启用了通过 Direct3D 运行时处理多个处理器优化[ **LockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)， [ **UnlockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)，并[**重命名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rename)函数。 使用这些功能，要很好地配合经常锁定动态资源的应用程序的多个处理器优化。 *LockAsync*并*UnlockAsync*函数-以及与[ **GetQueryData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getquerydata)函数-必须对驱动程序可重入的公开 DDI 0x0000000B 或更高版本。 该驱动程序中的 DDI 版本值返回**DriverVersion**的成员[ **D3D10DDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)对驱动程序的调用中的结构[**OpenAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)函数。 当运行时可重入的方式调用驱动程序函数时，一个线程可以执行函数时引用相同的显示设备的另一个线程内另一个驱动程序函数执行的内部。

Direct3D 运行时在某些情况下使用多个处理器的优化，以任务卸载到单独的处理器和提高计算机性能。 启用多处理器优化后，Direct3D 运行时和用户模式显示驱动程序之间添加一个额外的软件层。 此软件层截获所有 Direct3D 运行时导致用户模式显示驱动程序的函数的调用。

而不是调用用户模式下直接显示驱动程序、 软件层到工作线程以异步方式处理的批处理进行排队命令。 但是，软件层不能对用户模式显示驱动程序的函数进行的所有调用的批处理。 具体而言，软件层无法批处理对返回的信息的函数的调用 (例如， [ **CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource))。 当软件层必须调用这些类型的驱动程序函数之一时，刷新工作线程中，通过所有排队的命令，然后软件层在主应用程序线程上调用驱动程序函数的方式。

### <a name="span-iddriver-handledmultiple-processoroptimizationsspanspan-iddriver-handledmultiple-processoroptimizationsspanspan-iddriver-handledmultiple-processoroptimizationsspandriver-handled-multiple-processor-optimizations"></a><span id="Driver-Handled_Multiple-Processor_Optimizations"></span><span id="driver-handled_multiple-processor_optimizations"></span><span id="DRIVER-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>驱动程序处理多个处理器优化

如果驱动程序将执行其自己的多个处理器优化，它必须实现[ **LockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)， [ **UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)，和[**重命名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rename)函数。 在这种情况下，该驱动程序必须调用[ **pfnSetAsyncCallbacksCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setasynccallbackscb)函数运行时是否将启动或停止接收通知运行时调用从运行时的回调函数工作线程。

如果该驱动程序会执行其自己的多个处理器优化，它应遵循相同时它会确定要启用多处理器优化 Direct3D 运行时使用的策略。 此策略，所有进程间的系统资源的公平共享。 具体而言，该驱动程序应禁用在以下情况下的多个处理器优化：

-   在窗口模式下运行应用程序。

-   计算机包含只有一个处理器 （或处理器核心）;该驱动程序应禁用超线程的单处理器计算机上的优化。

-   应用程序请求不启用任何多处理器优化的或应用程序使用软件顶点处理;此信息传递给驱动程序的[ **CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)函数。

如果供应商想要启用多处理器优化在以下情况之一，应首先联系 Microsoft。

 

 





