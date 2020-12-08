---
title: 编写预操作和后操作回调例程
description: 编写预操作和后操作回调例程
keywords:
- 文件系统微筛选器驱动程序 WDK，preoperation 回调例程
- 微筛选器驱动程序 WDK，preoperation 回调例程
- preoperation 回调例程 WDK 文件系统微筛选器，关于 preoperation 回调例程
- postoperation 回调例程 WDK 文件系统微筛选器，关于 postoperation 回调例程
- 文件系统微筛选器驱动程序 WDK，postoperation 回调例程
- 微筛选器驱动程序 WDK，postoperation 回调例程
- preoperation 回调例程 WDK 文件系统微筛选器
- postoperation 回调例程 WDK 文件系统微筛选器
- I/o WDK 文件系统
- 回调例程 WDK 文件系统
- 筛选 i/o 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d71683105ef221f3e059c16659394d8227614f75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832997"
---
# <a name="writing-preoperation-and-postoperation-callback-routines"></a>编写预操作和后操作回调例程


## <span id="ddk_writing_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


在其 **DriverEntry** 例程中，微筛选器驱动程序最多可注册一个 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) ，最多可注册一个 [**postoperation 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 例程，用于需要进行筛选的每种类型的 i/o 操作。

与旧式文件系统筛选器驱动程序不同，微筛选器驱动程序可以选择要筛选的 i/o 操作的类型。 微筛选器驱动程序可以为给定类型的 i/o 操作注册一个 preoperation 回调例程，而无需注册 postoperation 回调，反之亦然。 微筛选器驱动程序只接收其已注册 preoperation 或 postoperation 回调例程的 i/o 操作。

*Preoperation 回调例程* 类似于旧筛选器驱动程序模型中的调度例程。 当筛选器管理器处理 i/o 操作时，它会在为此类型的 i/o 操作注册了一个的微筛选器驱动程序实例堆栈中调用每个微筛选器驱动程序的 preoperation 回调例程。 堆栈中最顶层的微筛选器驱动程序（即，其实例的最高级别为，即首先接收操作）。 当该微筛选器驱动程序完成处理操作时，它会将操作返回到筛选器管理器，然后将操作传递到下一个最高的微筛选器驱动程序，等等。 如果微筛选器驱动程序实例堆栈中的所有微筛选器驱动程序都已处理 i/o 操作（除非微筛选器驱动程序已完成 i/o 操作），则筛选器管理器会将操作发送到旧筛选器和文件系统。

*Postoperation 回调例程* 类似于旧筛选器驱动程序模型中的完成例程。 I/o 管理器将操作传递到文件系统，并将操作的已注册完成例程的旧筛选器传递给文件系统和旧筛选器后，开始处理 i/o 操作。 完成这些完成例程后，筛选器管理器将执行该操作的完成处理。 然后，筛选器管理器将在为此类型的 i/o 操作注册了一个微筛选器驱动程序实例堆栈中的每个微筛选器驱动程序中调用 postoperation 回调例程。 堆栈中的底部微筛选器驱动程序（即，其实例具有最低级别的驱动程序）首先接收操作。 当该微筛选器驱动程序完成处理操作时，它会将操作返回到筛选器管理器，然后将操作传递到下一个最小的微筛选器驱动程序，等等。

本节包括：

[注册 Preoperation 和 Postoperation 回调例程](registering-preoperation-and-postoperation-callback-routines.md)

[筛选微筛选器驱动程序中的 i/o 操作](filtering-i-o-operations-in-a-minifilter-driver.md)

[编写 Preoperation 回调例程](writing-preoperation-callback-routines.md)

[编写 Postoperation 回调例程](writing-postoperation-callback-routines.md)

[修改 i/o 操作的参数](modifying-the-parameters-for-an-i-o-operation.md)

[确定 i/o 操作的缓冲方法](determining-the-buffering-method-for-an-i-o-operation.md)

[访问 i/o 操作的用户缓冲区](accessing-the-user-buffers-for-an-i-o-operation.md)

 

