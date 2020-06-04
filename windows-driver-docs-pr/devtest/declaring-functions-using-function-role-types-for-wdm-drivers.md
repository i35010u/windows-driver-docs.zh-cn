---
title: 使用 WDM 驱动程序的函数角色类型来声明函数
description: 使用 WDM 驱动程序的函数角色类型来声明函数
ms.assetid: 3260b53e-82be-4dbc-8ac5-d0e52de77f9d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8710aff79de9d8772229a6b3b38c8b2efeb07f16
ms.sourcegitcommit: a386cf5ac5a157dfe1041e7c23b6e70a33ca2704
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330061"
---
# <a name="declaring-functions-using-function-role-types-for-wdm-drivers"></a>使用 WDM 驱动程序的函数角色类型来声明函数

> [!NOTE]
> 从 Windows 10 版本2004开始，[静态驱动程序验证程序](https://review.docs.microsoft.com/en-us/windows-hardware/drivers/devtest/static-driver-verifier)（SDV）不再需要批注来识别 WDM 驱动程序的调度例程的角色类型。  请按照本页的*基本和高级初始化*部分中的指导进行操作。

若要在分析 WDM 驱动程序时通知 SDV 驱动程序的入口点，必须使用函数角色类型声明声明函数。 在 Wdm .h 中定义函数角色类型。 WDM 驱动程序中*DriverEntry*例程的每个入口点都必须通过指定相应的角色类型进行声明。 角色类型是预定义的 typedef，它们对应于 WDM 驱动程序中的已识别入口点。

例如，若要为驱动程序的[**unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程（称为*CsampUnload*）创建函数角色类型声明，请使用预定义的 typedef 驱动程序 \_ 卸载角色类型声明。 函数角色类型声明必须出现在函数定义之前。

```
DRIVER_UNLOAD CsampUnload;
```

*CsampUnload*函数的定义保持不变：

```
VOID
CsampUnload(
    IN PDRIVER_OBJECT DriverObject
    )
{
    ...
}
```

SDV 识别下表中显示的入口点的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WDM 函数角色类型</th>
<th align="left">WDM 例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DRIVER_INITIALIZE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;em&gt;DriverEntry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><em>DriverEntry</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_STARTIO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio" data-raw-source="[&lt;em&gt;StartIO&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)"><em>StartIO</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_UNLOAD</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)"><em>[</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_ADD_DEVICE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong><em>Dispatch_type</em>（</strong> <em>类型</em> <strong>）</strong> DRIVER_DISPATCH</td>
<td align="left"><p>驱动程序使用的调度例程。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines" data-raw-source="[Writing Dispatch Routines](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)">编写调度例程</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_COMPLETION_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a></p>
<p><em>IoCompletion</em>例程是通过调用<em>IoSetCompletionRoutine</em>或<em>IoSetCompletionRoutineEx</em> ，并将函数指针作为第二个参数传递到<em>IoCompletion</em>例程来设置的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_CANCEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel" data-raw-source="[&lt;em&gt;Cancel&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)"><em>取消</em></a></p>
<p>通过调用<strong>IoSetCancelRoutine</strong>并将该函数指针作为函数的第二个参数传递到该函数的第二个参数，可设置<strong>取消</strong>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_DPC_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)"><em>DpcForIsr</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)"><em>DpcForIsr</em></a>例程通过调用<em>IoInitializeDpcRequest</em>并将函数指针作为第二个参数传递到<em>DpcForIsr</em>例程来注册。 若要将 DPC 排队，请使用同一 DPC 对象从 ISR 例程调用<em>IoQueueDpc</em> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KDEFERRED_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)"><em>CustomDpc</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)"><em>CustomDpc</em></a>例程是通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc" data-raw-source="[&lt;strong&gt;KeInitializeDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)"><strong>KeInitializeDpc</strong></a>并将函数指针作为第二个参数传递到<em>CustomDpc</em>来设置的。 若要对驱动程序的<em>CustomDpc</em>进行排队，请使用同一 DPC 对象从 ISR 例程调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc" data-raw-source="[&lt;strong&gt;KeInsertQueueDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)"><strong>KeInsertQueueDpc</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSERVICE_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)"><em>InterruptService</em></a></p>
<p>如有必要，InterruptService 例程（ISR）会为设备中断和计划接收的数据的中断后处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>REQUEST_POWER_COMPLETE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-request_power_complete" data-raw-source="[&lt;em&gt;PowerCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-request_power_complete)"><em>PowerCompletion</em></a>回调例程完成对 power IRP 的处理。 如果驱动程序在所有其他驱动程序都完成 IRP 之后需要执行其他任务，则驱动程序将在调用分配 IRP 的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)"><strong>PoRequestPowerIrp</strong></a>例程期间注册一个<em>PowerCompletion</em>回调例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WORKER_THREAD_ROUTINE</p></td>
<td align="left"><p><em>例程所返回的值</em></p>
<p><em>例程</em>是在<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl" data-raw-source="[&lt;strong&gt;ExInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)"><strong>ExInitializeWorkItem</strong></a>函数的第二个参数中指定的回调例程。</p>
<p>仅当驱动程序调用<strong>ExQueueWorkItem</strong>将工作项添加到系统队列时，才应以这种方式声明<em>例程</em>。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idannotating_driver_dispatch_routinesspanspan-idannotating_driver_dispatch_routinesspandeclaring-driver-dispatch-routines"></a><span id="annotating_driver_dispatch_routines"></span><span id="ANNOTATING_DRIVER_DISPATCH_ROUTINES"></span>声明驱动程序调度例程

