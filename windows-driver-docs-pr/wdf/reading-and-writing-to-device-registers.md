---
title: 读取设备注册表和写入到设备注册表
description: 读取设备注册表和写入到设备注册表
ms.assetid: 58A94C75-94C1-4517-A300-9F04AA7B771A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c698108f6bf39a778b5d7dc47b84eed7b365206d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191009"
---
# <a name="reading-and-writing-to-device-registers"></a>读取设备注册表和写入到设备注册表


驱动程序按照 [查找和映射硬件资源](finding-and-mapping-hardware-resources.md)中所述的方式映射寄存器后，KMDF 驱动程序使用 [**HAL 库例程**](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) 来读取和写入寄存器，而 UMDF 驱动程序 (版本2.0 或更高版本) 通常使用 [WDF 注册/端口访问函数](/windows-hardware/drivers/ddi/wdfhwaccess/)。

如果 UMDF 驱动程序需要直接访问内存映射的寄存器，则可以将 INF 指令 **UmdfRegisterAccessMode** 设置为 **RegisterAccessUsingUserModeMapping** ，然后调用 [**WdfDeviceGetHardwareRegisterMappedAddress**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegethardwareregistermappedaddress) 来检索用户模式映射地址。 由于框架不验证以这种方式执行的读取和写入访问，因此不建议将此方法用于寄存器访问。 有关 UMDF INF 指令的完整列表，请参阅 [在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

下面的示例包含可使用 KMDF (1.13 或更高版本) 或 UMDF (2.0 或更高版本) 进行编译的代码。 该示例演示驱动程序如何使用其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数检查其内存映射寄存器资源，并将其映射到用户模式地址空间。 然后，该示例演示如何访问内存位置。

在访问设备寄存器和端口之前，UMDF 驱动程序必须在驱动程序的 INF 文件中将 **UmdfDirectHardwareAccess** 指令设置为 **AllowDirectHardwareAccess** 。

```cpp
NTSTATUS
 MyDevicePrepareHardware (
    IN WDFDEVICE  Device,
    IN WDFCMRESLIST  ResourcesRaw,
    IN WDFCMRESLIST  ResourcesTranslated
    )
  
{
    PCM_PARTIAL_RESOURCE_DESCRIPTOR desc = NULL;
    PCM_PARTIAL_RESOURCE_DESCRIPTOR  descTranslated = NULL;
    PHYSICAL_ADDRESS regBasePA = {0};
    ULONG regLength = 0;
    BOOLEAN found = FALSE;
    ULONG  i;
    PFDO_DATA deviceContext;
    NTSTATUS status = STATUS_SUCCESS;
    
    UNREFERENCED_PARAMETER(ResourcesRaw);

    MyKdPrint(("MyEvtDevicePrepareHardware Device 0x%p ResRaw 0x%p ResTrans "
        "0x%p Count %d\n", Device, ResourcesRaw, ResourcesTranslated,
        WdfCmResourceListGetCount(ResourcesTranslated)));

#ifndef _KERNEL_MODE
    WDF_DEVICE_IO_TYPE stackReadWriteIotype = WdfDeviceIoUndefined; 
    WDF_DEVICE_IO_TYPE stackIoctlIotype = WdfDeviceIoUndefined;
    WdfDeviceGetDeviceStackIoType(Device,
                                  &stackReadWriteIotype,
                                  &stackIoctlIotype);
    MyKdPrint(("Device 0x%p stackReadWriteIoType %S stackIoctlIoType %S\n",
        Device,
        GetIoTypeName(stackReadWriteIotype),
        GetIoTypeName(stackIoctlIotype)
        ));

#endif

    deviceContext = ToasterFdoGetData(Device);
    
    //
    // Scan the list and identify our resource
    //
    for (i = 0; i < WdfCmResourceListGetCount(ResourcesTranslated); i++) {
        desc = WdfCmResourceListGetDescriptor(Resources, i);
        descTranslated =  WdfCmResourceListGetDescriptor(ResourcesTranslated, i);
           
        switch (desc->Type) {
            case CmResourceTypeMemory:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypeMemory resources \n"));
                //
                // see if this is the memory resource we're looking for
                // 
                if (desc->u.Memory.Length == 0x200) {
                    regBasePA = desc->u.Memory.Start;
                    regLength = desc->u.Memory.Length;
                    found = TRUE;                    
                }
                break;
                
            case CmResourceTypePort:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypePort"
                    " resource\n"));

                switch(descTranslated->Type) {

                case CmResourceTypePort:
                    deviceContext->PortWasMapped = FALSE;
                    deviceContext->PortBase = 
                        ULongToPtr(descTranslated->u.Port.Start.LowPart);
                    deviceContext->PortCount = descTranslated ->u.Port.Length;
                    MyKdPrint(("Resource Translated Port: (%x) Length: (%d)\n",
                             descTranslated->u.Port.Start.LowPart,
                             descTranslated->u.Port.Length));                        
                    break;
                    
                case CmResourceTypeMemory:
                    //
                    // Map the memory
                    //

#if IS_UMDF_DRIVER                    
                    status = WdfDeviceMapIoSpace(
                                            Device,
                                            descTranslated->u.Memory.Start,
                                            descTranslated->u.Memory.Length,
                                            MmNonCached,
                                            &deviceContext->PortBase
                                            );

                    if (!NT_SUCCESS(status)) {
                        WdfVerifierDbgBreakPoint();
                    }
#else
                    deviceContext->PortBase = (PVOID) 
                                        MmMapIoSpace(
                                            descTranslated->u.Memory.Start,
                                            descTranslated->u.Memory.Length,
                                            MmNonCached
                                            );
                    UNREFERENCED_PARAMETER(status);

#endif
                    deviceContext->PortCount = descTranslated->u.Memory.Length;
                    deviceContext->PortWasMapped = TRUE;
                    MyKdPrint(("Resource Translated Memory: (%x) Length: (%d)\n",
                             descTranslated->u.Memory.Start.LowPart,
                             descTranslated->u.Memory.Length));                        
                    break;
                default:
                    MyKdPrint(("Unhandled resource_type (0x%x)\n", 
                        descTranslated->Type));
                }
                break;

            case CmResourceTypeInterrupt:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypeInterrupt"
                    "resource\n"));
                break;                

            case CmResourceTypeConnection:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypeConnection"
                    "resource\n"));
                break;                

            default:
                MyKdPrint(("EvtPrepareHardware: found resources of type %d"
                    "(CM_RESOURCE_TYPE)\n", desc->Type));
                break;
        }
    }


//
// Next, the driver uses register/port access macros to access the port.
//

    if ((PUCHAR)&deviceContext->PortBase != NULL) {
        UCHAR data;
        
#ifndef _KERNEL_MODE
        data = WDF_READ_PORT_UCHAR(Device, (PUCHAR)deviceContext->PortBase);
#else
        data = READ_PORT_UCHAR((PUCHAR)deviceContext->PortBase);
#endif

        MyKdPrint(("Read value %d from port address 0x%p\n", data, 
            deviceContext->PortBase));
    }
  
  if (i == 0) {
        MyKdPrint(("EvtPrepareHardware: no cm resources found \n"));
    }
    
    return STATUS_SUCCESS;
}



NTSTATUS
 MyDeviceReleaseHardware (
    IN WDFDEVICE  Device,
    IN WDFCMRESLIST  ResourcesTranslated
    )

{
    PFDO_DATA deviceContext;

    UNREFERENCED_PARAMETER(ResourcesTranslated);

    MyKdPrint(("CovEvtDeviceReleaseHardware Device 0x%p ResTrans 0x%p\n", 
        Device, ResourcesTranslated));

    deviceContext = ToasterFdoGetData(Device);

    if (deviceContext->PortWasMapped) {
#if IS_UMDF_DRIVER
        WdfDeviceUnmapIoSpace(Device,
                              deviceContext->PortBase,
                              deviceContext->PortCount);
#else
        MmUnmapIoSpace(deviceContext->PortBase,
                     deviceContext->PortCount);
#endif
    }

    return STATUS_SUCCESS;
}
```

 

