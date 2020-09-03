---
title: _Flt_CompletionContext_Outptr_ 注释
description: 在声明文件系统微筛选器预操作回调函数 PFLT_PRE_OPERATION_CALLBACK 时，请使用 _Flt_CompletionContext_Outptr_ 注释。
ms.assetid: C3B285EA-0DAB-48D4-AE2F-CB4FBB30EF15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef38c4c493c98b54664923859f64b5bac61831d8
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384471"
---
# <a name="_flt_completioncontext_outptr_-annotation"></a>\_Flt \_ CompletionContext \_ Outptr \_ 批注


在声明文件系统微筛选器预操作回调函数[**PFLT \_ 预 \_ 操作 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)时，使用** \_ Flt \_ CompletionContext \_ Outptr \_ **批注。 将此批注放置在 *CompletionContext* 参数上。 此批注指示代码分析工具检查 *CompletionContext* 是否适用于 FLT \_ PREOP \_ 回调 \_ 状态返回值。

如果预操作回调函数 ([**PFLT \_ 预 \_ 操作 \_ **](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 回调) 返回 FLT \_ PREOP \_ SUCCESS \_ WITH \_ callback 或 FLT \_ PREOP \_ 同步 *CompletionContext* ，则可能为 NULL，也可能不是 NULL。 对于任何其他 FLT \_ PREOP \_ 回调 \_ 状态返回值， *CompletionContext* 必须为 NULL。 *CompletionContext*是筛选器定义的状态，它从筛选器的操作前回调传递到相应的操作后回调函数 ([**PFLT \_ post \_ 操作 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)) 。 仅当筛选器返回的 FLT \_ PREOP \_ SUCCESS \_ \_ FLT 回调或 \_ PREOP \_ 从其预操作回调函数中同步时，才会调用操作后回调。 如果筛选器未将任何状态从其预操作回调函数传递到其操作后回调函数，则 *CompletionContext* 为 null，因此，其后操作回调函数中的 *COMPLETIONCONTEXT* 将为 null。 每个单独的筛选器决定是否从预操作回调函数返回 *completioncontext* 中的状态，因此，每个筛选器均由每个筛选器确定是否应查看其操作后回调函数中的 *completioncontext* 。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的示例演示了名为*SwapPreReadBuffers*的[**PFLT \_ 预 \_ 操作 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)函数的函数原型。 *CompletionContext*参数接收将传递给操作后回调函数的上下文，并通过** \_ Flt \_ CompletionContext \_ Outptr \_ **批注进行声明。

```ManagedCPlusPlus
FLT_PREOP_CALLBACK_STATUS
SwapPreReadBuffers(
    _Inout_ PFLT_CALLBACK_DATA Data,
    _In_ PCFLT_RELATED_OBJECTS FltObjects,
    _Flt_CompletionContext_Outptr_ PVOID *CompletionContext
    );
```

** \_ Flt \_ CompletionContext \_ Outptr \_ **批注是在 specstrings 中定义的。 使用批注可在不增加代码开销或复杂性的情况下添加有价值的错误检查。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**PFLT \_ 预 \_ 操作 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)

[**PFLT \_ POST \_ 操作 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)

[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)