---
title: 对 IRP 进行预处理和后处理
description: 对 IRP 进行预处理和后处理
ms.assetid: a0e14ae6-a06e-4c24-8b64-b56f485cf9ff
keywords:
- 预处理 Irp WDK KMDF
- 后续处理 Irp WDK KMDF
- WDM Irp WDK KMDF，预处理脚本和后续处理
- Irp WDK KMDF，预处理脚本和后续处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d01f64a404e9698a37009c69ef2506674cb8542
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390054"
---
# <a name="preprocessing-and-postprocessing-irps"></a>对 IRP 进行预处理和后处理


\[仅适用于 KMDF\]

如果您的驱动程序必须之前截获的 I/O 请求数据包 (IRP) 或驱动程序框架将处理 IRP 后，可以调用[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043)注册[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)主要的 I/O 函数代码和 （可选） 特定次要 I/O 函数的代码与主要代码相关联的事件的回调函数。 随后，框架将调用的驱动程序*EvtDeviceWdmIrpPreprocess*回调函数时，驱动程序接收 IRP，其中包含指定的主版本号和次函数代码。

[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数可以会尽一切努力预处理 IRP，并且它必须调用[ **WdfDeviceWdmDispatchPreprocessedIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546927) IRP 返回到框架，除非驱动程序，否则[处理 IRP 框架不支持](handling-an-irp-that-the-framework-does-not-support.md)。

驱动程序调用后[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)，框架中时，驱动程序不提供的相同方式处理 IRP [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数。 如果 IRP 的 I/O 函数代码是一个框架将传递给驱动程序，该驱动程序将 IRP 再次收到作为请求对象。

如果驱动程序所需的低级驱动程序完成 IRP，驱动程序的后 postprocess IRP [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数可以调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)若要设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程之前它将调用[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)。

后驱动程序调用[ **WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546043)，框架会导致 I/O 管理器，以添加其他[I/O 堆栈位置](https://msdn.microsoft.com/library/windows/hardware/ff551821)到所有的 Irp以便[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数可以设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。 回调函数调用之前必须更新 IRP 的 I/O 堆栈位置指针[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)。

### <a name="calling-wdfdevicewdmdispatchpreprocessedirp"></a>调用 WdfDeviceWdmDispatchPreprocessedIrp

因为 I/O 管理器将其他 I/O 堆栈位置添加到 IRP [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数必须调用[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)或[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387) （若要设置的下一步的 I/O 堆栈位置中） 之前调用[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)。

如果您的驱动程序预处理 IRP，但不是后续处理 IRP，驱动程序不需要设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程对于 IRP，并且可以调用[ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)，如下面的代码示例所示。

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

如果您的驱动程序后续处理 IRP，驱动程序必须调用[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387)，，然后必须调用[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)来设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程的 IRP，如下面的代码示例所示。

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

您的驱动程序不能调用[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387) (并因此不能设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程) 如果设备对象处理的驱动程序[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数接收表示物理设备对象 (PDO) 和函数代码如果 IRP 的主要是 IRP\_MJ\_PNP 或 IRP\_MJ\_电源。 否则为[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)将报告错误。

有关何时调用详细信息[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387)， [ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)，和[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)，请参阅[驱动程序堆栈的下层传递 Irp](https://msdn.microsoft.com/library/windows/hardware/ff558781)。

 

 





