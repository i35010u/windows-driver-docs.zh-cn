---
title: 驱动程序的 IRQL 注释
description: 当驱动程序代码具有 IRQL 批注时，代码分析工具可对函数应运行的级别范围做出更好的推理，并可以更准确地查找错误。
ms.assetid: E4C1D490-BE06-483A-90E4-6F3223E269A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de19094f3914b68ad830e798019ba9965897e51
ms.sourcegitcommit: 9111f8ebcefc41d3a10e8db241d45003a79bec56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864708"
---
# <a name="irql-annotations-for-drivers"></a>驱动程序的 IRQL 注释

所有驱动程序开发人员必须考虑中断请求级别（IRQLs）。 IRQL 是0到31之间的一个整数;被动 \_ 级别、调度 \_ 级别和 APC \_ 级别通常称为符号，另一个由其数值来引用。 引发和降低 IRQL 应遵循严格的堆栈原则。 函数应以调用它的相同 IRQL 返回。 在堆栈中，IRQL 值必须不会递减。 而且，如果不首先引发，函数就不能降低 IRQL。 IRQL 批注用于帮助强制执行这些规则。

当驱动程序代码具有 IRQL 批注时，代码分析工具可对函数应运行的级别范围做出更好的推理，并可以更准确地查找错误。 例如，可以添加批注来指定可调用函数的最大 IRQL;如果调用函数时使用的 IRQL 较高，则代码分析工具可以识别不一致的情况。

应为驱动程序函数注释尽可能多的 IRQL 的信息。 如果提供了其他信息，则它会在对调用函数和被调用函数进行后续检查时帮助代码分析工具。 在某些情况下，添加批注是取消误报的好方法。 某些函数（如实用工具函数）可以在任何 IRQL 上调用。 在这种情况下，没有 IRQL 批注是正确的批注。

在为 IRQL 注释函数时，考虑函数的发展方式（而不仅仅是其当前实现）尤其重要。 例如，实现的函数的运行速度可能比设计器所需的 IRQL 高。 尽管根据代码实际执行的操作为函数添加批注很有吸引力，但设计人员可能会注意到未来的要求，例如，对于某些未来的增强或挂起的系统要求，需要降低最大 IRQL。 批注应从函数设计器的意图派生，而不是从实际实现派生。

您可以使用下表中的注释来指示函数及其参数的正确 IRQL。 在 Wdm .h 中定义 IRQL 值。

|IRQL 批注|说明|
|--- |--- |
|\_IRQL_requires_max_ （_irql_）|_Irql_是函数可调用的最大 irql。|
|\_IRQL_requires_min_ （_irql_）|_Irql_是可调用函数的最小 irql。|
|\_IRQL_requires_ （_irql_）|函数必须以_irql_指定的 irql 输入。|
|\_IRQL_raises_ （_irql_）|函数以指定的_irql_退出，但只能调用它来引发（不小于）当前的 irql。|
|\_IRQL_saves_|带批注的参数将保存当前的 IRQL 以便以后还原。|
|\_IRQL_restores_|带批注的参数包含在函数返回时要还原_IRQL_saves_中的 IRQL 值。|
|\_IRQL_saves_global_ （kind，param）|当前的 IRQL 保存到代码分析工具内部的一个位置，该位置是要从中还原 IRQL 的代码分析工具。 此批注用于批注函数。 该位置由 kind 标识，并由 param 进一步优化。 例如，OldIrql 可以是类型，而 FastMutex 可能是保留了旧 IRQL 值的参数。|
|\_IRQL_restores_global_ （_kind_， _param_）|用 IRQL_saves_global 批注的函数保存的 IRQL 从代码分析工具内部的位置还原。|
|\_IRQL_always_function_min_ （_值_）|IRQL 值是函数可降低 IRQL 的最小值。|
|\_IRQL_always_function_max_ （_值_）|IRQL 值是函数可以将 IRQL 提升到的最大值。|
|\_IRQL_requires_same_|带批注的函数必须以相同的 IRQL 进入和退出。 函数可以更改 IRQL，但必须在退出之前将 IRQL 还原到其原始值。|
|\_IRQL_uses_cancel_|批注参数是应由 DRIVER_CANCEL 回调函数还原的 IRQL 值。 在大多数情况下，请改用 IRQL_is_cancel 注释。|
 

## <a name="span-idannotations_for_driver_cancelspanspan-idannotations_for_driver_cancelspanspan-idannotations_for_driver_cancelspanannotations-for-driver_cancel"></a><span id="Annotations_for_DRIVER_CANCEL"></span><span id="annotations_for_driver_cancel"></span><span id="ANNOTATIONS_FOR_DRIVER_CANCEL"></span>用于取消驱动程序的批注 \_


