---
title: 按微筛选器驱动程序实例堆栈向下传递 i/o 操作
description: 沿微筛选器驱动程序实例堆栈向下传递 I/O 操作
ms.assetid: b2661e1e-2190-4def-be6c-27057c631304
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，并向下传递驱动程序实例堆栈
- 将 i/o 操作按下微筛选器驱动程序堆栈 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b76b17d9f2663a04777f799b524043460cbe7f47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841045"
---
# <a name="passing-io-operations-down-the-minifilter-driver-instance-stack"></a>按微筛选器驱动程序实例堆栈向下传递 i/o 操作


## <span id="ddk_passing_an_io_operation_down_the_minifilter_instance_stack_if"></span><span id="DDK_PASSING_AN_IO_OPERATION_DOWN_THE_MINIFILTER_INSTANCE_STACK_IF"></span>


当微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)或工作例程向筛选器管理器返回 i/o 操作时，筛选器管理器会将该操作发送到微筛选器驱动程序实例中当前微微筛选器驱动程序下的微筛选器驱动程序堆栈和到旧筛选器以及文件系统以进行进一步处理。

微筛选器驱动程序的 preoperation 回调例程返回筛选器管理器的 i/o 操作，以便进一步处理，方法是返回以下状态值之一：

-   FLT\_PREOP\_成功\_不\_回调（所有操作类型）

-   FLT\_PREOP\_成功\_\_回调（所有操作类型）

-   FLT\_PREOP\_同步（仅限基于 IRP 的 i/o 操作）

**请注意**   虽然只应为基于 IRP 的 i/o 操作返回 FLT\_PREOP\_同步，但你可以为其他操作类型返回此状态值。 如果为不是基于 IRP 的 i/o 操作的 i/o 操作返回，则筛选器管理器会将此返回值视为 FLT\_PREOP\_SUCCESS\_与\_回调一起使用。

 

或者，在 preoperation 回调例程中挂起的操作的工作例程会在调用 [**时通过在 CallbackStatus 参数中传递其中一个状态值来向筛选器管理器返回 i/o 操作FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)恢复挂起的 i/o 操作的处理。

本部分包括：

[\_回拨返回 FLT\_PREOP\_SUCCESS\_](returning-flt-preop-success-with-callback.md)

[返回 FLT\_PREOP\_成功\_不\_回拨](returning-flt-preop-success-no-callback.md)

[返回 FLT\_PREOP\_同步](returning-flt-preop-synchronize.md)

 

 




