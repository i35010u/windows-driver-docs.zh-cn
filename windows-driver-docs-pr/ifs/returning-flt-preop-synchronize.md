---
title: 返回 FLT_PREOP_SYNCHRONIZE
description: 返回 FLT_PREOP_SYNCHRONIZE
keywords:
- FLT_PREOP_SYNCHRONIZE
- 同步 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ba5bab54f98e1d349231eb57c76daccf6d5e1e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838909"
---
# <a name="returning-flt_preop_synchronize"></a>返回 FLT \_ PREOP \_ SYNCHRONIZE


## <span id="ddk_returning_flt_preop_synchronize_if"></span><span id="DDK_RETURNING_FLT_PREOP_SYNCHRONIZE_IF"></span>


如果微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 通过返回 FLT PREOP SYNCHRONIZE 来同步 i/o 操作 \_ \_ ，则筛选器管理器将在 i/o 完成期间调用微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 。

筛选器管理器将在与 preoperation 回调相同的线程上下文中调用微筛选器驱动程序的 postoperation 回调例程，以 IRQL &lt; = APC \_ 级别。  (请注意，此线程上下文不一定是起始线程的上下文。 ) 

**注意**   如果微筛选器驱动程序的 preoperation 回调例程返回 FLT \_ PREOP \_ SYNCHRONIZE，但微筛选器驱动程序未为操作注册 postoperation 回调例程，则系统会在已检查的内部版本中断言。

 

如果微筛选器驱动程序的 preoperation 回调例程返回 FLT \_ PREOP \_ SYNCHRONIZE，则它可以在其 *CompletionContext* output 参数中返回非 NULL 值。 此参数是一个可选的上下文指针，它传递到相应的 postoperation 回调例程。 Postoperation 回调例程在其 *CompletionContext* 输入参数中接收此指针。

微筛选器驱动程序的 preoperation 回调例程应 \_ \_ 为基于 IRP 的 i/o 操作返回 FLT PREOP SYNCHRONIZE。 但是，可以为其他操作类型返回此状态值。 如果为不是基于 IRP 的 i/o 操作的 i/o 操作返回，则筛选器管理器会将此返回值视为 FLT \_ PREOP \_ SUCCESS 是否成功 \_ \_ 。 若要确定某个操作是否为基于 IRP 的 i/o 操作，请使用 [**FLT \_ 为 \_ irp \_ 操作**](/previous-versions/ff544654(v=vs.85)) 宏。

微筛选器驱动程序不 \_ 应 \_ 为创建操作返回 FLT PREOP 同步，因为这些操作已由筛选器管理器同步。 如果微筛选器驱动程序已为 IRP MJ CREATE 操作注册了 preoperation 和 postoperation 回调例程，则在与 \_ \_ \_ 预先创建回调例程相同的线程上下文中，将在 IRQL = 被动级别调用创建后回调例程。

微微筛选器驱动程序绝不能返回 FLT \_ PREOP \_ 同步异步读取或写入操作。 这样做可能会严重降低微筛选器驱动程序和系统性能，甚至可能会导致死锁（例如，已修改的页面写入器线程被阻止）。 在 \_ \_ 为基于 IRP 的读取或写入操作返回 FLT PREOP 同步之前，微筛选器驱动程序应通过调用 [**FltIsOperationSynchronous**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisoperationsynchronous)来验证该操作是否同步。

无法同步以下类型的 i/o 操作：

-   Oplock 文件系统控制 (FSCTL) 操作 (**MajorFunction** 为 IRP \_ MJ \_ 文件 \_ 系统 \_ 控制; **FsControlCode** 是 [**FSCTL \_ 请求 \_ 筛选器 \_ oplock**](./fsctl-request-filter-oplock.md)、 [**FSCTL \_ 请求 \_ 批处理 \_ oplock**](./fsctl-request-batch-oplock.md)、 [**FSCTL \_ 请求 \_ oplock \_ level \_ 1**](./fsctl-request-oplock-level-1.md)或 [**FSCTL \_ request \_ oplock \_ level \_ 2**](./fsctl-request-oplock-level-2.md)。 ) 

-    (**MajorFunction** 为 IRP \_ MJ \_ 目录控制通知更改目录操作 \_ ; **MinorFunction** 为 IRP \_ MN \_ 通知 \_ 更改 \_ 目录。 ) 

-    (**MajorFunction** 的字节范围锁请求为 IRP \_ MJ \_ lock \_ 控制; **MinorFunction** 为 IRP \_ MN \_ LOCK。 ) 

\_ \_ 不能为这些操作返回 FLT PREOP SYNCHRONIZE。

 

