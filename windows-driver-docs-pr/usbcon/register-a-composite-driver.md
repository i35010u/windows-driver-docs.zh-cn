---
Description: How a USB multi-function device, called a composite driver, registers and unregisters the composite device with the underlying USB driver stack.
title: 如何注册的复合设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e092c6de69302762c0caec881974a95038bd4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564369"
---
# <a name="how-to-register-a-composite-device"></a>如何注册的复合设备


本主题介绍如何称为复合驱动程序，USB 多功能设备的驱动程序可以注册和注销的复合设备与基础的 USB 驱动程序堆栈。 Microsoft 提供驱动程序，Usbccgp.sys，是由 Windows 加载默认复合驱动程序。 本主题中的过程适用于自定义 Windows 驱动程序模型 WDM 基于复合驱动程序，用于替换 Usbccgp.sys。

通用串行总线 (USB) 设备可以提供多个同时处于活动状态的函数。 此类多功能设备也被称为*复合设备*。 例如，复合设备可能定义的键盘功能的函数和鼠标的另一个函数。 通过复合驱动程序枚举设备的功能。 复合驱动程序可以管理这些函数本身中的整体模型或为每个函数创建物理设备对象 (PDOs)。 这些单个 PDOs 由其各自的 USB 函数驱动程序、 键盘驱动程序和鼠标驱动程序管理。

USB 3.0 规范定义了*函数挂起和远程唤醒功能*，使各个函数进入和退出低功耗状态，而不会影响其他函数或整个设备的电源状态。 有关功能的详细信息，请参阅[实现函数挂起复合驱动程序中如何](how-to--implement-remote-and-function-wake-support.md)。

若要使用的功能，复合驱动程序需要将设备注册为基础的 USB 驱动程序堆栈。 此功能适用于 USB 3.0 设备，因为复合驱动程序必须确保基础堆栈支持版本 USBD\_接口\_版本\_602。 通过注册请求，复合的驱动程序：

-   通知基础的 USB 驱动程序堆栈，该驱动程序是负责发送请求以 arm 远程唤醒的函数。 远程唤醒请求被通过 USB 驱动程序堆栈，可将必要的协议请求发送到设备。
-   获取通过 USB 驱动程序堆栈分配的函数的句柄 （一个每个函数） 的列表。 复合驱动程序然后可以使用中的驱动程序函数的句柄请求的函数与句柄关联的远程唤醒。

通常情况下复合驱动程序发送注册请求中的驱动程序 AddDevice 或启动设备例程来处理[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749). 因此，复合的驱动程序释放的资源，如停止设备的驱动程序的卸载例程中注册为分配 ([**IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)) 或删除设备例程 ([**IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738))。

### <a name="prerequisites"></a>先决条件

在发送前注册请求，请确保：

-   必须在设备中的函数数目。 数字可以派生 get 配置请求来检索的描述符。
-   获取以前调用的 USBD 句柄[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)。
-   基础的 USB 驱动程序堆栈支持 USB 3.0 设备。 若要执行此操作，调用[ **USBD\_IsInterfaceVersionSupported** ](https://msdn.microsoft.com/library/windows/hardware/hh406233) ，并将传递 USBD\_接口\_版本\_602 作为要检查的版本。

有关代码示例，请参阅[实现函数挂起复合驱动程序中如何](how-to--implement-remote-and-function-wake-support.md)。
说明
------------

### <a name="register-a-composite-device"></a>注册的复合设备

以下过程描述应如何生成和发送注册请求以复合驱动程序相关联的 USB 驱动程序堆栈。

1.  分配[**复合\_设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh450801)结构，并将其初始化通过调用[**复合\_设备\_功能\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/hh450803)宏。
2.  设置**CapabilityFunctionSuspend**的成员[**复合\_设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh450801)为 1。
3.  分配[**注册\_复合\_设备**](https://msdn.microsoft.com/library/windows/hardware/hh450898)结构，并通过调用初始化结构[ **USBD\_BuildRegisterCompositeDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh406229)例程。 在调用中，指定 USBD 句柄，初始化[**复合\_设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh450801)结构和功能的数量。
4.  分配到 I/O 请求数据包 (IRP) 通过调用[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)并获得到 IRP 的第一个堆栈位置的指针 ([**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)) 通过调用[ **IoGetNextIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549266)。
5.  为大到足以保留函数句柄数组的缓冲区分配内存 (USBD\_函数\_处理)。 数组中的元素数必须为 PDOs 数。
6.  通过设置以下成员的生成请求[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659):
    -   通过设置指定的请求的类型**Parameters.DeviceIoControl.IoControlCode**到[ **IOCTL\_内部\_USB\_注册\_复合\_设备**](https://msdn.microsoft.com/library/windows/hardware/hh450854)。
    -   通过设置指定的输入的参数**Parameters.Others.Argument1**到的地址初始化[**注册\_复合\_设备**](https://msdn.microsoft.com/library/windows/hardware/hh450898)结构。
    -   通过设置来指定输出参数**AssociatedIrp.SystemBuffer**到在步骤 5 中分配的缓冲区。

7.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)将请求发送通过将 IRP 传递到下一步的堆栈位置。

完成后，检查返回的 USB 驱动程序堆栈的函数的句柄数组。 可以将数组存储在驱动程序的设备上下文以供将来使用。

下面的代码示例演示如何生成和发送注册请求。 该示例假定复合驱动程序存储以前获得的函数和 USBD 处理驱动程序的设备上下文中。

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

### <a name="unregister-the-composite-device"></a>注销在复合设备

1.  通过调用分配 IRP [ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)并获得到 IRP 的第一个堆栈位置的指针 ([**IO\_堆栈\_位置** ](https://msdn.microsoft.com/library/windows/hardware/ff550659)) 通过调用[ **IoGetNextIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549266)。
2.  通过设置生成请求**Parameters.DeviceIoControl.IoControlCode**的成员[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)到[ **IOCTL\_内部\_USB\_注销\_复合\_设备**](https://msdn.microsoft.com/library/windows/hardware/hh450855)。
3.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)将请求发送通过将 IRP 传递到下一步的堆栈位置。

[ **IOCTL\_内部\_USB\_注销\_复合\_设备**](https://msdn.microsoft.com/library/windows/hardware/hh450855)请求中的复合驱动程序通过发送一次删除设备例程的上下文。 请求的目的是删除 USB 驱动程序堆栈和复合的驱动程序和其枚举的函数之间的关联。 请求还可清除创建维护该关联的任何资源和以前的注册请求中返回的所有函数句柄。

下面的代码示例演示如何生成和发送请求以取消注册复合设备。 该示例假定，复合的驱动程序以前注册的注册请求通过本主题中前面所述。

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
[**IOCTL\_INTERNAL\_USB\_REGISTER\_COMPOSITE\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/hh450854)  
[**IOCTL\_INTERNAL\_USB\_UNREGISTER\_COMPOSITE\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/hh450855)  



