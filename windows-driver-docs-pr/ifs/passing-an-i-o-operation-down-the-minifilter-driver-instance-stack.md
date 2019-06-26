---
title: 传递 I/O 操作向下微筛选器驱动程序实例堆栈
description: 沿微筛选器驱动程序实例堆栈向下传递 I/O 操作
ms.assetid: b2661e1e-2190-4def-be6c-27057c631304
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，传递关闭驱动程序实例堆栈
- 传递下微筛选器驱动程序堆栈 WDK 文件系统 I/O 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e9a289fea888c3577847929b06b30dc21d19a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386062"
---
# <a name="passing-io-operations-down-the-minifilter-driver-instance-stack"></a>传递 I/O 操作向下微筛选器驱动程序实例堆栈


## <span id="ddk_passing_an_io_operation_down_the_minifilter_instance_stack_if"></span><span id="DDK_PASSING_AN_IO_OPERATION_DOWN_THE_MINIFILTER_INSTANCE_STACK_IF"></span>


当微筛选器驱动程序[ **preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)或工作例程返回 I/O 操作筛选器管理器，筛选器管理器将操作发送到以下微筛选器驱动程序当前微筛选器驱动程序在微筛选器驱动程序实例堆栈并与旧的筛选器和文件系统，用于进一步处理。

微筛选器驱动程序的 preoperation 回调例程返回 I/O 操作到筛选器管理器以做进一步的处理返回以下状态的值之一：

-   FLT\_PREOP\_成功\_否\_回调 （所有操作类型）

-   FLT\_PREOP\_成功\_WITH\_回调 （所有操作类型）

-   FLT\_PREOP\_同步 （仅适用于基于 IRP 的 I/O 操作）

**请注意**  虽然 FLT\_PREOP\_同步应返回仅对于基于 IRP 的 I/O 操作，可以返回此状态值对于其他操作类型。 如果不是一个基于 IRP 的 I/O 操作的 I/O 操作返回它，则筛选器管理器会将此返回值，就好像 FLT\_PREOP\_成功\_WITH\_回调。

 

或者，被 preoperation 回调例程中的挂起的操作的工作例程返回 I/O 操作到筛选器管理器通过将传递在前面的状态值之一*CallbackStatus*参数时它调用[ **FltCompletePendedPreOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)恢复的挂起 I/O 操作的处理。

本部分包括：

[返回 FLT\_PREOP\_成功\_WITH\_回调](returning-flt-preop-success-with-callback.md)

[返回 FLT\_PREOP\_成功\_否\_回调](returning-flt-preop-success-no-callback.md)

[返回 FLT\_PREOP\_同步](returning-flt-preop-synchronize.md)

 

 