\_Irql \_ 使用 "取消" \_ \_ ，而 \_ irql 为 " \_ \_ 取消批注" \_ 。 \_IRQL \_ 使用 \_ 取消 \_ 批注仅指定带批注的参数是应由驱动程序 \_ 取消回调函数还原的 IRQL 值。 \_Irql \_ 是 \_ cancel \_ 批注，它是一个包含 IRQL 的复合批注，该批注使用 "取消" \_ \_ \_ \_ 和其他一些批注，以确保驱动程序 \_ 取消回调实用工具函数的正确行为。 默认情况下， \_ irql \_ 使用 \_ 取消 \_ 批注只是偶尔有用; 例如，如果 IRQL 所述的其余责任是取消，则会 \_ \_ \_ \_ 以其他方式完成。

|IRQL 批注|说明|
|--- |--- |
|IRQL_is_cancel|带批注的参数是作为调用 DRIVER_CANCEL 回调函数的一部分传入的 IRQL。 此批注指示函数是一个实用工具，该实用工具是从取消例程调用的，并满足 DRIVER_CANCEL 函数的要求，包括取消旋转锁的释放。|


## <a name="span-idhow_irql_annotations_interactspanspan-idhow_irql_annotations_interactspanspan-idhow_irql_annotations_interactspanhow-irql-annotations-interact"></a><span id="How_IRQL_Annotations_Interact"></span><span id="how_irql_annotations_interact"></span><span id="HOW_IRQL_ANNOTATIONS_INTERACT"></span>IRQL 批注的交互方式


IRQL 参数批注与其他批注都交互，因为使用各种被调用函数设置、重置、保存和还原 IRQL 值。

### <a name="span-idspecifying_maximum_and_minimum_irqlspanspan-idspecifying_maximum_and_minimum_irqlspanspan-idspecifying_maximum_and_minimum_irqlspanspecifying-maximum-and-minimum-irql"></a><span id="Specifying_Maximum_and_Minimum_IRQL"></span><span id="specifying_maximum_and_minimum_irql"></span><span id="SPECIFYING_MAXIMUM_AND_MINIMUM_IRQL"></span>指定最大和最小 IRQL

\_IRQL \_ 要求 \_ max \_ 和 \_ irql 要求使用 \_ \_ min \_ 批注指定不应从大于或小于指定值的 IRQL 调用函数。 例如，当 PREfast 看到一个不会更改 IRQL 的函数调用序列时，如果它找到一个具有 \_ irql 的 \_ \_ 最大值要求最 \_ 小值低于最小值， \_ \_ \_ \_ 则它将报告遇到的第二次调用。 第一次调用时可能会发生此错误;消息指示发生了另一半冲突的位置。

如果函数上的批注提到 IRQL 并且未显式应用 \_ irql \_ \_ ，则要求最大值 \_ ，则代码分析工具将隐式应用批注 \_ irql \_ \_ \_ \_ ，这通常是正确的，很少出现异常。 默认情况下，将其隐式应用于默认值可消除大量的注释混乱，并使例外更为明显。

\_Irql \_ 要求 \_ 最小值 \_ （被动 \_ 级别）批注始终是隐含的，因为 irql 可能不会降低; 因此，不存在有关最小 IRQL 的相应显式规则。 非常少的函数同时具有除调度 \_ 级别和非被动级别以外的下限 \_ 。

某些函数在被调用函数无法安全地在其上提升 IRQL 的上下文中调用，更常见的是，更常见的是，不能安全地降低下面的最小值。 \_Irql \_ 始终 \_ 函数 \_ max \_ 和 \_ IRQL \_ 始终 \_ 功能 \_ 最小 \_ 批注有助于 PREfast 查找意外情况发生的情况。

例如，驱动程序 STARTIO 类型的函数 \_ 以 \_ IRQL 始终是 \_ \_ 函数 \_ min \_ （调度 \_ 级别）进行批注。 这意味着在执行驱动程序 STARTIO 函数的过程中 \_ ，降低调度级别下面的 IRQL 是错误的 \_ 。 其他批注指示该函数必须在调度级别进入和退出 \_ 。

### <a name="span-idspecifying_an_explicit_irqlspanspan-idspecifying_an_explicit_irqlspanspan-idspecifying_an_explicit_irqlspanspecifying-an-explicit-irql"></a><span id="Specifying_an_Explicit_IRQL"></span><span id="specifying_an_explicit_irql"></span><span id="SPECIFYING_AN_EXPLICIT_IRQL"></span>指定显式 IRQL

