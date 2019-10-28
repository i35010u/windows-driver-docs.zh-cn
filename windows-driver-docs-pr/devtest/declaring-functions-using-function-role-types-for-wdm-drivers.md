---
title: 使用 WDM 驱动程序的函数角色类型来声明函数
description: 使用 WDM 驱动程序的函数角色类型来声明函数
ms.assetid: 3260b53e-82be-4dbc-8ac5-d0e52de77f9d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a42d75ee0447ce0fc250ead2afb40065feaa9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840286"
---
# <a name="declaring-functions-using-function-role-types-for-wdm-drivers"></a>使用 WDM 驱动程序的函数角色类型来声明函数


若要在分析 WDM 驱动程序时通知 SDV 驱动程序的入口点，必须使用函数角色类型声明声明函数。 在 Wdm .h 中定义函数角色类型。 WDM 驱动程序中*DriverEntry*例程的每个入口点都必须通过指定相应的角色类型进行声明。 角色类型是预定义的 typedef，它们对应于 WDM 驱动程序中的已识别入口点。

例如，若要为驱动程序的[**unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程（称为*CsampUnload*）创建函数角色类型声明，请使用预定义的 TYPEDEF 驱动程序\_卸载角色类型声明。 函数角色类型声明必须出现在函数定义之前。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)"></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_ADD_DEVICE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong><em>Dispatch_type</em>（</strong> <em>type</em> <strong>）</strong> DRIVER_DISPATCH</td>
<td align="left"><p>驱动程序使用的调度例程。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines" data-raw-source="[Writing Dispatch Routines](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)">编写调度例程</a>。 <strong><em>Dispatch_type</em>（</strong><em>类型</em><strong>）</strong>批注必须与 DRIVER_DISPATCH 角色类型声明组合在一起，才能指定驱动程序入口点。</p></td>
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
<td align="left"><p><em>例程</em></p>
<p><em>例程</em>是在<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl" data-raw-source="[&lt;strong&gt;ExInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)"><strong>ExInitializeWorkItem</strong></a>函数的第二个参数中指定的回调例程。</p>
<p>仅当驱动程序调用<strong>ExQueueWorkItem</strong>将工作项添加到系统队列时，才应以这种方式声明<em>例程</em>。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idannotating_driver_dispatch_routinesspanspan-idannotating_driver_dispatch_routinesspandeclaring-driver-dispatch-routines"></a><span id="annotating_driver_dispatch_routines"></span><span id="ANNOTATING_DRIVER_DISPATCH_ROUTINES"></span>声明驱动程序调度例程

调度例程的函数角色类型声明需要额外的信息。 使用批注 **\_调度\_类型**在用于提供主要 IRP 函数代码的调度例程的声明中\_（<em>类型</em> **）** 。 *类型*是主 i/o 函数代码（例如，IRP\_MJ\_CREATE、IRP\_MJ\_CLOSE、IRP\_MJ\_系统\_控件）。

有关如何声明驱动程序调度例程的示例，请参阅 Cancel 示例驱动程序的源代码（node.js）。 在驱动程序头文件（Cancel .h）中，有一个用于*CsampCleanup*的函数角色类型声明，该声明处理 IRP\_MJ\_清理 i/o 函数代码。 **\_调度\_\_ 类型** **注释在**驱动程序\_调度角色类型声明之前。

*CsampCleanup*例程的声明如下所示：

```
_Dispatch_type_(IRP_MJ_CLEANUP)
DRIVER_DISPATCH CsampCleanup;
```

取消示例驱动程序还具有驱动程序调度例程*CsampCreateClose*，它同时处理 IRP\_MJ\_CREATE 和 IRP\_MJ\_CLOSE i/o 函数代码。 *CsampCreateClose*例程在 Cancel 中声明。 由于此例程处理两个 i/o 函数代码，因此它需要两个 **\_调度\_类型\_** 批注以及驱动程序\_调度角色类型声明。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
DRIVER_DISPATCH CsampCreateClose;
```

假设筛选器驱动程序具有一个名为*FilterDispatchIo*的驱动程序调度例程，该例程处理 IRP\_MJ\_CREATE、IRP\_MJ\_CLOSE、IRP\_MJ\_清理和 IRP\_控制 i/o 函数代码。

*FilterDispatchIo*例程在筛选器 .h 中声明，如下所示。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
_Dispatch_type_(IRP_MJ_CLEANUP)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH FilterDispatchIo;
```

### <a name="span-idquick_steps__how_to_annotate_a_wdm_driverspanspan-idquick_steps__how_to_annotate_a_wdm_driverspanquick-steps-how-to-annotate-a-wdm-driver"></a><span id="quick_steps__how_to_annotate_a_wdm_driver"></span><span id="QUICK_STEPS__HOW_TO_ANNOTATE_A_WDM_DRIVER"></span>快速步骤：如何为 WDM 驱动程序添加批注

使用函数角色类型声明函数的过程如下所示：

1.  找到*DriverEntry*例程的源代码。

2.  确保分配给以下指针的例程是使用函数角色类型声明的。

    ```
    DriverObject->DriverStartIo
    DriverObject->Unload
    DriverObject->DriverExtension->AddDevice 
    ```

    例如，下面的代码示例显示了对应于这些指针（*myDriverStartIO*、 *myUnload*和*myAddDevice*）的例程的函数角色类型声明。

    ```
    DRIVER_STARTIO myDriverStartIo;
    DRIVER_UNLOAD myUnload;
    DRIVER_ADD_DEVICE myAddDevice 
    ```

3.  确保分配到以下指针的例程使用驱动程序\_调度角色类型进行声明，并确保它们具有 **\_调度\_类型\_** 注释。

    ```
    DriverObject->MajorFunction[IRP_MJ_xxx]
    ```

    例如：

    ```
    _Dispatch_type_(IRP_MJ_CLEANUP)
    DRIVER_DISPATCH CsampCleanup;
    ```

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>函数参数和函数角色类型

根据 C 编程语言的要求，在函数定义中使用的参数类型必须与函数原型的参数类型匹配，在本例中为函数角色类型。 SDV 依赖于用于分析的函数签名，并忽略其签名不匹配的函数。

例如，你应该使用 IO\_完成\_例程函数角色类型声明一个[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程：

```
IO_COMPLETION_ROUTINE myCompletionRoutine;
```

实现*myCompletionRoutine*时，参数类型必须与 IO\_完成\_例程（即，PDEVICE\_OBJECT，PIRP，和 PVOID）所使用的类型匹配（有关语法，请参阅[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程）。

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

 

 





