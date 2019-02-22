---
title: 声明用于 WDM 驱动程序函数的角色类型的函数
description: 声明用于 WDM 驱动程序函数的角色类型的函数
ms.assetid: 3260b53e-82be-4dbc-8ac5-d0e52de77f9d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eefd27d42e1d4d8619b2b75a3eba015e4a6d60d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542421"
---
# <a name="declaring-functions-using-function-role-types-for-wdm-drivers"></a>声明用于 WDM 驱动程序函数的角色类型的函数


若要在分析 WDM 驱动程序时将 SDV 告知驱动程序的入口点，必须声明使用函数角色类型声明的函数。 中 wdm.h 中定义的函数角色类型。 在每个入口点*DriverEntry* WDM 驱动程序中的例程必须通过指定相应的角色类型声明。 角色类型是 WDM 驱动程序中的已识别的入口点相对应的预定义的 typedef。

例如，若要创建的驱动程序的函数角色类型声明[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)调用的例程*CsampUnload*，使用预定义的 typedef 驱动程序\_卸载角色类型声明。 函数角色类型声明必须出现在函数定义之前。

```
DRIVER_UNLOAD CsampUnload;
```

定义*CsampUnload*函数保持不变：

```
VOID
CsampUnload(
    IN PDRIVER_OBJECT DriverObject
    )
{
    ...
}
```

