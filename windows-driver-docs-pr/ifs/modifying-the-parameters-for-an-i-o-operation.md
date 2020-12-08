---
title: 修改 I/O 操作的参数
description: 修改 I/O 操作的参数
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，修改参数
- postoperation 回调例程 WDK 文件系统微筛选器，修改参数
- 文件系统筛选器驱动程序 WDK，修改 i/o 参数
- 微筛选器驱动程序 WDK，修改 i/o 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b478169759bd0b845330a6ff66ed2eaa97124b89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819045"
---
# <a name="modifying-the-parameters-for-an-io-operation"></a>修改 I/O 操作的参数


## <span id="ddk_modifying_the_parameters_for_an_io_operation_if"></span><span id="DDK_MODIFYING_THE_PARAMETERS_FOR_AN_IO_OPERATION_IF"></span>


微筛选器驱动程序可以修改 i/o 操作的参数。 例如，微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 可以通过更改操作的目标实例，将 i/o 操作重定向到其他卷。 新目标实例必须是同一微筛选器驱动程序的实例，该驱动程序在另一个卷上的相同级别上。

I/o 操作的参数在回调数据 ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构和 I/o 参数块 ([**FLT \_ IO \_ 参数 \_**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block) 块) 操作的结构。 微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 和 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 接收指向 *数据* 输入参数中操作的回调数据结构的指针。 回调数据结构的 *Iopb* 成员是指向 i/o 参数块结构的指针，该结构包含操作的参数。

如果微筛选器驱动程序的 preoperation 回调例程修改了某个 i/o 操作的参数，则微筛选器驱动程序实例堆栈中该微筛选器驱动程序以下的所有微筛选器驱动程序都将在其 preoperation 和 postoperation 回调例程中收到修改后的参数。

当前微筛选器驱动程序的 postoperation 回调例程或筛选器驱动程序实例堆栈中的微筛选器驱动程序之上的任何微筛选器驱动程序都不会收到修改的参数。 在所有情况下，微筛选器驱动程序的 preoperation 和 postoperation 回调例程会接收相同的输入参数值用于给定 i/o 操作。

在修改 i/o 操作的参数后，preoperation 或 postoperation 回调例程必须通过调用 [**FltSetCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)指示它已完成，除非它已更改回调数据结构的 **IoStatus** 字段的内容。 否则，筛选器管理器将忽略对参数值所做的任何更改。 **FltSetCallbackDataDirty** 在 \_ \_ \_ i/o 操作的回调数据结构中设置 FLTFL 回调数据脏标志。 微筛选器驱动程序可以通过调用 [**FltIsCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltiscallbackdatadirty) 来测试此标志，或通过调用 [**FltClearCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclearcallbackdatadirty)将其清除。

如果微筛选器驱动程序的 preoperation 回调例程修改了某个 i/o 操作的参数，则微筛选器驱动程序实例堆栈中该微筛选器驱动程序以下的所有微筛选器驱动程序都将在其 preoperation 和 postoperation 回调例程的 *数据* 和 *FltObjects* 输入参数中收到修改后的参数。  (微筛选器驱动程序不能直接修改 *FltObjects* 参数指向的 [**FLT \_ 相关 \_ 对象**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_related_objects)结构的内容。 但是，如果微筛选器驱动程序修改了 i/o 操作的目标实例或目标文件对象，则筛选器管理器将修改 **Instance** **FileObject** \_ \_ 传递到较低微筛选器驱动程序的 FLT 相关对象结构的对应实例或 FileObject 成员的值。 ) 

虽然微筛选器驱动程序的 preoperation 回调例程进行的任何参数更改不会由微筛选器驱动程序自己的 postoperation 回调例程接收，但 preoperation 回调例程可将有关已更改参数的信息传递给微筛选器驱动程序自己的 postoperation 回调例程。 如果 preoperation 回调例程通过返回 FLT \_ PREOP \_ SUCCESS \_ WITH callback 或 FLT PREOP SYNCHRONIZE 来向下传递堆栈 \_ \_ \_ ，则它可将有关更改的参数值的信息存储到由 *CompletionContext* output 参数指向的微筛选器驱动程序驱动程序定义的结构中。 筛选器管理器将 *CompletionContext* 输入参数中的此结构指针传递到 postoperation 回调例程。

有关 i/o 操作参数的详细信息，请参阅 [**FLT \_ 回调 \_ DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 和 [**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)。

 

