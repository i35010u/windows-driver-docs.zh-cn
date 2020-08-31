---
title: 取消注册微筛选器
description: 取消注册微筛选器
ms.assetid: 4af2d4fd-bfbe-4a75-bbfb-2a1c4b5c2032
keywords:
- 正在取消注册 minifilters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0c0cdb1879ba4ab44e74c3ee8ec21a71af7863f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063218"
---
# <a name="unregistering-the-minifilter"></a>取消注册微筛选器


## <span id="ddk_unregistering_the_minifilter_if"></span><span id="DDK_UNREGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序的 [**FilterUnloadCallback**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback) 例程必须调用 [**FltUnregisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter) 来注销微筛选器驱动程序。 调用 **FltUnregisterFilter** 会导致发生以下情况：

-   取消注册微筛选器驱动程序的回调例程。

-   微筛选器驱动程序的实例已被断开，并为每个微筛选器驱动程序实例调用微筛选器驱动程序的 [**InstanceTeardownStartCallback**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback) 和 **InstanceTeardownCompleteCallback** 例程。

-   如果微筛选器驱动程序设置卷、实例、流或流句柄上的任何上下文，则会删除这些上下文。 如果微筛选器驱动程序已经为给定的上下文类型注册了 [**CleanupContext**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback) 回调例程，则筛选器管理器将在删除上下文之前调用 *CleanupContext* 例程。

如果微筛选器驱动程序的不透明筛选指针上存在未完成的断开引用，则 **FltUnregisterFilter** 将进入等待状态，直到它们被删除。 由于微筛选器驱动程序已调用 [**FltQueueGenericWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem) 将工作项插入系统工作队列，且尚未取消排队和处理该工作项，因此通常会发生未处理断开引用。  (筛选器管理器将在微筛选器驱动程序调用 **FltQueueGenericWorkItem** 时添加断开引用，并在微筛选器驱动程序的工作例程返回时将其删除。 ) 

如果微筛选器驱动程序调用了向微筛选器驱动程序的不透明筛选器指针添加断开引用的任何例程（如 [**FltObjectReference**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltobjectreference) 或 [**FltGetFilterFromInstance**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilterfrominstance)），但后来未调用 [**FltObjectDereference**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltobjectdereference)，则也会发生未完成的断开引用。

 

