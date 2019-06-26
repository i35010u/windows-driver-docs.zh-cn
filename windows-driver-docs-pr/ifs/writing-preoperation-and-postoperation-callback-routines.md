---
title: 编写预操作和后操作回调例程
description: 编写预操作和后操作回调例程
ms.assetid: ad706d01-7a14-4730-8189-c465637987dc
keywords:
- 文件系统微筛选器驱动程序 WDK，preoperation 回调例程
- 微筛选器驱动程序 WDK，preoperation 回调例程
- preoperation 回调例程 WDK 文件系统微筛选器，有关 preoperation 回调例程
- postoperation 回调例程 WDK 文件系统微筛选器，有关 postoperation 回调例程
- 文件系统微筛选器驱动程序 WDK，postoperation 回调例程
- 微筛选器驱动程序 WDK，postoperation 回调例程
- preoperation 回调例程 WDK 文件系统微筛选器
- postoperation 回调例程 WDK 文件系统微筛选器
- I/O WDK 的文件系统
- 回调例程 WDK 文件系统
- 筛选 I/O 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6711177bb980e9b045bd5bd1670b75103f1af90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385643"
---
# <a name="writing-preoperation-and-postoperation-callback-routines"></a>编写预操作和后操作回调例程


## <span id="ddk_writing_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


在其**DriverEntry**例程，微筛选器驱动程序可以注册最多一个[ **preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)且最多一个[ **postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)每种类型的 I/O 操作所需筛选器。

与传统文件系统筛选器驱动程序，不同的微筛选器驱动程序可以选择哪些类型的 I/O 操作来筛选。 微筛选器驱动程序可以注册为给定类型的 I/O 操作的 preoperation 回调例程，而不注册 postoperation 回调，反之亦然。 微筛选器驱动程序接收的 I/O 操作是操作它已为其注册 preoperation 或 postoperation 回调例程。

一个*preoperation 回调例程*类似于传统筛选器驱动程序模型中的调度例程。 当筛选器管理器处理的 I/O 操作时，它将调用微筛选器驱动程序实例堆栈的已注册一个用于此类型的 I/O 操作中的每个微筛选器驱动程序 preoperation 回调例程。 最顶层微筛选器驱动程序堆栈-也就是说，其实例具有最高的海拔高度-接收该操作第一次。 完成该微筛选器驱动程序在处理该操作后，它将返回到筛选器管理器，然后将该操作传递到下一步最高的微筛选器驱动程序等的操作。 当微筛选器驱动程序实例堆栈中的所有微筛选器驱动程序处理 I/O 操作-除非微筛选器驱动程序已完成 I/O 操作-筛选器管理器将发送到旧的筛选器的操作和文件系统。

一个*postoperation 回调例程*类似于传统筛选器驱动程序模型中的完成例程。 完成处理的 I/O 操作开始时的 I/O 管理器将操作传递到已注册的操作的完成例程的文件系统和旧筛选器。 这些完成例程完成后，筛选器管理器执行完成处理操作。 筛选器管理器然后微筛选器驱动程序实例堆栈的已注册一个用于此类型的 I/O 操作中调用每个微筛选器驱动程序 postoperation 回调的例程。 底部微筛选器驱动程序堆栈-也就是说，其实例所具有最低的海拔高度-接收该操作第一次。 完成该微筛选器驱动程序在处理该操作后，它将其返回给筛选器管理器，然后将该操作传递到下一步最低微筛选器驱动程序中，依次类推。

本部分包括：

[注册 Preoperation 和 Postoperation 回调例程](registering-preoperation-and-postoperation-callback-routines.md)

[筛选微筛选器驱动程序中的 I/O 操作](filtering-i-o-operations-in-a-minifilter-driver.md)

[编写 Preoperation 回调例程](writing-preoperation-callback-routines.md)

[编写 Postoperation 回调例程](writing-postoperation-callback-routines.md)

[对于 I/O 操作修改的参数](modifying-the-parameters-for-an-i-o-operation.md)

[对于 I/O 操作确定缓冲方法](determining-the-buffering-method-for-an-i-o-operation.md)

[对于 I/O 操作中访问用户缓冲区](accessing-the-user-buffers-for-an-i-o-operation.md)

 

 




