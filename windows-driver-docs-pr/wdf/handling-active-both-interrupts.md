---
title: 处理同时处于活动状态的中断
description: 处理同时处于活动状态的中断
ms.assetid: CFA205B1-FDDD-4E27-8CF9-106C8D1CC4EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a72528f4cadb34bd9c91b75385dca8370bc0b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366495"
---
# <a name="handling-active-both-interrupts"></a>处理同时处于活动状态的中断


**请注意**  本主题适用仅到内核模式驱动程序框架 (KMDF) 版本 1.13 及更早版本。

 

许多设备都有硬件寄存器该控制中断生成和屏蔽。 通常情况下，此类设备用于 KMDF 和 UMDF 驱动程序使用框架的内置中断支持。

但是，一个芯片 (SoC) 的硬件平台上的系统上的简单设备可能没有中断的硬件寄存器。 因此，此类设备的驱动程序可能不能够控制时生成中断，或能够掩码中的硬件中断。 如果设备连接后，立即中断，并且该驱动程序正在使用框架的中断支持，就可以中断该框架已完全初始化的 framework 中断对象之前激发。 因此，KMDF 驱动程序必须调用 WDM 例程直接进行连接和断开连接中断。 UMDF 驱动程序不能调用这些方法，因为您无法编写此类设备的 UMDF 驱动程序。

本主题介绍如何 KMDF 驱动程序可能处理这类设备的中断。

SoC 硬件平台上同时处于活动状态的中断通常用于非常简单的设备，如硬件按钮。 当用户按下按钮式时，从设备的中断信号行转换从低到很高，或从高到低。 当用户释放按钮式时，中断行转换相反的方向。 GPIO pin 配置为同时处于活动状态的中断输入生成低到高和高到低的转换，从而导致在这两种情况下调用外围设备驱动程序的中断服务例程 (ISR) 在系统上的中断。 但是，该驱动程序不会接收指示转换是否低到高或高到低。

若要区分低到高和高到低的转换，该驱动程序必须跟踪每个中断状态。 为此，您的驱动程序可能维护是布尔中断状态值**FALSE**中断行状态较低时和**TRUE**高行状态时。

请考虑在其中的行状态默认为低在系统启动时的示例。 该驱动程序初始化到状态值**FALSE**在其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数。 然后每次调用时，驱动程序的 ISR，发出信号状态，更改驱动程序反转其 ISR.中的状态值

如果在系统启动时，行状态为高，中断之后将立即触发启用它。 由于该驱动程序调用[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)直接，而不是调用例程[ **WdfInterruptCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547345)，它是确保接收可能立即中断。

