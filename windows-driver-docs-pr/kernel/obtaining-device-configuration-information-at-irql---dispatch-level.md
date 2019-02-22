---
title: 获取在 IRQL DISPATCH_LEVEL 设备配置信息
description: 获取在 IRQL DISPATCH_LEVEL 设备配置信息
ms.assetid: e168a12b-f32e-4b8d-8768-dc622b37b421
keywords:
- I/O WDK 内核，设备配置空间
- 设备配置空间 WDK I/O
- 配置空间 WDK I/O
- 空间 WDK I/O
- DISPATCH_LEVEL WDK
- BUS_INTERFACE_STANDARD
- 驱动程序堆栈 WDK 配置信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd20100a3270ec30fb38b8fb91a4332f4dbbf8fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545273"
---
# <a name="obtaining-device-configuration-information-at-irql--dispatchlevel"></a>获取设备配置信息在 IRQL = 调度\_级别





该方法中所示[获取设备配置信息在 IRQL = 被动\_级别](obtaining-device-configuration-information-at-irql---passive-level.md)部分将使用的 I/O 请求数据包 (Irp)，因此仅对驱动程序运行在 IRQL 有效 = 被动\_级别。 驱动程序运行在 IRQL = 调度\_级别必须使用总线接口获取设备配置的空间数据。 若要获取此数据，可以使用特定于总线的接口或系统提供独立于总线的总线接口**总线\_界面\_标准**。

GUID_BUS_INTERFACE_STANDARD 接口 (在中定义`wdmguids.h`) 使设备驱动程序，使父总线驱动程序例程，而不是使用 I/O 请求数据包 (IRP) 与总线驱动程序进行通信的直接调用。 具体而言，此接口允许驱动程序来访问总线驱动程序提供了以下函数的例程：

-    将总线地址转换 
-    检索在其中总线适配器支持 DMA 的情况下的 DMA 适配器结构 
-    读取和设置在总线上的特定设备的总线配置空间 

若要使用此接口，请将 IRP_MN_QUERY_INTERFACE IRP 发送到总线驱动程序与 InterfaceType = GUID_BUS_INTERFACE_STANDARD。 总线驱动程序提供了指向包含该接口的单个例程的指针的 BUS_INTERFACE_STANDARD 结构的指针。


最好使用**总线\_界面\_标准**如果可能，因为不需要检索配置信息时使用的总线号**总线\_接口\_标准**，而检索总线特定于接口时，驱动程序通常必须标识总线数。 对于某些总线，如 PCI 总线数字可以动态更改。 因此，驱动程序不应依赖于总线编号，以直接访问 PCI 端口。 执行此操作可能会导致系统出现故障。

访问在 IRQL PCI 设备的配置空间时，三个步骤所需 = 调度\_级别：

1.  发送[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求在 IRQL = 被动\_级别以获取直接调用接口结构 (**总线\_界面\_标准**) 从 PCI 总线驱动程序。 存储在非分页缓冲的池内存 （通常在设备扩展）。

2.  调用**总线\_界面\_标准**接口例程[ *SetBusData* ](https://msdn.microsoft.com/library/windows/hardware/gg604856)并[ *GetBusData* ](https://msdn.microsoft.com/library/windows/hardware/gg604850)，以访问 PCI 配置空间在 IRQL = 调度\_级别。

3.  取消对接口的引用。 PCI 总线驱动程序的引用计数在接口上之前会返回，以便访问接口的驱动程序必须对其取消引用，一旦不再需要。

下面的代码示例演示如何实现这三个步骤：

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

下面的代码段演示如何使用[ *GetBusData* ](https://msdn.microsoft.com/library/windows/hardware/gg604850)接口例程来获取配置的空间数据 （步骤 2）。

```cpp
 bytes = busInterfaceStandard.GetBusData(
                    busInterfaceStandard.Context,
                    PCI_WHICHSPACE_CONFIG,
                    Buffer
                    Offset,
                    Length);
```

如果该驱动程序用接口完成的它可以使用类似于以下代码片段的代码若要取消引用接口 （步骤 3）。 取消对接口的引用后，驱动程序必须调用接口例程。

```cpp
    (busInterfaceStandard.InterfaceDereference)(
                    (PVOID)busInterfaceStandard.Context);
```

该接口与 PCI 总线驱动程序的访问同步总线硬件对调用方的访问。 驱动程序编写器不需要担心如何创建自旋锁以避免争用访问总线硬件的 PCI 总线驱动程序。

请注意，是否它只需要是总线、 函数和设备号，这是通常不需要求助于总线接口，以获取此信息。 检索此数据可以是间接通过将传递到目标设备的 PDO [ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)函数，如下所示：

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

 

 




