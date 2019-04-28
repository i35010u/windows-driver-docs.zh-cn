---
title: 传递 I/O 操作向下微筛选器驱动程序实例堆栈
description: 沿微筛选器驱动程序实例堆栈向下传递 I/O 操作
ms.assetid: b2661e1e-2190-4def-be6c-27057c631304
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，传递关闭驱动程序实例堆栈
- 传递下微筛选器驱动程序堆栈 WDK 文件系统 I/O 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48079622557ad60edc9f96ab8390779024c194cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352782"
---
# <a name="passing-io-operations-down-the-minifilter-driver-instance-stack"></a>传递 I/O 操作向下微筛选器驱动程序实例堆栈


## <span id="ddk_passing_an_io_operation_down_the_minifilter_instance_stack_if"></span><span id="DDK_PASSING_AN_IO_OPERATION_DOWN_THE_MINIFILTER_INSTANCE_STACK_IF"></span>


当微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)或工作例程返回 I/O 操作筛选器管理器，筛选器管理器将操作发送到以下微筛选器驱动程序当前微筛选器驱动程序在微筛选器驱动程序实例堆栈并与旧的筛选器和文件系统，用于进一步处理。

微筛选器驱动程序的 preoperation 回调例程返回 I/O 操作到筛选器管理器以做进一步的处理返回以下状态的值之一：

-   FLT\_PREOP\_成功\_否\_回调 （所有操作类型）

-   FLT\_PREOP\_成功\_WITH\_回调 （所有操作类型）

-   FLT\_PREOP\_同步 （仅适用于基于 IRP 的 I/O 操作）

**请注意**  虽然 FLT\_PREOP\_同步应返回仅对于基于 IRP 的 I/O 操作，可以返回此状态值对于其他操作类型。 如果不是一个基于 IRP 的 I/O 操作的 I/O 操作返回它，则筛选器管理器会将此返回值，就好像 FLT\_PREOP\_成功\_WITH\_回调。

 

或者，被 preoperation 回调例程中的挂起的操作的工作例程返回 I/O 操作到筛选器管理器通过将传递在前面的状态值之一*CallbackStatus*参数时它调用[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913)恢复的挂起 I/O 操作的处理。

本部分包括：

[返回 FLT\_PREOP\_成功\_WITH\_回调](returning-flt-preop-success-with-callback.md)

[返回 FLT\_PREOP\_成功\_否\_回调](returning-flt-preop-success-no-callback.md)

[返回 FLT\_PREOP\_同步](returning-flt-preop-synchronize.md)

 

 