从 Windows 10 版本2004开始，调度例程的函数角色类型声明通过其 IRP 类别根据 WDM 驱动程序的 DriverEntry 例程中的 >DriverObject MajorFunction 表的初始化自动进行优化。  

驱动程序 Foo 必须使用基本或高级声明样式来完成角色声明，才能符合 SDV。  

#### <a name="basic-and-advanced-initializations"></a>基本和高级初始化

在下面的示例中可以看到基本样式（请注意，调度例程名称 FooCreate 和 FooCleanup 只是示例，可以使用任何适当的名称）：

```
DriverObject->MajorFunction[IRP_MJ_CREATE] = FooCreate; //Basic style
DriverObject->MajorFunction[IRP_MJ_CLEANUP] = FooCleanup;
```

可以采用更高级的方法来缩短所需的列表。  虽然同一调度例程用于多个 IRP 类别，但驱动程序可以通过这种方式编码两次初始化：

```
DriverObject->MajorFunction[IRP_MJ_CREATE] = 
DriverObject->MajorFunction[IRP_MJ_CLEANUP] = FooCreateCleanup; // Advanced style for a multi-role dispatch routine 
```

为了使驱动程序能够正常运行 SDV，**驱动程序必须仅使用上面所示的*基本*或*高级*样式**。  如果未使用这两种方法中的一种，则驱动程序上的 SDV 验证**将无法按预期方式工作**。

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>函数参数和函数角色类型

根据 C 编程语言的要求，在函数定义中使用的参数类型必须与函数原型的参数类型匹配，在本例中为函数角色类型。 SDV 依赖于用于分析的函数签名，并忽略其签名不匹配的函数。

例如，你应该使用 IO [**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) \_ 完成 \_ 例程函数角色类型声明一个 IoCompletion 例程：

```
IO_COMPLETION_ROUTINE myCompletionRoutine;
```

实现*myCompletionRoutine*时，参数类型必须与 IO 完成例程使用的参数类型匹配 \_ \_ ，即 PDEVICE \_ 对象、PIRP 和 PVOID （有关语法，请参阅[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程）。

```
NTSTATUS
myCompletionRoutine(
 PDEVICE_OBJECT  DeviceObject,
 PIRP  Irp,
 PVOID  Context
 )
{
}
```

## <a name="span-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspanspan-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span>为驱动程序运行代码分析来验证函数声明


为帮助您确定是否已准备好源代码，请[对驱动程序运行代码分析](code-analysis-for-drivers.md)。 用于驱动程序的代码分析检查函数角色类型声明，并有助于识别可能已丢失的函数声明，或函数定义的参数与函数角色类型中的参数不匹配时发出警告。
