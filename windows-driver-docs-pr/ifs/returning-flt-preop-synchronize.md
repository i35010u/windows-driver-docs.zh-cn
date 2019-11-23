---
title: 返回 FLT_PREOP_SYNCHRONIZE
description: 返回 FLT_PREOP_SYNCHRONIZE
ms.assetid: b1331f8d-e230-45b2-be1b-f85d85557350
keywords:
- FLT_PREOP_SYNCHRONIZE
- 同步 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96fa564840fc874ecd3e53923ece3122c86b6a7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840992"
---
# <a name="returning-flt_preop_synchronize"></a>返回 FLT\_PREOP\_同步


## <span id="ddk_returning_flt_preop_synchronize_if"></span><span id="DDK_RETURNING_FLT_PREOP_SYNCHRONIZE_IF"></span>


如果微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)通过返回 FLT\_PREOP\_SYNCHRONIZE 来同步 i/o 操作，筛选器管理器将在 i/o 完成期间调用微筛选器驱动程序的[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)。

筛选器管理器将在与 preoperation 回调相同的线程上下文中调用微筛选器驱动程序的 postoperation 回调例程，介于 IRQL &lt;= APC\_级别。 （请注意，此线程上下文不一定是起始线程的上下文。）

**请注意**   如果微筛选器驱动程序的 preoperation 回调例程返回 FLT\_PREOP\_同步，但微筛选器驱动程序未注册操作的 postoperation 回调例程，则系统会在已检查的内部版本中断言。

 

如果微筛选器驱动程序的 preoperation 回调例程返回 FLT\_PREOP\_SYNCHRONIZE，则它可以在其*CompletionContext* output 参数中返回非 NULL 值。 此参数是一个可选的上下文指针，它传递到相应的 postoperation 回调例程。 Postoperation 回调例程在其*CompletionContext*输入参数中接收此指针。

微筛选器驱动程序的 preoperation 回调例程应返回 FLT\_PREOP\_只同步基于 IRP 的 i/o 操作。 但是，可以为其他操作类型返回此状态值。 如果为不是基于 IRP 的 i/o 操作的 i/o 操作返回，则筛选器管理器会将此返回值视为 FLT\_PREOP\_SUCCESS\_与\_回调一起使用。 若要确定某个操作是否是基于 IRP 的 i/o 操作，请使用[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))宏。

微筛选器驱动程序不应返回 FLT\_PREOP\_为创建操作同步，因为这些操作已经被筛选器管理器同步。 如果微筛选器驱动程序已为 IRP\_MJ 注册了 preoperation 和 postoperation 回调例程\_创建操作，则会在与预先创建回调例程相同的线程上下文中的 IRQL = 被动\_级别调用创建后回调例程。

微筛选器驱动程序绝不能返回 FLT\_PREOP\_同步异步读取或写入操作。 这样做可能会严重降低微筛选器驱动程序和系统性能，甚至可能会导致死锁（例如，已修改的页面写入器线程被阻止）。 在返回 FLT\_PREOP\_为基于 IRP 的读取或写入操作进行同步之前，微筛选器驱动程序应通过调用[**FltIsOperationSynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisoperationsynchronous)来验证该操作是否同步。

无法同步以下类型的 i/o 操作：

-   Oplock 文件系统控制（FSCTL）操作（**MajorFunction**是 IRP\_MJ\_文件\_系统\_控件;**FsControlCode**是[**FSCTL\_REQUEST\_FILTER\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-filter-oplock)、 [**FSCTL\_请求\_BATCH\_oplock**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-batch-oplock)、 [**FSCTL\_请求\_oplock\_level\_1**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock-level-1)或[**FSCTL\_请求\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock-level-2)\_\_级别。）

-   通知更改目录操作（**MajorFunction**为 IRP\_MJ\_DIRECTORY\_控件;**MinorFunction**是 IRP\_MN\_通知\_更改\_目录。）

-   字节范围锁请求（**MajorFunction**是 IRP\_MJ\_锁定\_控件;**MinorFunction**是 IRP\_MN\_锁定。）

不能为这些操作返回 FLT\_PREOP\_同步。

 

 