SDV 可以识别以下表中所示的入口点的类型。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544113" data-raw-source="[&lt;em&gt;DriverEntry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544113)"><em>DriverEntry</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_STARTIO</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563858" data-raw-source="[&lt;em&gt;StartIO&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563858)"><em>StartIO</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_UNLOAD</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564886" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564886)"><em>卸载</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_ADD_DEVICE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"><em>AddDevice</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong><em>Dispatch_type</em>(</strong> <em>type</em> <strong>)</strong> DRIVER_DISPATCH</td>
<td align="left"><p>驱动程序使用的调度 routine(s)。 请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff566407" data-raw-source="[Writing Dispatch Routines](https://msdn.microsoft.com/library/windows/hardware/ff566407)">编写调度例程</a>。  <strong><em>Dispatch_type</em>(</strong><em>类型</em><strong>)</strong>批注必须结合 DRIVER_DISPATCH 角色类型声明，以指定驱动程序的入口点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_COMPLETION_ROUTINE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548354" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548354)"><em>IoCompletion</em></a></p>
<p><em>IoCompletion</em>通过调用设置例程<em>IoSetCompletionRoutine</em>或<em>IoSetCompletionRoutineEx</em>并传递到函数指针<em>IoCompletion</em>例程作为第二个参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_CANCEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540742" data-raw-source="[&lt;em&gt;Cancel&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540742)"><em>Cancel</em></a></p>
<p><strong>取消</strong>通过调用设置例程<strong>IoSetCancelRoutine</strong>和函数指针传递给取消例程的 IRP 作为函数的第二个参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_DPC_ROUTINE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544079" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544079)"><em>DpcForIsr</em></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544079" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544079)"> <em>DpcForIsr</em> </a>例程注册通过调用<em>IoInitializeDpcRequest</em>并传递到函数指针<em>DpcForIsr</em>第二个参数的例程。 若要排队 DPC，请调用<em>IoQueueDpc</em> ISR 例程使用相同的 DPC 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KDEFERRED_ROUTINE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542972" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542972)"><em>CustomDpc</em></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542972" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542972)"> <em>CustomDpc</em> </a>例程通过调用设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff552130" data-raw-source="[&lt;strong&gt;KeInitializeDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552130)"> <strong>KeInitializeDpc</strong> </a>并传递到函数指针<em>CustomDpc</em>第二个参数。 到队列<em>CustomDpc</em>驱动程序，调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552185" data-raw-source="[&lt;strong&gt;KeInsertQueueDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552185)"> <strong>KeInsertQueueDpc</strong> </a> ISR 例程使用相同的 DPC 对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSERVICE_ROUTINE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547958" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547958)"><em>InterruptService</em></a></p>
<p>如有必要，InterruptService 例程 (ISR) 服务接收数据的设备中断和计划后中断处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>REQUEST_POWER_COMPLETE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff961906" data-raw-source="[&lt;em&gt;PowerCompletion&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff961906)"> <em>PowerCompletion</em> </a>回调例程完成 power IRP 的处理。 如果驱动程序需要执行其他任务之后所有其他驱动程序已完成 IRP，驱动程序寄存器<em>PowerCompletion</em>在调用回调例程<a href="https://msdn.microsoft.com/library/windows/hardware/ff559734" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559734)"> <strong>PoRequestPowerIrp</strong></a>分配 IRP 的例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WORKER_THREAD_ROUTINE</p></td>
<td align="left"><p><em>Routine</em></p>
<p><em>例程</em>中的第二个参数指定的回调例程<a href="https://msdn.microsoft.com/library/windows/hardware/ff545327" data-raw-source="[&lt;strong&gt;ExInitializeWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545327)"> <strong>ExInitializeWorkItem</strong> </a>函数。</p>
<p><em>日常</em>只应声明这种方式如果驱动程序调用<strong>ExQueueWorkItem</strong>若要将工作项添加到系统队列。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idannotatingdriverdispatchroutinesspanspan-idannotatingdriverdispatchroutinesspandeclaring-driver-dispatch-routines"></a><span id="annotating_driver_dispatch_routines"></span><span id="ANNOTATING_DRIVER_DISPATCH_ROUTINES"></span>声明驱动程序调度例程

调度例程的函数角色类型声明需要其他信息。 使用批注**\_调度\_类型\_(**<em>类型</em>**)** 中提供主要 IRP 的调度例程的声明函数代码。 *类型*是主要的 I/O 函数代码 (例如，IRP\_MJ\_创建、 IRP\_MJ\_关闭、 IRP\_MJ\_系统\_控件)。

有关如何声明驱动程序调度例程的示例，请参阅取消按钮示例驱动程序 (Cancel.sys) 的源代码。 中没有的函数角色类型声明的驱动程序 (Cancel.h) 的标头文件*CsampCleanup*，处理 IRP 的驱动程序调度例程\_MJ\_清理 I/O 函数代码。 **\_调度\_类型\_(**<em>类型</em>**)** 批注位于驱动程序\_调度角色类型声明。

*CsampCleanup*例程声明，如下所示：

```
_Dispatch_type_(IRP_MJ_CLEANUP)
DRIVER_DISPATCH CsampCleanup;
```

取消按钮示例驱动程序还具有驱动程序调度例程*CsampCreateClose*，用于处理这两个 IRP\_MJ\_创建和 IRP\_MJ\_关闭 I/O 函数代码。 *CsampCreateClose*中 Cancel.h 声明例程。 此例程处理两个 I/O 函数代码，因为它需要两个**\_调度\_类型\_** 除了驱动程序的批注\_调度角色类型声明。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
DRIVER_DISPATCH CsampCreateClose;
```

假设筛选器驱动程序具有驱动程序调度调用的例程*FilterDispatchIo*处理 IRP\_MJ\_创建、 IRP\_MJ\_关闭、 IRP\_MJ\_清理和 IRP\_MJ\_设备\_控件 I/O 函数代码。

*FilterDispatchIo*例程声明 Filter.h 中，如下所示。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
_Dispatch_type_(IRP_MJ_CLEANUP)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH FilterDispatchIo;
```

### <a name="span-idquickstepshowtoannotateawdmdriverspanspan-idquickstepshowtoannotateawdmdriverspanquick-steps-how-to-annotate-a-wdm-driver"></a><span id="quick_steps__how_to_annotate_a_wdm_driver"></span><span id="QUICK_STEPS__HOW_TO_ANNOTATE_A_WDM_DRIVER"></span>快速步骤：如何批注 WDM 驱动程序

函数使用函数角色类型声明的过程如下所示：

1.  找到的源代码*DriverEntry*例程。

2.  请确保使用函数角色类型声明分配给以下指针的例程。

    ```
    DriverObject->DriverStartIo
    DriverObject->Unload
    DriverObject->DriverExtension->AddDevice 
    ```

    例如，下面的代码示例显示函数对应于这些指针的例程的角色类型声明 (*myDriverStartIO*， *myUnload*，和*myAddDevice*).

    ```
    DRIVER_STARTIO myDriverStartIo;
    DRIVER_UNLOAD myUnload;
    DRIVER_ADD_DEVICE myAddDevice 
    ```

3.  请确保使用的驱动程序声明分配给以下指针的例程\_调度角色类型，并且具有**\_调度\_类型\_** 批注。

    ```
    DriverObject->MajorFunction[IRP_MJ_xxx]
    ```

    例如：

    ```
    _Dispatch_type_(IRP_MJ_CLEANUP)
    DRIVER_DISPATCH CsampCleanup;
    ```

### <a name="span-idfunctionparametersandfunctionroletypesspanspan-idfunctionparametersandfunctionroletypesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>函数参数和函数的角色类型

根据需要在 C 编程语言中，在函数定义中使用的参数类型必须匹配的函数原型中，参数类型或函数角色在此示例中，键入。 SDV 取决于分析的函数签名，并忽略的函数的签名不匹配。

例如，应声明[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程使用 IO\_完成\_例程函数角色类型：

```
IO_COMPLETION_ROUTINE myCompletionRoutine;
```

当您实现*myCompletionRoutine*，参数类型必须匹配所使用的 IO\_完成\_例程，即 PDEVICE\_对象、 PIRP 和 PVOID (请参阅[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程的语法)。

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

## <a name="span-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspanspan-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span> 运行 Code Analysis for Drivers 验证函数声明


若要帮助您确定是否准备好的源代码，请运行[Code Analysis for Drivers](code-analysis-for-drivers.md)。 代码分析函数角色类型声明的驱动程序检查并且可以帮助标识可能错过的函数声明或函数定义的参数不匹配函数角色类型中时向您发出警告。

 

 





