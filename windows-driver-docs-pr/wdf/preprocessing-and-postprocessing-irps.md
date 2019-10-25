---
title: 对 IRP 进行预处理和后处理
description: 对 IRP 进行预处理和后处理
ms.assetid: a0e14ae6-a06e-4c24-8b64-b56f485cf9ff
keywords:
- 预处理 Irp WDK KMDF
- 后处理 Irp WDK KMDF
- WDM Irp WDK KMDF、预处理和后处理
- Irp WDK KMDF、预处理和后处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90a32e3cb8abbc171e4cbb90f56457d650982d40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842234"
---
# <a name="preprocessing-and-postprocessing-irps"></a>对 IRP 进行预处理和后处理


\[仅适用于 KMDF\]

如果驱动程序必须在框架处理 IRP 之前或之后截获 i/o 请求数据包（IRP），驱动程序可以调用[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)来注册的[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)事件回调函数主 i/o 函数代码和（可选），适用于与主要代码相关联的特定小的 i/o 函数代码。 随后，只要驱动程序收到包含指定的主要和次要函数代码的 IRP，框架就会调用驱动程序的*EvtDeviceWdmIrpPreprocess*回调函数。

[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数可以执行预处理 IRP 所需的任何操作，然后必须调用[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)将 irp 返回到框架，除非该驱动程序正在[处理 irp框架不支持](handling-an-irp-that-the-framework-does-not-support.md)。

驱动程序调用[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)后，框架将处理 IRP，其方式与驱动程序未提供[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数时相同。 如果 IRP 的 i/o 函数代码是框架传递给驱动程序的代码，则驱动程序将再次接收 IRP 作为请求对象。

如果在较低级别的驱动程序完成 IRP 之后，驱动程序需要 postprocess IRP，则驱动程序的[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数可以调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)来设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，然后再调用[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)。

驱动程序调用[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)后，框架会使 i/o 管理器向所有 irp 添加一个额外的[i/o 堆栈位置](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations)，以便[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数可以设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 回调函数必须更新 IRP 的 i/o 堆栈位置指针，然后再调用[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)。

### <a name="calling-wdfdevicewdmdispatchpreprocessedirp"></a>调用 WdfDeviceWdmDispatchPreprocessedIrp

因为 i/o 管理器向 IRP 添加了额外的 i/o 堆栈位置，所以[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数必须调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) （以设置下一个 i/o中的堆栈位置），然后再调用[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)。

如果你的驱动程序正在预处理 IRP，而不是后处理 IRP，则驱动程序无需为 IRP 设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，并且可以调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，如以下代码示例所示。

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

如果驱动程序正在后处理 IRP，则驱动程序必须调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)，然后它必须调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)为 IRP 设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，如以下代码示例所示。

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

如果驱动程序的[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数接收的设备对象句柄，则驱动程序不得调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) （因此不得设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程）物理设备对象（PDO），并且如果 IRP 的主要函数代码为 IRP\_MJ\_PNP 或 IRP\_MJ\_电源。 否则，[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)器将报告错误。

有关何时调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)、 [**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)和[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)的详细信息，请参阅[向下传递 irp 驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/kernel/passing-irps-down-the-driver-stack)。

 

 





