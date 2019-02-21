---
title: 驱动程序的 IRQL 批注
description: 当驱动程序代码的 IRQL 批注时，代码分析工具可使的范围级别的函数应运行和的详细信息可以准确地找到错误的更好地推断。
ms.assetid: E4C1D490-BE06-483A-90E4-6F3223E269A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d184f7742da975a6375884141aa9f33f2e033e4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533422"
---
# <a name="irql-annotations-for-drivers"></a>驱动程序的 IRQL 批注

当驱动程序代码的 IRQL 批注时，代码分析工具可使的范围级别的函数应运行和的详细信息可以准确地找到错误的更好地推断。 例如，可以添加指定的可调用的函数; 最大 IRQL 的批注如果在更高版本的 IRQL 调用的函数，代码分析工具可以识别不一致。

所有驱动程序开发人员必须考虑中断请求级别 (于 Irql)。 IRQL 是 0 到 31; 之间的整数被动\_级别、 调度\_级别和 APC\_级别通常称为种，和其他人通过其数字值。 提高和降低 IRQL 应遵循严格的堆栈规则。 函数应力求在相同的 IRQL 的调用返回。 IRQL 值必须为非减少堆栈中。 和一个函数不能降低 IRQL 不会第一个生成它。 IRQL 批注旨在帮助强制实施这些规则。

当驱动程序代码的 IRQL 批注时，代码分析工具可使的范围级别的函数应运行和的详细信息可以准确地找到错误的更好地推断。 例如，可以添加指定的可调用的函数; 最大 IRQL 的批注如果在更高版本的 IRQL 调用的函数，代码分析工具可以识别不一致。

驱动程序函数应使用尽可能多的信息可能适合 IRQL 有关注释。 如果提供了其他信息，它可帮助在调用函数和被调用的函数的后续检查的代码分析工具。 在某些情况下，添加批注是取消假正的好方法。 一些函数，如的实用工具函数，可以调用的任何 irql。 在这种情况下，无任何 IRQL 批注是正确的批注。

对函数进行批注的 IRQL，时，尤其要考虑如何函数可能会演变，而不仅仅是其当前的实现。 例如，实现的函数可能正常工作，在更高版本的 IRQL 比预期的设计器。 虽然很容易使人批注函数基于代码的实际作用，但在设计器可能在未来的需求，例如需要降低一些以后可增强功能或挂起的系统要求的最大 IRQL 注意。 批注应派生自函数设计器中，不能从实际实现的意图。

可以使用下表中的批注以指示正确的 IRQL 对函数和其参数。 IRQL 值中 wdm.h 中定义。

|IRQL 批注|描述|
|--- |--- |
|\_IRQL_requires_max_(_irql_)|_Irql_是最大的 IRQL 会调用该函数。|
|\_IRQL_requires_min_(_irql_)|_Irql_是最小的 IRQL 会调用该函数。|
|\_IRQL_requires_(_irql_)|该函数必须输入在指定的 IRQL _irql_。|
|\_IRQL_raises_(_irql_)|在指定的函数退出_irql_，但它仅可以调用以引发 （不降低） 当前 IRQL。|
|\_IRQL_saves_|带批注的参数将保存当前 IRQL，若要在以后还原。|
|\_IRQL_restores_|带批注的参数包含 IRQL 值从_IRQL_saves_这是要还原在函数返回时。|
|\_IRQL_saves_global_ （类型、 参数）|当前 IRQL 会保存到的位置是要还原的 IRQL 的代码分析工具的内部。 此批注用于批注的函数。 位置是由类型标识，通过 param 进一步优化。 例如，OldIrql 可能是类型，并且 FastMutex 可能持有该旧的 IRQL 值的参数。|
|\_IRQL_restores_global_(_kind_, _param_)|函数使用 IRQL_saves_global 批注保存 IRQL 恢复是内部的代码分析工具的位置中。|
|\_IRQL_always_function_min_(_value_)|IRQL 值是到该函数可以降低 IRQL 的最小值。|
|\_IRQL_always_function_max_(_value_)|IRQL 值是到该函数可以引发 IRQL 的最大值。|
|\_IRQL_requires_same_|带批注的函数必须输入，并在相同的 IRQL 退出。 该函数可以更改 IRQL，但它必须在退出之前将 IRQL 恢复到其原始值。|
|\_IRQL_uses_cancel_|带批注的参数是 DRIVER_CANCEL 回调函数应还原的 IRQL 值。 在大多数情况下，改用 IRQL_is_cancel 批注。|
 

## <a name="span-idannotationsfordrivercancelspanspan-idannotationsfordrivercancelspanspan-idannotationsfordrivercancelspanannotations-for-drivercancel"></a><span id="Annotations_for_DRIVER_CANCEL"></span><span id="annotations_for_driver_cancel"></span><span id="ANNOTATIONS_FOR_DRIVER_CANCEL"></span>驱动程序的批注\_取消


