---
title: 对于 I/O 操作修改的参数
description: 对于 I/O 操作修改的参数
ms.assetid: 8e25842f-6f10-412f-8cb2-156bea7d7983
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，修改参数
- postoperation 回调例程 WDK 文件系统微筛选器，修改参数
- 文件系统微筛选器驱动程序 WDK，修改 I/O 参数
- 微筛选器驱动程序 WDK，修改 I/O 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bba99331db7919c3b2c44ada8bbe286f8dfc0ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533167"
---
# <a name="modifying-the-parameters-for-an-io-operation"></a>对于 I/O 操作修改的参数


## <span id="ddk_modifying_the_parameters_for_an_io_operation_if"></span><span id="DDK_MODIFYING_THE_PARAMETERS_FOR_AN_IO_OPERATION_IF"></span>


微筛选器驱动程序可以修改某个 I/O 操作的参数。 例如，微筛选器驱动程序的[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)可重定向的 I/O 操作到另一个卷通过更改该操作的目标实例。 新的目标实例必须是在另一个卷上相同的海拔高度相同的微筛选器驱动程序的实例。

在回调数据中找到某个 I/O 操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构和 I/O 参数块 ([ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)) 操作结构。 在微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)并[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)接收一个指向在操作的回调数据结构*数据*输入的参数。 *Iopb*回调数据结构中的成员是指向 I/O 参数块结构，其中包含该操作的参数。

如果微筛选器驱动程序的 preoperation 回调例程修改某个 I/O 操作的参数，通过下面微筛选器驱动程序实例堆栈中该微筛选器驱动程序的所有微筛选器驱动程序将接收其 preoperation 修改后的参数和postoperation 回调例程。

通过当前微筛选器驱动程序的 postoperation 回调例程或上面微筛选器驱动程序实例堆栈中该微筛选器驱动程序的任何微筛选器驱动程序不接收已修改的参数。 在所有情况下，微筛选器驱动程序的 preoperation 和 postoperation 回调例程接收相同的输入的参数值为指定的 I/O 操作。

修改某个 I/O 操作的参数后，preoperation 或 postoperation 回调例程必须指示，它还执行该操作通过调用[ **FltSetCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff544383)，除非它已更改回调数据结构的内容**IoStatus**字段。 否则，筛选器管理器将忽略对参数值的任何更改。 **FltSetCallbackDataDirty**设置 FLTFL\_回调\_数据\_脏标志在 I/O 操作的回调数据结构。 微筛选器驱动程序可以通过调用来测试此标志[ **FltIsCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff543311)或清除它通过调用[ **FltClearCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff541853).

如果微筛选器驱动程序的 preoperation 回调例程修改某个 I/O 操作的参数，如下微筛选器驱动程序实例堆栈中该微筛选器驱动程序的所有微筛选器驱动程序将接收中的已修改的参数*的数据*并*FltObjects*输入到其 preoperation 和 postoperation 回调例程的参数。 (微筛选器驱动程序不能直接修改的内容[ **FLT\_RELATED\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544816)所指向的结构*FltObjects*参数。 但是，如果微筛选器驱动程序修改的目标实例或 I/O 操作的目标文件对象，筛选器管理器修改的相应值**实例**或**的文件对象**的成员FLT\_RELATED\_对象结构，它是传递到较低微筛选器驱动程序。)

尽管微筛选器驱动程序自己 postoperation 回调例程不接收任何参数做的更改的微筛选器驱动程序的 preoperation 回调例程，则 preoperation 回调例程可以是能够传递已更改的参数有关的信息到微筛选器驱动程序自己 postoperation 回调例程。 如果 preoperation 回调例程通过返回 FLT 通过 I/O 操作在堆栈的下层\_PREOP\_成功\_WITH\_回调或 FLT\_PREOP\_同步，它可以存储有关已更改的参数值所指向的微筛选器驱动程序定义结构的信息*CompletionContext*输出参数。 筛选器管理器将在此结构指针传递*CompletionContext* postoperation 回调例程的输入的参数。

有关 I/O 操作的参数的详细信息，请参阅[ **FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)并[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)。

 

 




