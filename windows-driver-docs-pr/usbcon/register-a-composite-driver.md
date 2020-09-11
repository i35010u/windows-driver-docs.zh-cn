---
description: 称为复合驱动程序的 USB 多功能设备如何使用基础 USB 驱动程序堆栈注册和注销复合设备。
title: 如何注册复合设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52347da0aab68e170da392225eb59c4fae67f960
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010615"
---
# <a name="how-to-register-a-composite-device"></a>如何注册复合设备


本主题介绍了称为复合驱动程序的 USB 多功能设备的驱动程序如何使用基础 USB 驱动程序堆栈注册和注销复合设备。 Microsoft 提供的驱动程序 Usbccgp.sys 是 Windows 加载的默认复合驱动程序。 本主题中的过程适用于自定义 Windows 驱动模型基于 (WDM) 的复合驱动程序，该驱动程序将替换 Usbccgp.sys。

 (USB) 设备的通用串行总线可以提供同时处于活动状态的多个功能。 此类多功能设备也称为 *复合设备*。 例如，复合设备可以定义键盘功能的函数和鼠标的另一个函数。 设备的功能由复合驱动程序枚举。 复合驱动程序可以在单一模型中管理这些函数本身，也可以为每个函数 (PDOs) 创建物理设备对象。 这些单独的 PDOs 由其各自的 USB 函数驱动程序、键盘驱动程序和鼠标驱动程序管理。

USB 3.0 规范定义 *函数挂起和远程唤醒功能* ，使个别功能能够进入和退出低功耗状态，而不会影响其他功能或整个设备的电源状态。 有关该功能的详细信息，请参阅 [如何在复合驱动程序中实现函数挂起](how-to--implement-remote-and-function-wake-support.md)。

若要使用此功能，复合驱动程序需要使用基础 USB 驱动程序堆栈注册设备。 由于此功能适用于 USB 3.0 设备，因此复合驱动程序必须确保基础堆栈支持版本 USBD \_ 接口 \_ 版本 \_ 602。 通过注册请求，复合驱动程序：

-   通知底层 USB 驱动程序堆栈，驱动程序负责向 arm 提供用于远程唤醒功能的请求。 远程唤醒请求由 USB 驱动程序堆栈处理，该堆栈将必要的协议请求发送到设备。
-   获取一个函数句柄列表，其中 (每个函数) 由 USB 驱动程序堆栈分配。 然后，复合驱动程序可以使用驱动程序中的函数句柄来对与句柄关联的函数的远程唤醒请求。

通常，复合驱动程序会在驱动程序的 AddDevice 中发送注册请求，或使用启动设备例程来处理 [**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md)。 因此，复合驱动程序会释放为驱动程序的卸载例程（如 stop-device ([**irp \_ MN \_ stop \_ device**](../kernel/irp-mn-stop-device.md)) 或 Remove-device 例程 ([**IRP \_ MN \_ remove \_ device**](../kernel/irp-mn-remove-device.md)) 中的注册分配的资源。

### <a name="prerequisites"></a>先决条件

在发送注册请求之前，请确保：

-   设备中有数目的函数。 该数字可以派生接收配置请求检索到的描述符。
-   已在对 [**USBD \_ CreateHandle**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)的先前调用中获取 USBD 句柄。
-   基础 USB 驱动程序堆栈支持 USB 3.0 设备。 为此，请调用 [**USBD \_ IsInterfaceVersionSupported**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isinterfaceversionsupported) 并传递 USBD \_ 接口 \_ 版本 \_ 602 作为要检查的版本。

有关代码示例，请参阅 [如何在复合驱动程序中实现函数挂起](how-to--implement-remote-and-function-wake-support.md)。
Instructions
------------

### <a name="register-a-composite-device"></a>注册复合设备

下面的过程介绍了如何生成和发送注册请求，以将复合驱动程序与 USB 驱动程序堆栈相关联。

