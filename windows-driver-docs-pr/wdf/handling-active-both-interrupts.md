---
title: 处理同时处于活动状态的中断
description: 处理同时处于活动状态的中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4126b66a94a8bfb47382ddcd64e9bf0db6d441
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815641"
---
# <a name="handling-active-both-interrupts"></a>处理同时处于活动状态的中断


**注意**  本主题仅适用于 Kernel-Mode Driver Framework (KMDF) 1.13 版及更早版本。

 

许多设备都有控制中断生成和屏蔽的硬件寄存器。 通常，此类设备的 KMDF 和 UMDF 驱动程序使用框架的内置中断支持。

但是，芯片上系统上的一个简单设备 (SoC) 硬件平台上可能没有用于中断的硬件寄存器。 因此，此类设备的驱动程序可能无法控制中断的生成时间，也不能掩盖硬件中的中断。 如果设备在连接时立即中断，并且驱动程序使用框架的中断支持，则在框架完全初始化框架中断对象之前，中断可能会激发。 因此，KMDF 驱动程序必须直接调用 WDM 例程来连接和断开中断。 因为 UMDF 驱动程序无法调用这些方法，所以无法为此类设备写入 UMDF 驱动程序。

本主题介绍了 KMDF 驱动程序如何处理此类设备的中断。

在 SoC 硬件平台上，活动-两个中断通常用于非常简单的设备，如硬件推送按钮。 当用户按下按钮时，来自设备的中断信号线路从低到高进行转换，或从高到低转换。 当用户释放 "推送" 按钮时，中断线会以相反方向转换。 配置为 "活动-两个中断" 的 GPIO 输入会在低到高和低到低的转换上生成中断，因此，在这两种情况下，系统会 (ISR) 调用外围设备驱动程序的中断服务例程。 但是，驱动程序不会收到指示转换是从低到高还是从高到低的指示。

若要区分低到高和低到低转换，驱动程序必须跟踪每个中断的状态。 若要执行此操作，驱动程序可能会保留一个布尔中断状态值，该值在中断线路状态为 low 时为 **FALSE** ，当行状态为高时为 TRUE，则为 **TRUE** 。

假设在系统启动时，线路状态默认为 low。 驱动程序在其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数中将状态值初始化为 **FALSE** 。 然后，每次调用驱动程序的 ISR 时，向状态的更改发出信号，驱动程序将反转其 ISR 中的状态值。

如果在系统启动时线路状态很高，则中断在启用后立即触发。 由于驱动程序直接调用 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 例程，而不是调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)，因此可以确保接收可能的即时中断。

此解决方案要求 GPIO 控制器支持在硬件中的主动中断，或 GPIO 控制器的驱动程序在软件中模拟活动-两个中断。 有关模拟活动-两个中断的信息，请参阅 [**控制器 \_ 属性 \_ 标志**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_controller_attribute_flags)结构的 **EmulateActiveBoth** 成员的说明。

下面的代码示例演示如何使用 KMDF 驱动程序来跟踪中断极性。

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

在上面的代码示例中，驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数将配置设备上下文，然后调用 [**IoInitializeDpcRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializedpcrequest) 来注册 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程。

驱动程序的 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程反转中断状态值，然后调用 [**IoRequestDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc) 将 DPC 排队。

在其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数中，驱动程序将状态值初始化为 **FALSE** ，然后调用 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)。 在其 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调函数中，驱动程序调用 [**IoDisconnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex) 来注销其 ISR。

 

