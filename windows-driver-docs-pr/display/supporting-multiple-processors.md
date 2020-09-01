---
title: 支持多个处理器
description: 支持多个处理器
ms.assetid: 906d6b31-a447-4a94-b1a5-cd3028722db7
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，多处理器
- 多处理器支持 WDK 显示
- 运行时处理的多处理器优化 WDK 显示
- 驱动程序处理的多处理器优化 WDK 显示
- 多处理器优化 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68137fd38c22c31baccd9dd56427dfb303add6ae
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064578"
---
# <a name="supporting-multiple-processors"></a>支持多个处理器


多处理器计算机上的用户模式显示驱动程序可以让 Microsoft Direct3D 运行时处理多处理器优化，或者驱动程序可以执行其自己的多处理器优化。

### <a name="span-idruntime-handled_multiple-processor_optimizationsspanspan-idruntime-handled_multiple-processor_optimizationsspanspan-idruntime-handled_multiple-processor_optimizationsspanruntime-handled-multiple-processor-optimizations"></a><span id="Runtime-Handled_Multiple-Processor_Optimizations"></span><span id="runtime-handled_multiple-processor_optimizations"></span><span id="RUNTIME-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>运行时处理的多处理器优化

Direct3D 运行时处理的多处理器优化仅在支持 [**LockAsync**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)、 [**UnlockAsync**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)和 [**Rename**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rename) 函数的驱动程序上启用。 利用这些函数，多处理器优化可以很好地处理经常锁定动态资源的应用程序。 *LockAsync*和*UnlockAsync*函数与[**GetQueryData**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getquerydata)函数一起使用时，必须在公开 DDI 版本0x0000000B 或更高版本的驱动程序上是可重入的。 驱动程序在调用驱动程序的[**OPENADAPTER**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)函数的[**D3D10DDIARG \_ OPENADAPTER**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构的**DriverVersion**成员中返回 DDI 版本值。 当运行时以可重入方式调用驱动程序函数时，一个线程可以在该函数内执行，而另一个引用同一显示设备的线程在另一个驱动程序函数内执行。

在某些情况下，Direct3D 运行时使用多处理器优化将工作卸载到单独的处理器上并提高计算机性能。 启用多处理器优化后，会在 Direct3D 运行时和用户模式显示驱动程序之间添加其他软件层。 此软件层将截获 Direct3D 运行时要对用户模式显示驱动程序的功能进行的所有调用。

软件层不是直接调用用户模式显示驱动程序，而是将命令排队，以便批处理工作线程异步处理。 不过，软件层无法对用户模式显示驱动程序的所有调用进行批处理。 特别是，软件层无法对返回信息 (例如 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)) 的函数进行批处理调用。 当软件层必须调用这两种类型的驱动程序时，它将通过工作线程刷新所有排队的命令，然后软件层在主应用程序线程上调用驱动程序函数。

### <a name="span-iddriver-handled_multiple-processor_optimizationsspanspan-iddriver-handled_multiple-processor_optimizationsspanspan-iddriver-handled_multiple-processor_optimizationsspandriver-handled-multiple-processor-optimizations"></a><span id="Driver-Handled_Multiple-Processor_Optimizations"></span><span id="driver-handled_multiple-processor_optimizations"></span><span id="DRIVER-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>驱动程序处理的多处理器优化

如果驱动程序将执行自己的多处理器优化，则它不能实现 [**LockAsync**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)、 [**UnlockAsync**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)和 [**Rename**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rename) 函数。 在这种情况下，驱动程序必须调用 [**pfnSetAsyncCallbacksCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setasynccallbackscb) 函数以通知运行时，运行时是启动还是停止从工作线程接收对运行时的回调函数的调用。

如果驱动程序执行其自己的多处理器优化，则它应遵循 Direct3D 运行时在确定启用多处理器优化时使用的相同策略。 此策略允许跨所有进程公平共享系统资源。 具体而言，驱动程序应在下列情况下禁用多处理器优化：

-   应用程序在窗口模式下运行。

-   计算机只包含一个处理器 (或处理器核心) ;驱动程序应在具有超线程的单处理器计算机上禁用优化。

-   应用程序请求没有启用多处理器优化，或者应用程序使用软件顶点处理;此信息将传递给驱动程序的 [**CreateDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice) 函数。

如果供应商想要在其中一种情况下启用多处理器优化，则他们应该首先与 Microsoft 联系。

 

