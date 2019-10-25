---
title: 修改 I/O 操作的参数
description: 修改 I/O 操作的参数
ms.assetid: 8e25842f-6f10-412f-8cb2-156bea7d7983
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，修改参数
- postoperation 回调例程 WDK 文件系统微筛选器，修改参数
- 文件系统筛选器驱动程序 WDK，修改 i/o 参数
- 微筛选器驱动程序 WDK，修改 i/o 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 722c396c4169b887d11958e104c00fe3f903690c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841120"
---
# <a name="modifying-the-parameters-for-an-io-operation"></a>修改 I/O 操作的参数


## <span id="ddk_modifying_the_parameters_for_an_io_operation_if"></span><span id="DDK_MODIFYING_THE_PARAMETERS_FOR_AN_IO_OPERATION_IF"></span>


微筛选器驱动程序可以修改 i/o 操作的参数。 例如，微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)可以通过更改操作的目标实例，将 i/o 操作重定向到其他卷。 新目标实例必须是同一微筛选器驱动程序的实例，该驱动程序在另一个卷上的相同级别上。

I/o 操作的参数位于操作的回调数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构和 i/o 参数块（[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)）结构中。 微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)和[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)接收指向*数据*输入参数中操作的回调数据结构的指针。 回调数据结构的*Iopb*成员是指向 i/o 参数块结构的指针，该结构包含操作的参数。

如果微筛选器驱动程序的 preoperation 回调例程修改了 i/o 操作的参数，则微筛选器驱动程序实例堆栈中该微筛选器驱动程序以下的所有微筛选器驱动程序都将在其 preoperation 中收到修改后的参数，并postoperation 回调例程。

当前微筛选器驱动程序的 postoperation 回调例程或筛选器驱动程序实例堆栈中的微筛选器驱动程序之上的任何微筛选器驱动程序都不会收到修改的参数。 在所有情况下，微筛选器驱动程序的 preoperation 和 postoperation 回调例程会接收相同的输入参数值用于给定 i/o 操作。

在修改 i/o 操作的参数后，preoperation 或 postoperation 回调例程必须通过调用[**FltSetCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)指示它已完成，除非它已更改回调数据结构**的IoStatus**字段。 否则，筛选器管理器将忽略对参数值所做的任何更改。 **FltSetCallbackDataDirty**在 i/o 操作的回调数据结构中设置 FLTFL\_回调\_数据\_脏标志。 微筛选器驱动程序可以通过调用[**FltIsCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltiscallbackdatadirty)来测试此标志，或通过调用[**FltClearCallbackDataDirty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclearcallbackdatadirty)将其清除。

如果微筛选器驱动程序的 preoperation 回调例程修改了 i/o 操作的参数，则微筛选器驱动程序实例堆栈中该微筛选器驱动程序以下的所有微筛选器驱动程序都将接收*数据*中修改后的参数和*FltObjects* preoperation 和 postoperation 回调例程的输入参数。 （微筛选器驱动程序不能直接修改由*FltObjects*参数指向的[**FLT\_相关\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_related_objects)结构的内容。 但是，如果微筛选器驱动程序修改了 i/o 操作的目标实例或目标文件对象，则筛选器管理器将修改 FLT\_相关\_对象的相应**实例**或**FileObject**成员的值。传递给降低微筛选器驱动程序的结构。）

虽然微筛选器驱动程序的 preoperation 回调例程进行的任何参数更改不会被微筛选器驱动程序自己的 postoperation 回调例程接收，但 preoperation 回调例程可以传递有关已更改参数的信息到微筛选器驱动程序自己的 postoperation 回调例程。 如果 preoperation 回调例程通过返回 FLT\_PREOP\_SUCCESS\_，并\_回拨或 FLT\_PREOP\_SYNCHRONIZE 来向下传递 i/o 操作，则可以存储已更改参数的相关信息值转换为由*CompletionContext* output 参数指向的微筛选器驱动程序驱动程序的结构。 筛选器管理器将*CompletionContext*输入参数中的此结构指针传递到 postoperation 回调例程。

有关 i/o 操作参数的详细信息，请参阅[**FLT\_回调\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) and [**FLT\_IO\_参数\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)。

 

 