1.  通过调用[**复合 \_ 设备 \_ 功能 \_ INIT**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-composite_device_capabilities_init)宏来分配[**复合 \_ 设备 \_ 功能**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_composite_device_capabilities)结构并对其进行初始化。
2.  将[**复合 \_ 设备 \_ 功能**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_composite_device_capabilities)的**CapabilityFunctionSuspend**成员设置为1。
3.  通过调用[**USBD \_ BuildRegisterCompositeDevice**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_buildregistercompositedevice)例程分配[**注册 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_register_composite_device)结构并初始化结构。 在调用中，指定 USBD 句柄、已初始化的 [**复合 \_ 设备 \_ 功能**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_composite_device_capabilities) 结构和函数的数目。
4.  通过调用[**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)来分配 i/o 请求数据包 (irp) ，并通过调用[**IOGETNEXTIRPSTACKLOCATION**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)获取指向 IRP 的第一个堆栈位置 ([**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) 的指针。
5.  为缓冲区分配内存，使其足以容纳函数句柄的数组， (USBD \_ 函数 \_ 句柄) 。 数组中的元素数必须是 PDOs 的数目。
6.  通过设置 [**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的以下成员生成请求：
    -   通过将 **IoControlCode** 设置为 [**IOCTL \_ 内部 \_ USB \_ 注册 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device)，指定请求的类型。
    -   通过将参数设置为 Argument1 来指定输入参数 **。其他.** 请将设置为已初始化的 [**注册 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_register_composite_device) 结构的地址。
    -   通过将 **AssociatedIrp.SystemBuffer** 设置为在步骤5中分配的缓冲区来指定输出参数。

7.  通过将 IRP 传递到下一个堆栈位置来调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 以发送请求。

完成后，检查 USB 驱动程序堆栈返回的函数句柄数组。 可以将阵列存储在驱动程序的设备上下文中，供将来使用。

下面的代码示例演示如何生成和发送注册请求。 该示例假设复合驱动程序将以前获得的函数和 USBD 句柄存储在驱动程序的设备上下文中。

```ManagedCPlusPlus
VOID  RegisterCompositeDriver(PPARENT_FDO_EXT parentFdoExt)  
{  
    PIRP                            irp;  
    REGISTER_COMPOSITE_DRIVER       registerInfo;  
    COMPOSITE_DRIVER_CAPABILITIES   capabilities;  
    NTSTATUS                        status;  
    PVOID                           buffer;  
    ULONG                           bufSize;  
    PIO_STACK_LOCATION              nextSp;  

    buffer = NULL;  

    COMPOSITE_DRIVER_CAPABILITIES_INIT(&capabilities);  
    capabilities.CapabilityFunctionSuspend = 1;  

    USBD_BuildRegisterCompositeDriver(parentFdoExt->usbdHandle,  
        capabilities,  
        parentFdoExt->numFunctions,  
        &registerInfo);  

    irp = IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE);  

    if (irp == NULL) 
    {  
        //IoAllocateIrp failed.
        status = STATUS_INSUFFICIENT_RESOURCES;  
        goto ExitRegisterCompositeDriver;    
    }  

    nextSp = IoGetNextIrpStackLocation(irp);  

    bufSize = parentFdoExt->numFunctions * sizeof(USBD_FUNCTION_HANDLE);  

    buffer = ExAllocatePoolWithTag (NonPagedPool, bufSize, POOL_TAG);  

    if (buffer == NULL) 
    {  
        // Memory alloc for function-handles failed.
        status = STATUS_INSUFFICIENT_RESOURCES;  
        goto ExitRegisterCompositeDriver;    
    }  

    nextSp->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;     
    nextSp->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_REGISTER_COMPOSITE_DRIVER;  

    //Set the input buffer in Argument1      
    nextSp->Parameters.Others.Argument1 = &registerInfo;  

    //Set the output buffer in SystemBuffer field for USBD_FUNCTION_HANDLE.      
    irp->AssociatedIrp.SystemBuffer = buffer;  

    // Pass the IRP down to the next device object in the stack. Not shown.
    status = CallNextDriverSync(parentFdoExt, irp, FALSE);  

    if (!NT_SUCCESS(status))
    {  
        //Failed to register the composite driver.
        goto ExitRegisterCompositeDriver;    
    }  

    parentFdoExt->compositeDriverRegistered = TRUE;  

    parentFdoExt->functionHandleArray = (PUSBD_FUNCTION_HANDLE) buffer;  

End:  
    if (!NT_SUCCESS(status)) 
    {  
        if (buffer != NULL) 
        {  
            ExFreePoolWithTag (buffer, POOL_TAG);  
            buffer = NULL;  
        }  
    }  

    if (irp != NULL) 
    {  
        IoFreeIrp(irp);  
        irp = NULL;  
    }  

    return;  
}
```

### <a name="unregister-the-composite-device"></a>取消注册复合设备

1.  通过调用[**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)分配 irp，并通过调用[**IOGETNEXTIRPSTACKLOCATION**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)获取指向 IRP 的第一个堆栈位置 ([**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) 。
2.  通过将[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的**DeviceIoControl. IoControlCode**成员设置为[**IOCTL \_ 内部 \_ USB \_ 注销 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)来生成请求。
3.  通过将 IRP 传递到下一个堆栈位置来调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 以发送请求。

[**IOCTL \_ 内部 \_ USB \_ 注销 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)请求将由复合驱动程序在 "删除设备" 例程的上下文中发送一次。 请求的目的是删除 USB 驱动程序堆栈与复合驱动程序及其枚举函数之间的关联。 请求还会清理为维护该关联而创建的所有资源，以及在上一个注册请求中返回的所有函数句柄。

下面的代码示例演示如何生成并发送请求以取消注册复合设备。 该示例假设已通过注册请求注册了复合驱动程序，如本主题前面所述。

```ManagedCPlusPlus
VOID  UnregisterCompositeDriver(  
    PPARENT_FDO_EXT parentFdoExt )  
{  
    PIRP                irp;  
    PIO_STACK_LOCATION  nextSp;  
    NTSTATUS            status;  

    PAGED_CODE();  

    irp = IoAllocateIrp(parentFdoExt->topDevObj->StackSize, FALSE);  

    if (irp == NULL) 
    {  
        //IoAllocateIrp failed.
        status = STATUS_INSUFFICIENT_RESOURCES;  
        return;  
    }  

    nextSp = IoGetNextIrpStackLocation(irp);  

    nextSp->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;     
    nextSp->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_UNREGISTER_COMPOSITE_DRIVER;  

    // Pass the IRP down to the next device object in the stack. Not shown.
    status = CallNextDriverSync(parentFdoExt, irp, FALSE);  

    if (NT_SUCCESS(status)) 
    {  
        parentFdoExt->compositeDriverRegistered = FALSE;      
    }  

    IoFreeIrp(irp);  

    return;  
}
```

## <a name="related-topics"></a>相关主题
[**IOCTL \_ 内部 \_ USB \_ 注册 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_register_composite_device)  
[**IOCTL \_ 内部 \_ USB \_ 注销 \_ 复合 \_ 设备**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_unregister_composite_device)