没有之间的差异\_IRQL\_使用\_取消\_并\_IRQL\_是\_取消\_批注。 \_IRQL\_使用\_取消\_批注只需指定带批注的参数，是应由驱动程序还原的 IRQL 值\_取消回调函数。 \_IRQL\_是\_取消\_批注是组成的复合批注\_IRQL\_使用\_取消\_另外几个其他批注确保驱动程序的正确行为\_取消回调实用工具函数。 其本身而言， \_IRQL\_使用\_取消\_批注只是偶尔会非常有用; 例如，如果义务的其余部分所述\_IRQL\_是\_取消\_已满足某种其他方式。

|IRQL 批注|描述|
|--- |--- |
|IRQL_is_cancel|带批注的参数是调用的对 DRIVER_CANCEL 回调函数的一部分传入 IRQL。 此批注指示该函数是一个实用程序，从取消例程的调用和完成 DRIVER_CANCEL 函数，其中包括取消自旋锁的版本的要求。|


## <a name="span-idhowirqlannotationsinteractspanspan-idhowirqlannotationsinteractspanspan-idhowirqlannotationsinteractspanhow-irql-annotations-interact"></a><span id="How_IRQL_Annotations_Interact"></span><span id="how_irql_annotations_interact"></span><span id="HOW_IRQL_ANNOTATIONS_INTERACT"></span>如何进行交互的 IRQL 批注


IRQL 参数批注与多个其他批注其他每个交互，因为 IRQL 值是设置、 重置、 保存和还原由各种调用的函数。

### <a name="span-idspecifyingmaximumandminimumirqlspanspan-idspecifyingmaximumandminimumirqlspanspan-idspecifyingmaximumandminimumirqlspanspecifying-maximum-and-minimum-irql"></a><span id="Specifying_Maximum_and_Minimum_IRQL"></span><span id="specifying_maximum_and_minimum_irql"></span><span id="SPECIFYING_MAXIMUM_AND_MINIMUM_IRQL"></span>指定最大和最小的 IRQL

\_IRQL\_需要\_max\_并\_IRQL\_需要\_最小值\_批注指定，该函数不应调用从是 IRQL高于或低于指定的值。 例如，当 PREfast 发现一系列函数调用，不要更改 irql，因此如果找到具有\_IRQL\_要求\_max\_低于值附近\_IRQL\_需要\_min\_，在遇到第二次调用将会报告警告。 第一次调用; 实际上可能会出现此错误该消息指示发生冲突的另一半的位置。

如果在函数上的批注提及 IRQL 和显式不适用于\_IRQL\_要求\_max\_，代码分析工具隐式应用批注\_IRQL\_需要\_最大\_(调度\_级别)，这是除少数例外通常正确。 隐式应用此为默认值可以消除许多批注混乱，并使异常更可见。

\_IRQL\_要求\_min\_(被动\_级别) 始终隐式批注，因为 IRQL 可以没有较低的; 因此，没有相应的显式规则最小的 IRQL 有关。 很少的函数具有两个上限以外调度\_级别和下限为非被动\_级别。

某些函数进行调用的上下文中调用的函数不能安全地提升 IRQL 一些最大值或，更多时候，不能安全地将它降级低于一些最小值。 \_IRQL\_始终\_函数\_max\_并\_IRQL\_始终\_函数\_min\_批注帮助 PREfast查找发生这种情况会无意中。

例如，类型驱动程序的函数\_STARTIO 批注与\_IRQL\_始终\_函数\_min\_(调度\_级别)。 这意味着，在驱动程序的执行期间\_STARTIO 函数是错误降低下面调度 IRQL\_级别。 其他批注指示该函数必须输入并在调度退出\_级别。

### <a name="span-idspecifyinganexplicitirqlspanspan-idspecifyinganexplicitirqlspanspan-idspecifyinganexplicitirqlspanspecifying-an-explicit-irql"></a><span id="Specifying_an_Explicit_IRQL"></span><span id="specifying_an_explicit_irql"></span><span id="SPECIFYING_AN_EXPLICIT_IRQL"></span>指定显式 IRQL

使用\_IRQL\_引发\_或\_IRQL\_需要\_批注以更好地帮助 PREfast 报告发现的不一致\_IRQL\_需要\_最大\_或\_IRQL\_要求\_min\_批注因为它然后知道 IRQL。

