---
title: 以 IRQL DISPATCH_LEVEL 获取设备配置信息
description: 以 IRQL DISPATCH_LEVEL 获取设备配置信息
ms.assetid: e168a12b-f32e-4b8d-8768-dc622b37b421
keywords:
- I/o WDK 内核，设备配置空间
- 设备配置空间 WDK i/o
- 配置空间 WDK i/o
- 太空 WDK i/o
- DISPATCH_LEVEL WDK
- BUS_INTERFACE_STANDARD
- 驱动程序堆栈 WDK 配置信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c43de5b4188fc05141060abf308625a8a435805
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191169"
---
# <a name="obtaining-device-configuration-information-at-irql--dispatch_level"></a>获取 IRQL 的设备配置信息 = 调度 \_ 级别





在 [irql = 被动 \_ 级别获取设备配置信息](obtaining-device-configuration-information-at-irql---passive-level.md) 部分中所示的方法将使用 i/o 请求数据包 (irp) ，因此它仅对以 IRQL = 被动级别运行的驱动程序有效 \_ 。 以 IRQL = 调度级别运行的驱动程序 \_ 必须使用总线接口来获取设备配置空间数据。 若要获取此数据，可以使用特定于总线的接口或系统提供的与总线无关的总线接口，即 **总线 \_ 接口 \_ 标准**。

) 中定义的 GUID_BUS_INTERFACE_STANDARD 接口 (`wdmguid.h` 使设备驱动程序能够直接调用父总线驱动程序例程，而不是使用 i/o 请求数据包 (IRP) 与总线驱动程序通信。 具体而言，此接口使驱动程序能够访问总线驱动程序为以下函数提供的例程：

-    转换总线地址 
-    在总线适配器支持 DMA 的情况下检索 DMA 适配器结构 
-    在总线上读取和设置特定设备的总线配置空间 

若要使用此接口，请使用 InterfaceType = GUID_BUS_INTERFACE_STANDARD 将 IRP_MN_QUERY_INTERFACE IRP 发送到总线驱动程序。 总线驱动程序提供一个指向 BUS_INTERFACE_STANDARD 结构的指针，该结构包含指向接口的各个例程的指针。


最好尽可能使用 **总线 \_ 接口 \_ 标准** ，因为在使用 **总线 \_ 接口 \_ 标准版**时，无需使用总线号来检索配置信息，而驱动程序必须经常在检索特定于总线的接口时标识总线号。 某些总线的总线号，如 PCI，可以动态更改。 因此，驱动程序不应依赖于总线号直接访问 PCI 端口。 这样做可能会导致系统故障。

访问 PCI 设备的配置空间时，需要执行三个步骤，如下所 \_ 示：

1.  以 IRQL = 被动级别发送 [**IRP \_ MN \_ 查询 \_ 接口**](./irp-mn-query-interface.md) 请求 \_ ，以从 PCI 总线驱动程序 (**总线 \_ 接口 \_ 标准**) 中获取直接调用接口结构。 将其存储在非分页池内存中 (通常在设备扩展) 中。

2.  调用 **总线 \_ 接口 \_ 标准** 接口例程 [*SetBusData*](/previous-versions/windows/hardware/drivers/gg604856(v=vs.85)) 和 [*GetBusData*](/windows-hardware/drivers/ddi/wdm/nc-wdm-get_set_device_data)，以在 IRQL = 调度级别访问 PCI 配置空间 \_ 。

3.  取消引用接口。 PCI 总线驱动程序在其返回之前会在接口上使用引用计数，因此，访问接口的驱动程序必须在不再需要该接口时对其取消引用。

下面的代码示例演示如何实现以下三个步骤：

```cpp
NTSTATUS
GetPCIBusInterfaceStandard(
    IN  PDEVICE_OBJECT DeviceObject,
    OUT PBUS_INTERFACE_STANDARD BusInterfaceStandard
    )
/*++
Routine Description:
    This routine gets the bus interface standard information from the PDO.
Arguments:
    DeviceObject - Device object to query for this information.
    BusInterface - Supplies a pointer to the retrieved information.
Return Value:
    NT status.
--*/ 
{
    KEVENT event;
    NTSTATUS status;
    PIRP irp;
    IO_STATUS_BLOCK ioStatusBlock;
    PIO_STACK_LOCATION irpStack;
    PDEVICE_OBJECT targetObject;

    Bus_KdPrint(("GetPciBusInterfaceStandard entered.\n"));
    KeInitializeEvent(&event, NotificationEvent, FALSE);
    targetObject = IoGetAttachedDeviceReference(DeviceObject);
    irp = IoBuildSynchronousFsdRequest(IRP_MJ_PNP,
                                       targetObject,
                                       NULL,
                                       0,
                                       NULL,
                                       &event,
                                       &ioStatusBlock);
    if (irp == NULL) {
        status = STATUS_INSUFFICIENT_RESOURCES;
        goto End;
    }
    irpStack = IoGetNextIrpStackLocation( irp );
    irpStack->MinorFunction = IRP_MN_QUERY_INTERFACE;
    irpStack->Parameters.QueryInterface.InterfaceType = (LPGUID)&GUID_BUS_INTERFACE_STANDARD;
    irpStack->Parameters.QueryInterface.Size = sizeof(BUS_INTERFACE_STANDARD);
    irpStack->Parameters.QueryInterface.Version = 1;
    irpStack->Parameters.QueryInterface.Interface = (PINTERFACE)BusInterfaceStandard;
    irpStack->Parameters.QueryInterface.InterfaceSpecificData = NULL;

    // Initialize the status to error in case the bus driver does not 
    // set it correctly.
    irp->IoStatus.Status = STATUS_NOT_SUPPORTED;
    status = IoCallDriver(targetObject, irp);
    if (status == STATUS_PENDING) {
        KeWaitForSingleObject(&event, Executive, KernelMode, FALSE, NULL);
        status = ioStatusBlock.Status;
    }
End:
    // Done with reference
    ObDereferenceObject(targetObject);
    return status;
}
```

下面的代码段演示如何使用 [*GetBusData*](/windows-hardware/drivers/ddi/wdm/nc-wdm-get_set_device_data) 接口例程) 步骤 2 (获取配置空间数据。

```cpp
 bytes = busInterfaceStandard.GetBusData(
                    busInterfaceStandard.Context,
                    PCI_WHICHSPACE_CONFIG,
                    Buffer
                    Offset,
                    Length);
```

当使用接口完成驱动程序时，它可以使用类似于以下代码片段的代码来取消引用第3步)  (接口。 在取消引用接口后，驱动程序不得调用接口例程。

```cpp
    (busInterfaceStandard.InterfaceDereference)(
                    (PVOID)busInterfaceStandard.Context);
```

接口使用 PCI 总线驱动程序的访问权限同步调用方对总线硬件的访问。 驱动程序编写器不必担心如何创建自旋锁，以避免与 PCI 总线驱动程序争用以访问总线硬件。

请注意，如果所有需要的都是总线、函数和设备号，则通常不需要使用总线接口来获取此信息。 可以通过将目标设备的 PDO 传递到 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 函数来间接检索此数据，如下所示：

```cpp
    ULONG   propertyAddress, length;
    USHORT  FunctionNumber, DeviceNumber;

    // Get the BusNumber. Be warned that bus numbers may be
    // dynamic and therefore subject to change unpredictably!!!
    IoGetDeviceProperty(PhysicalDeviceObject,
                        DevicePropertyBusNumber,
                        sizeof(ULONG),
                        (PVOID)&BusNumber,
                        &length);

    // Get the DevicePropertyAddress
    IoGetDeviceProperty(PhysicalDeviceObject,
                        DevicePropertyAddress,
                        sizeof(ULONG),
                        (PVOID)&propertyAddress,
                        &length);

    // For PCI, the DevicePropertyAddress has device number 
    // in the high word and the function number in the low word. 
    FunctionNumber = (USHORT)((propertyAddress) & 0x0000FFFF);
    DeviceNumber = (USHORT)(((propertyAddress) >> 16) & 0x0000FFFF);
```

 