使用 \_ irql \_ 引发 \_ 或 \_ irql \_ 需要 \_ 批注来帮助 PREfast 更好地报告发现的不一致性需要最 \_ \_ \_ \_ \_ 小值或 irql 要求 \_ \_ 最小值 \_ 注释，因为它知道 IRQL。

\_Irql \_ 引发 \_ 批注表示函数返回，其 IRQL 设置为新值。 使用 \_ IRQL \_ 引发 \_ 批注时，它还会将 winspool.drv maxFunctionIRQL 批注有效地设置 \_ \_ 为相同的 IRQL 值。 但是，如果函数引发比最终值更高的 IRQL，然后将其降低到最终值，则应在 \_ \_ \_ irql 引发批注后添加显式 irql 始终函数 \_ max \_ 批注， \_ \_ \_ 以允许更高的 irql 值。

### <a name="span-idraising_or_lowering_irqlspanspan-idraising_or_lowering_irqlspanspan-idraising_or_lowering_irqlspanraising-or-lowering-irql"></a><span id="Raising_or_Lowering_IRQL"></span><span id="raising_or_lowering_irql"></span><span id="RAISING_OR_LOWERING_IRQL"></span>引发或降低 IRQL

\_IRQL \_ 引发 \_ 批注表示函数必须仅用于引发 irql，而且不能用于降低 irql，即使函数的语法允许这样做也是如此。 KeRaiseIrql 是不应用于降低 IRQL 的函数的示例。

### <a name="span-idsaving_and_restoring_irqlspanspan-idsaving_and_restoring_irqlspanspan-idsaving_and_restoring_irqlspansaving-and-restoring-irql"></a><span id="Saving_and_Restoring_IRQL"></span><span id="saving_and_restoring_irql"></span><span id="SAVING_AND_RESTORING_IRQL"></span>保存和还原 IRQL

使用 " \_ irql \_ 保存" 和 "irql" 将 \_ \_ \_ 还原 \_ 批注，以指示当前的 IRQL （无论是完全知道还是只是大致）保存到批注参数还是从其还原。

有些函数会隐式保存和还原 IRQL。 例如，ExAcquireFastMutex 系统函数将 IRQL 保存在与第一个参数所标识的快速 mutex 对象关联的不透明位置中;对于该快速 mutex 对象，保存的 IRQL 由相应的 ExReleaseFastMutex 函数还原。 若要显式指示这些操作，请使用 \_ IRQL \_ 保存 \_ global \_ 和 \_ irql \_ 还原 \_ 全局 \_ 批注。 *Kind*和*param*参数指示保存 IRQL 值的位置。 不必准确指定保存值的位置，前提是保存和还原值的批注是一致的。

### <a name="span-idmaintaining_the_same_irqlspanspan-idmaintaining_the_same_irqlspanspan-idmaintaining_the_same_irqlspanmaintaining-the-same-irql"></a><span id="Maintaining_the_Same_IRQL"></span><span id="maintaining_the_same_irql"></span><span id="MAINTAINING_THE_SAME_IRQL"></span>维护相同的 IRQL

你应为驱动程序创建的任何函数添加使用 irql 来更改 IRQL 的功能， \_ 以使用 irql \_ 要求 \_ 相同的 \_ 批注或其他一个 如果缺少指示 IRQL 变化的注释，则代码分析工具将为任何不会在输入函数的 IRQL 相同的函数发出警告。 如果需要在 IRQL 中进行更改，请添加相应的批注以禁止显示错误。 如果不打算更改 IRQL，应更正代码。

### <a name="span-idsaving_and_restoring_irql_for_i_o_cancellation_routinesspanspan-idsaving_and_restoring_irql_for_i_o_cancellation_routinesspanspan-idsaving_and_restoring_irql_for_i_o_cancellation_routinesspansaving-and-restoring-irql-for-io-cancellation-routines"></a><span id="Saving_and_Restoring_IRQL_for_I_O_Cancellation_Routines"></span><span id="saving_and_restoring_irql_for_i_o_cancellation_routines"></span><span id="SAVING_AND_RESTORING_IRQL_FOR_I_O_CANCELLATION_ROUTINES"></span>为 i/o 取消例程保存和还原 IRQL

使用 " \_ IRQL \_ 使用 \_ 取消 \_ 批注" 指示批注参数是应由驱动程序取消回调函数还原的 IRQL 值 \_ 。 此批注指示函数是从取消例程调用的实用工具，并完成对驱动程序 cancel 函数所做的要求 \_ （也就是说，它出院调用方的义务）。

例如，以下是驱动程序的声明 \_ 取消回调函数类型。 其中一个参数是此函数应还原的 IRQL。 批注指示 cancel 函数的所有要求。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[用于驱动程序的 SAL 2.0 批注](sal-2-annotations-for-windows-drivers.md)

 

 