此解决方案需要 GPIO 控制器中的硬件，支持同时处于活动状态的中断或 GPIO 控制器的驱动程序模拟软件中同时处于活动状态的中断。 有关模拟同时处于活动状态的中断的信息，请参阅的说明**EmulateActiveBoth**的成员[**控制器\_特性\_标志**](https://msdn.microsoft.com/library/windows/hardware/hh439449)结构。

下面的代码示例演示如何外围设备的 KMDF 驱动程序可以跟踪中断极性。

```cpp
typedef struct _INTERRUPT_CONTEXT INTERRUPT_CONTEXT, *PINTERRUPT_CONTEXT;
typedef struct _DEVICE_CONTEXT DEVICE_CONTEXT, *PDEVICE_CONTEXT;


struct _INTERRUPT_CONTEXT
{
               BOOLEAN State;
               PDEVICE_CONTEXT DeviceContext;
};

struct _DEVICE_CONTEXT
{
               PKINTERRUPT Interrupt;
               INTERRUPT_CONTEXT InterruptContext;
               PDEVICE_OBJECT PhysicalDeviceObject;
               KSPIN_LOCK SpinLock;
};

...

BOOLEAN
YourInterruptIsr(
               __in PKINTERRUPT Interrupt,
               __in PVOID ServiceContext
               )
{
               PINTERRUPT_CONTEXT InterruptContext = (PINTERRUPT_CONTEXT)ServiceContext;
               PDEVICE_CONTEXT DeviceContext = InterruptContext->DeviceContext;

               //
               // Flip the state.
               //
               InterruptContext->State = !InterruptContext->State;

               IoRequestDpc(DeviceContext->PhysicalDeviceObject, DeviceContext->PhysicalDeviceObject->CurrentIrp, InterruptContext);
}

VOID
YourInterruptDpc(
               __in PKDPC Dpc,
               __in PDEVICE_OBJECT DeviceObject,
               __inout PIRP Irp,
               __in_opt PVOID ContextPointer
               )
{
               PINTERRUPT_CONTEXT InterruptContext = (PINTERRUPT_CONTEXT)ContextPointer;

               ...
}

NTSTATUS
EvtDriverDeviceAdd(
               __in  WDFDRIVER Driver,
               __in  PWDFDEVICE_INIT DeviceInit
               )
{
               WDFDEVICE Device;
               PDEVICE_CONTEXT DeviceContext;

               ...

               DeviceContext->Interrupt = NULL;
               DeviceContext->PhysicalDeviceObject = WdfDeviceWdmGetPhysicalDevice(Device);
               KeInitializeSpinLock(&DeviceContext->SpinLock);

               IoInitializeDpcRequest(DeviceContext->PhysicalDeviceObject, YourInterruptDpc);
}

NTSTATUS
EvtDevicePrepareHardware(
               __in  WDFDEVICE Device,
               __in  WDFCMRESLIST ResourcesRaw,
               __in  WDFCMRESLIST ResourcesTranslated
               )
{
               PDEVICE_CONTEXT DeviceContext = YourGetDeviceContext(Device);

               for (ULONG i = 0; i < WdfCmResourceListGetCount(ResourcesTranslated); i++)
               {
                              PCM_PARTIAL_RESOURCE_DESCRIPTOR descriptor = WdfCmResourceListGetDescriptor(ResourcesTranslated, i);

                              if (descriptor->Type == CmResourceTypeInterrupt)
                              {
                                             IO_CONNECT_INTERRUPT_PARAMETERS params;
                                             RtlZeroMemory(&params, sizeof(params));

                                             params.Version = CONNECT_FULLY_SPECIFIED;
                                             params.FullySpecified.PhysicalDeviceObject = DeviceContext->PhysicalDeviceObject;
                                             params.FullySpecified.InterruptObject = &DeviceContext->Interrupt;
                                             params.FullySpecified.ServiceRoutine = YourInterruptIsr;
                                             params.FullySpecified.ServiceContext = (PVOID)&DeviceContext->InterruptContext;
                                             params.FullySpecified.SpinLock = &DeviceContext->SpinLock;
                                             params.FullySpecified.Vector = descriptor->u.Interrupt.Vector;
                                             params.FullySpecified.Irql = (KIRQL)descriptor->u.Interrupt.Level;
                                             params.FullySpecified.SynchronizeIrql = (KIRQL)descriptor->u.Interrupt.Level;
                                             params.FullySpecified.InterruptMode = (descriptor->Flags & CM_RESOURCE_INTERRUPT_LATCHED) ? Latched : LevelSensitive;
                                             params.FullySpecified.ProcessorEnableMask = descriptor->u.Interrupt.Affinity;
                                             params.FullySpecified.ShareVector = descriptor->ShareDisposition;

                                             //
                                             // Default state is low.
                                             //
                                             DeviceContext->InterruptContext.State = 0;
                                             DeviceContext->InterruptContext.DeviceContext = DeviceContext;

                                             return IoConnectInterruptEx(&params);
                              }
               }

               return STATUS_SUCCESS;
}

NTSTATUS
EvtDeviceReleaseHardware(
               __in  WDFDEVICE Device,
               __in  WDFCMRESLIST ResourcesTranslated
)
{
               PDEVICE_CONTEXT DeviceContext = YourGetDeviceContext(Device);

               if (NULL != DeviceContext->Interrupt)
               {
                              IO_DISCONNECT_INTERRUPT_PARAMETERS params;

                              params.Version = CONNECT_FULLY_SPECIFIED;
                              params.ConnectionContext.InterruptObject = DeviceContext->Interrupt;

                              IoDisconnectInterruptEx(&params);
               }

               return STATUS_SUCCESS;
}
```

在前面的代码示例中，该驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数将配置的设备上下文，然后调用[ **IoInitializeDpcRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549307)注册[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程。

在驱动程序[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程反转中断状态值，然后调用[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)排队 DPC。

在其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数，该驱动程序初始化到状态值**FALSE** ，然后调用[ **IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378)。 在其[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数、 驱动程序调用[ **IoDisconnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549093)注销其 ISR.

 

 





