---
title: _Flt_CompletionContext_Outptr_ 注释
description: 在声明文件系统微筛选器预操作回调函数 PFLT_PRE_OPERATION_CALLBACK 时使用_Flt_CompletionContext_Outptr_批注。
ms.assetid: C3B285EA-0DAB-48D4-AE2F-CB4FBB30EF15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 128024ede88da13d6bebe1f984cba627a1f354e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839606"
---
# <a name="_flt_completioncontext_outptr_-annotation"></a>\_Flt\_CompletionContext\_Outptr\_ 批注


在声明文件系统微筛选器预操作回调函数[**PFLT\_\_之前\_操作回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)时，请使用 **\_Flt\_CompletionContext\_Outptr\_** 注释。 将此批注放置在*CompletionContext*参数上。 此批注指示代码分析工具检查*CompletionContext*是否适用于 FLT\_PREOP\_回调\_状态返回值。

如果预操作回调函数（[**PFLT\_pre\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)）返回 FLT\_PREOP\_成功\_使用\_回调或 FLT\_PREOP\_同步*CompletionContext*可以为，也可以不为 NULL。 对于任何其他 FLT\_PREOP\_回调\_状态返回值，则*CompletionContext*必须为 NULL。 *CompletionContext*是筛选器定义的状态，它从筛选器的操作前回调传递到相应的操作后回调函数（[**PFLT\_post\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)）。 仅当筛选器返回的 FLT\_PREOP\_SUCCESS\_\_回调或 FLT\_PREOP\_从其预操作回调函数同步时，才会调用操作后回调。 如果筛选器未将任何状态从其预操作回调函数传递到其操作后回调函数，则*CompletionContext*为 null，因此，其后操作回调函数中的*COMPLETIONCONTEXT*将为 null。 每个单独的筛选器决定是否从预操作回调函数返回*completioncontext*中的状态，因此，每个筛选器均由每个筛选器确定是否应查看其操作后回调中的*completioncontext*才能.

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的示例演示了一个名为*SwapPreReadBuffers*的[**PFLT\_前\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)函数的函数原型。 *CompletionContext*参数接收将传递给操作后回调函数的上下文，并将其声明为 **\_Flt\_CompletionContext\_Outptr\_** 注释。

```ManagedCPlusPlus
FLT_PREOP_CALLBACK_STATUS
SwapPreReadBuffers(
    _Inout_ PFLT_CALLBACK_DATA Data,
    _In_ PCFLT_RELATED_OBJECTS FltObjects,
    _Flt_CompletionContext_Outptr_ PVOID *CompletionContext
    );
```

Specstrings 中定义了 **\_Flt\_CompletionContext\_Outptr\_** 注释。 使用批注可在不增加代码开销或复杂性的情况下添加有价值的错误检查。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**PFLT\_预\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)

[**PFLT\_POST\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)

[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)





