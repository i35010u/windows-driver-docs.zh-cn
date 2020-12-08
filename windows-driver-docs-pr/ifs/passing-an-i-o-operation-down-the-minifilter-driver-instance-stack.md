---
title: 按微筛选器驱动程序实例堆栈向下传递 i/o 操作
description: 沿微筛选器驱动程序实例堆栈向下传递 I/O 操作
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，并向下传递驱动程序实例堆栈
- 将 i/o 操作按下微筛选器驱动程序堆栈 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4fd477cd32ca6af56af298b608e57ce058d7861
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816275"
---
# <a name="passing-io-operations-down-the-minifilter-driver-instance-stack"></a>按微筛选器驱动程序实例堆栈向下传递 i/o 操作


## <span id="ddk_passing_an_io_operation_down_the_minifilter_instance_stack_if"></span><span id="DDK_PASSING_AN_IO_OPERATION_DOWN_THE_MINIFILTER_INSTANCE_STACK_IF"></span>


当微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 或工作例程向筛选器管理器返回 i/o 操作时，筛选器管理器会将该操作发送到微筛选器驱动程序实例堆栈中当前微筛选器驱动程序下的微筛选器驱动程序，并发送到旧筛选器和文件系统以进行进一步处理。

微筛选器驱动程序的 preoperation 回调例程返回筛选器管理器的 i/o 操作，以便进一步处理，方法是返回以下状态值之一：

-   FLT \_ PREOP \_ SUCCESS \_ \_ (所有操作类型都不回) 

-   FLT \_ PREOP \_ 成功 \_ ， \_ 回调 (所有操作类型) 

-   FLT \_ PREOP \_ 仅同步 (基于 IRP 的 i/o 操作) 

**注意**   尽管 \_ \_ 仅应为基于 IRP 的 i/o 操作返回 FLT PREOP 同步，但你可以为其他操作类型返回此状态值。 如果为不是基于 IRP 的 i/o 操作的 i/o 操作返回，则筛选器管理器会将此返回值视为 FLT \_ PREOP \_ SUCCESS 是否成功 \_ \_ 。

 

或者，在 preoperation 回调例程中挂起的操作的工作例程会在调用 [**FltCompletePendedPreOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)以恢复处理挂起的 i/o 操作时，通过在 *CallbackStatus* 参数中传递上述状态值之一来返回对筛选器管理器的 i/o 操作。

本节包括：

[\_ \_ \_ 通过回调返回 FLT PREOP \_ SUCCESS](returning-flt-preop-success-with-callback.md)

[返回 FLT \_ PREOP \_ SUCCESS \_ NO \_ 回拨](returning-flt-preop-success-no-callback.md)

[返回 FLT \_ PREOP \_ SYNCHRONIZE](returning-flt-preop-synchronize.md)

 