\_IRQL\_引发\_批注指示，函数会返回与 IRQL 设置为新值。 当你使用\_IRQL\_引发\_批注，它还将有效设置\_drv\_maxFunctionIRQL 批注为相同的 IRQL 值。 但是，如果函数引发的最终值高于 IRQL，然后将其降低到最后一个值，则应添加显式\_IRQL\_始终\_函数\_max\_批注以下\_IRQL\_引发\_要允许更高版本的 IRQL 值批注。

### <a name="span-idraisingorloweringirqlspanspan-idraisingorloweringirqlspanspan-idraisingorloweringirqlspanraising-or-lowering-irql"></a><span id="Raising_or_Lowering_IRQL"></span><span id="raising_or_lowering_irql"></span><span id="RAISING_OR_LOWERING_IRQL"></span>引发或降低 IRQL

\_IRQL\_引发\_批注指示该函数必须使用只是为了引发 IRQL 和必须不能降低 irql，因此即使函数的语法将允许它。 KeRaiseIrql 是不应使用较低的 IRQL 在函数示例。

### <a name="span-idsavingandrestoringirqlspanspan-idsavingandrestoringirqlspanspan-idsavingandrestoringirqlspansaving-and-restoring-irql"></a><span id="Saving_and_Restoring_IRQL"></span><span id="saving_and_restoring_irql"></span><span id="SAVING_AND_RESTORING_IRQL"></span>保存和还原的 IRQL

使用\_IRQL\_将保存\_并\_IRQL\_还原\_批注以指示当前 IRQL （无论它已知的完全或仅可大概） 是保存到或从还原带批注的参数。

某些函数保存，并将 irql 恢复隐式。 例如，ExAcquireFastMutex 系统函数将保存 IRQL 与第一个参数标识; 的快速互斥体对象关联的不透明位置已保存的 IRQL 被还原该快速互斥体对象的相应 ExReleaseFastMutex 函数。 若要显式指示这些操作，使用\_IRQL\_将保存\_全局\_并\_IRQL\_还原\_全局\_批注。 *种类*并*param*参数指示的 IRQL 值的保存位置。 保存值的位置无需精确指定，只要保存和还原值的批注一致。

### <a name="span-idmaintainingthesameirqlspanspan-idmaintainingthesameirqlspanspan-idmaintainingthesameirqlspanmaintaining-the-same-irql"></a><span id="Maintaining_the_Same_IRQL"></span><span id="maintaining_the_same_irql"></span><span id="MAINTAINING_THE_SAME_IRQL"></span>维护相同的 IRQL

应该对您的驱动程序创建的更改所使用的 IRQL 任何函数进行批注\_IRQL\_要求\_相同\_批注或某个其他的 IRQL 批注以指示在 IRQL 更改为预期。 如果没有指示 IRQL 中的任何更改的批注，代码分析工具将发出警告不会退出在相同的 IRQL 输入函数的任何函数。 如果在 IRQL 中的更改的目的是，添加要取消显示该错误的相应批注。 如果不应在 IRQL 更改，则应纠正代码。

### <a name="span-idsavingandrestoringirqlforiocancellationroutinesspanspan-idsavingandrestoringirqlforiocancellationroutinesspanspan-idsavingandrestoringirqlforiocancellationroutinesspansaving-and-restoring-irql-for-io-cancellation-routines"></a><span id="Saving_and_Restoring_IRQL_for_I_O_Cancellation_Routines"></span><span id="saving_and_restoring_irql_for_i_o_cancellation_routines"></span><span id="SAVING_AND_RESTORING_IRQL_FOR_I_O_CANCELLATION_ROUTINES"></span>保存和还原的 I/O 取消例程的 IRQL

使用\_IRQL\_使用\_取消\_批注以指示该带批注的参数是应由驱动程序还原的 IRQL 值\_取消回调函数。 此批注指示该函数是一个实用工具，从取消例程调用和完成在驱动程序所做的要求\_CANCEL 函数 (即，discharges 调用方的义务)。

例如，以下是该驱动程序的声明\_取消回调函数类型。 其中一个参数是此函数应还原 IRQL。 表示批注指明所有取消函数的要求。

```ManagedCPlusPlus
// Define driver cancel routine type.  //    
__drv_functionClass(DRIVER_CANCEL)  
_Requires_lock_held_(_Global_cancel_spin_lock_)  
_Releases_lock_(_Global_cancel_spin_lock_)  
_IRQL_requires_min_(DISPATCH_LEVEL)  
_IRQL_requires_(DISPATCH_LEVEL)  
typedef  
VOID  
DRIVER_CANCEL (  
    _Inout_ struct _DEVICE_OBJECT *DeviceObject,  
    _Inout_ _IRQL_uses_cancel_ struct _IRP *Irp  
    );  
  
typedef DRIVER_CANCEL *PDRIVER_CANCEL;  
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[SAL 2.0 注释驱动程序](sal-2-annotations-for-windows-drivers.md)

 

 






