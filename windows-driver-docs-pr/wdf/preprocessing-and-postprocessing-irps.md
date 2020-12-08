---
title: 对 IRP 进行预处理和后处理
description: 对 IRP 进行预处理和后处理
keywords:
- 预处理 Irp WDK KMDF
- 后处理 Irp WDK KMDF
- WDM Irp WDK KMDF、预处理和后处理
- Irp WDK KMDF、预处理和后处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca9e9e4a14d6a02c47c01eb41cc4d339433019b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832881"
---
# <a name="preprocessing-and-postprocessing-irps"></a>对 IRP 进行预处理和后处理


\[仅适用于 KMDF\]

如果你的驱动程序必须在框架处理 IRP 之前或之后拦截 (IRP) 的 i/o 请求包，则驱动程序可以调用 [**WdfDeviceInitAssignWdmIrpPreprocessCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback) 为主要 i/o 函数代码注册 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 事件回调函数，并根据需要为与主要代码相关联的特定小的 i/o 函数代码注册该函数。 随后，只要驱动程序收到包含指定的主要和次要函数代码的 IRP，框架就会调用驱动程序的 *EvtDeviceWdmIrpPreprocess* 回调函数。

[*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数可执行对 irp 进行预处理所需的任何操作，然后必须调用 [**WdfDeviceWdmDispatchPreprocessedIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)将 irp 返回到框架，除非该驱动程序正在 [处理该框架不支持的 irp](handling-an-irp-that-the-framework-does-not-support.md)。

驱动程序调用 [**WdfDeviceWdmDispatchPreprocessedIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)后，框架将处理 IRP，其方式与驱动程序未提供 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数时相同。 如果 IRP 的 i/o 函数代码是框架传递给驱动程序的代码，则驱动程序将再次接收 IRP 作为请求对象。

如果在较低级别的驱动程序完成 IRP 之后，驱动程序需要 postprocess IRP，则驱动程序的 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数可以调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 来设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，然后再调用 [**WdfDeviceWdmDispatchPreprocessedIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)。

驱动程序调用 [**WdfDeviceInitAssignWdmIrpPreprocessCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)后，框架会使 i/o 管理器向所有 irp 添加一个额外的 [i/o 堆栈位置](../kernel/i-o-stack-locations.md) ，以便 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数可以设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 回调函数必须更新 IRP 的 i/o 堆栈位置指针，然后再调用 [**WdfDeviceWdmDispatchPreprocessedIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)。

### <a name="calling-wdfdevicewdmdispatchpreprocessedirp"></a>调用 WdfDeviceWdmDispatchPreprocessedIrp

因为 i/o 管理器向 IRP 添加了额外的 i/o 堆栈位置， [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数必须调用 [**IoSkipCurrentIrpStackLocation**](../kernel/mm-bad-pointer.md) 或 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) (来设置 irp) 中的下一个 i/o 堆栈位置，然后再调用 [**WdfDeviceWdmDispatchPreprocessedIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)。

如果你的驱动程序正在预处理 IRP，而不是后处理 IRP，则驱动程序无需为 IRP 设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，并且可以调用 [**IoSkipCurrentIrpStackLocation**](../kernel/mm-bad-pointer.md)，如以下代码示例所示。

```cpp
NTSTATUS
  EvtDeviceMyIrpPreprocess(
    IN WDFDEVICE Device,
    IN OUT PIRP Irp
    )
{
//
// Perform IRP preprocessing operations here.
//
...
//
// Deliver the IRP back to the framework. 
//
IoSkipCurrentIrpStackLocation(Irp);
return WdfDeviceWdmDispatchPreprocessedIrp(Device, Irp);
}
```

如果驱动程序正在后处理 IRP，则驱动程序必须调用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)，然后它必须调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 为 IRP 设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，如以下代码示例所示。

```cpp
NTSTATUS
  EvtDeviceMyIrpPreprocess(
    IN WDFDEVICE Device,
    IN OUT PIRP Irp
    )
{
//
// Perform IRP preprocessing operations here, if needed.
//
...
//
// Set a completion routine and deliver the IRP back to
// the framework. 
//
IoCopyCurrentIrpStackLocationToNext(Irp);
IoSetCompletionRoutine(
                       Irp,
                       MyIrpCompletionRoutine,
                       NULL,
                       TRUE,
                       TRUE,
                       TRUE
                      );
return WdfDeviceWdmDispatchPreprocessedIrp(Device, Irp);
}
```

你的驱动程序不得 (调用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) ，因此不能设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程) 如果驱动程序的 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数接收的设备对象处理程序表示 (PDO) 的物理设备对象，以及 IRP 的主要函数代码为 IRP \_ mj \_ PNP 或 irp \_ mj \_ 电源。 否则， [驱动程序验证](../devtest/driver-verifier.md) 器将报告错误。

有关何时调用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)、 [**IoSkipCurrentIrpStackLocation**](../kernel/mm-bad-pointer.md)和 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)的详细信息，请参阅 [向下传递 irp 驱动程序堆栈](../kernel/passing-irps-down-the-driver-stack.md)。

 

