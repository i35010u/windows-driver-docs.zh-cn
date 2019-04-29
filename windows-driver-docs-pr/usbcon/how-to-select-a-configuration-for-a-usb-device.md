---
Description: 在本主题中，您将学习有关如何选择一种配置中的通用串行总线 (USB) 设备。
title: 如何选择 USB 设备的配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d3f0877c8f73c5a464ea76f21fd5c747faefe85
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366043"
---
# <a name="how-to-select-a-configuration-for-a-usb-device"></a>如何选择 USB 设备的配置


在本主题中，您将学习有关如何选择一种配置中的通用串行总线 (USB) 设备。

若要选择 USB 设备的配置，设备的客户端驱动程序必须选择至少一个支持的配置，并指定要使用的每个接口的替代设置。 客户端驱动程序包中的这些选择*选择配置请求*并将请求发送到由 Microsoft 提供的 USB 驱动程序堆栈，专门 USB 总线驱动程序 （USB 集线器 PDO）。 USB 总线驱动程序选择指定的配置和设置通信通道中的每个接口或*管道*，到在界面中每个终结点。 在请求完成后，客户端驱动程序接收所选配置的句柄并在活动备用设置为每个接口中定义的终结点处理管道。 然后，客户端驱动程序可以使用收到的句柄更改配置设置还可以发送 I/O 读取和写入请求发送到特定终结点。

客户端驱动程序将选择配置请求发送[USB 请求块 (URB)](communicating-with-a-usb-device.md)的类型 URB\_函数\_选择\_配置。 本主题中的过程介绍如何使用[ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406243)例程，以生成该 URB。 例程为 URB 分配内存，并将格式对于选择配置的请求，URB 并 URB 的地址返回到客户端驱动程序。

或者，你可以分配[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构，然后手动或通过调用格式设置 URB [ **UsbBuildSelectConfigurationRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538968)宏。

### <a name="prerequisites"></a>系统必备

-   在 Windows 8 中， [ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406243)替换[ **USBD\_CreateConfigurationRequestEx**](https://msdn.microsoft.com/library/windows/hardware/ff539029).
-   在发送前选择配置请求，必须具有客户端驱动程序的注册与 USB 驱动程序堆栈的 USBD 句柄。 若要创建 USBD 句柄调用[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)。
-   请确保您已获得配置描述符 ([**USB\_配置\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539241)结构) 的要选择的配置。 通常情况下，提交类型 URB URB\_函数\_获取\_描述符\_FROM\_设备 (请参阅[  **\_URB\_控件\_描述符\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff540357)) 来检索有关设备配置信息。 有关详细信息，请参阅[USB 配置描述符](usb-configuration-descriptors.md)。

<a name="instructions"></a>说明
------------

### <a href="" id="create-an-array-of-usbd-interface-list-entry-structures-"></a>步骤 1:创建一个数组 USBD\_接口\_列表\_项结构。

1.  在配置中获取接口的数量。 此信息包含在**bNumInterfaces**的成员[ **USB\_配置\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539241)结构。
2.  创建的数组[ **USBD\_界面\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff539076)结构。 数组中的元素数必须是一个多个接口的数量。 通过调用初始化数组[ **RtlZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff563610)。

    客户端驱动程序指定备用的设置中启用的数组中每个接口[ **USBD\_界面\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff539076)结构。

    -   **InterfaceDescriptor**的每个结构成员指向包含替代设置的接口描述符。
    -   **接口**的每个结构成员将指向[ **USBD\_接口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539068)结构，其中包含管道的信息在其**管道**成员。 **管道**存储有关备用的设置中定义每个终结点的信息。

3.  在配置中获取每个接口 （或其备用设置） 的接口描述符。 你可以通过调用来获取这些接口描述符[ **USBD\_ParseConfigurationDescriptorEx**](https://msdn.microsoft.com/library/windows/hardware/ff539102)。

    **有关函数的 USB 复合设备驱动程序：  **

    如果 USB 设备是复合设备，由 Microsoft 提供选择的配置[USB 通用父驱动程序](usb-common-class-generic-parent-driver.md)(Usbccgp.sys)。 客户端驱动程序，这是一个功能的驱动程序的复合设备，无法更改的配置，但该驱动程序仍可发送通过 Usbccgp.sys 选择配置请求。

    在发送前该请求，客户端驱动程序必须提交 URB\_函数\_获取\_描述符\_FROM\_设备的请求。 在响应中，检索 Usbccgp.sys*部分配置描述符*，其中仅包含接口描述符和其他适用于为其加载客户端驱动程序的特定函数的描述符。 中报告接口的数量**bNumInterfaces**部分配置描述符字段不超过整个 USB 复合设备定义的接口的总数。 此外，在一个部分配置描述符，接口描述符的**bInterfaceNumber**指示相对于整个设备实际接口数。 例如，Usbccgp.sys 可能报告的部分配置描述符**bNumInterfaces**值为 2 和**bInterfaceNumber**值为 4 的第一个接口。 请注意，接口数大于接口报告的数量。

    在枚举中的部分配置的接口，避免计算基于接口的数量的接口数字搜索接口。 在前面的示例中，如果[ **USBD\_ParseConfigurationDescriptorEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539102)从零开始、 结束的循环中调用`(bNumInterfaces - 1)`，并递增 （指定的接口索引在中*InterfaceNumber*参数) 在每个迭代中，该例程无法获取正确的接口。 相反，请确保您在-1 表示通过搜索配置描述符中的所有接口的*InterfaceNumber*。 有关实现的详细信息，请参阅本部分中的代码示例。

    有关如何 Usbccgp.sys 处理客户端驱动程序发送一个选择配置的请求的信息，请参阅[配置 Usbccgp.sys 选择非默认 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)。

4.  对于数组中每个元素 （除了最后一个元素），设置**InterfaceDescriptor**成员添加到接口描述符的地址。 对于数组中的第一个元素，将设置**InterfaceDescriptor**成员添加到表示在配置中的第一个接口的接口描述符的地址。 同样对于*n*th 元素在数组中，设置**InterfaceDescriptor**成员添加到表示的接口描述符地址*n*中的第接口配置。
5.  **InterfaceDescriptor**的最后一个元素的成员必须设置为 NULL。

### <a href="" id="get-a-pointer-to-an-urb-allocated-by-the-usb-driver-stack-"></a>步骤 2:获取一个指向分配的 USB 驱动程序堆栈 URB。

接下来，调用[ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406243)通过指定要选择的配置和填充的数组[ **USBD\_界面\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff539076)结构。 例程将执行以下任务：

-   创建 URB 和使用指定的配置、 其接口和终结点，相关信息填充它，并将请求类型设置为 URB\_函数\_选择\_配置。
-   在该 URB 分配[ **USBD\_界面\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539068)的客户端驱动程序指定每个接口描述符结构。
-   集**接口**的成员*n*个元素，调用方提供[ **USBD\_接口\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff539076)到相应的地址数组[ **USBD\_接口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539068) URB 中的结构。
-   初始化**InterfaceNumber**， **AlternateSetting**， **NumberOfPipes**，**管道\[我\]。最大传输大小**，并**管道\[我\]。PipeFlags**成员。

    **请注意**  在 Windows 7 和前面部分中，客户端驱动程序创建选择配置请求 URB 通过调用[ **USBD\_CreateConfigurationRequestEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539029). 在 Windows 2000 **USBD\_CreateConfigurationRequestEx**初始化**管道\[我\]。最大传输大小**到单个 URB 读/写请求的默认最大传输大小。 客户端驱动程序可以指定不同的最大传输大小以**管道\[我\]。最大传输大小**。 USB 堆栈将忽略此值在 Windows XP、 Windows Server 2003 和更高版本的操作系统。 有关详细信息**最大传输大小**，请参阅"设置 USB 传输和数据包大小"中[USB 带宽分配](usb-bandwidth-allocation.md)。

### <a href="" id="submit-the-urb-to-the-usb-driver-stack-"></a>步骤 3:提交到 USB 驱动程序堆栈 URB。

若要提交到 USB 驱动程序堆栈 URB，客户端驱动程序必须发送[ **IOCTL\_内部\_USB\_提交\_URB** ](https://msdn.microsoft.com/library/windows/hardware/ff537271) I/O 控制请求。 有关提交 URB 信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

收到后 URB，USB 驱动程序堆栈填充其余的每个成员[ **USBD\_界面\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539068)结构。 具体而言，**管道**的有关接口的终结点与关联的管道的信息填充数组成员。

### <a href="" id="on-request-completion--inspect-the-usbd-interface-information-structures-and-the-urb-"></a>步骤 4:请求完成后，检查 USBD\_接口\_信息结构和 URB。

堆栈请求 IRP USB 驱动程序堆栈之后，返回的备用设置和中的相关的接口的列表[ **USBD\_界面\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff539076)数组。

1.  **管道**的每个成员[ **USBD\_接口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539068)结构的数组的点[ **USBD\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539114)包含有关与该特定接口的每个终结点相关联的管道的信息的结构。 客户端驱动程序可以获取管道中的句柄**管道\[我\]。PipeHandle**以及使用它们来将 I/O 请求发送到特定的管道。 **管道\[我\]。PipeType**成员指定的终结点和该管道支持的传输类型。

2.  内**UrbSelectConfiguration** URB 的成员，USB 驱动程序堆栈返回可用于通过提交类型 URB 的另一个 URB 选择备用接口设置的句柄\_函数\_选择\_接口 (*选择接口请求*)。 若要分配并生成该请求的 URB 结构时，调用[ **USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)。

    如果带宽不足，对等时，控件的支持，中断已启用的接口中的终结点，选择配置请求和选择接口请求可能会失败。 在这种情况下，USB 总线驱动程序设置**状态**USBD URB 标头的成员\_状态\_否\_带宽。

下面的代码示例演示如何创建一个数组[ **USBD\_界面\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff539076)结构和调用[ **USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)。 该示例通过调用 SubmitUrbSync 以同步方式发送请求。 若要查看 SubmitUrbSync 代码示例，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

```ManagedCPlusPlus
/*++

Routine Description:
This helper routine selects the specified configuration.

Arguments:
USBDHandle - USBD handle that is retrieved by the 
client driver in a previous call to the USBD_CreateHandle routine.

ConfigurationDescriptor - Pointer to the configuration
descriptor for the device. The caller receives this pointer
from the URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE request.

Return Value: NT status value
--*/

NTSTATUS SelectConfiguration (PDEVICE_OBJECT DeviceObject,
                              PUSB_CONFIGURATION_DESCRIPTOR ConfigurationDescriptor)
{
    PDEVICE_EXTENSION deviceExtension;
    PIO_STACK_LOCATION nextStack;
    PIRP irp;
    PURB urb = NULL;

    KEVENT    kEvent;
    NTSTATUS ntStatus;    

    PUSBD_INTERFACE_LIST_ENTRY   interfaceList = NULL; 
    PUSB_INTERFACE_DESCRIPTOR    interfaceDescriptor = NULL;
    PUSBD_INTERFACE_INFORMATION  Interface = NULL;
    USBD_PIPE_HANDLE             pipeHandle;

    ULONG                        interfaceIndex;

    PUCHAR StartPosition = (PUCHAR)ConfigurationDescriptor;

    deviceExtension = (PDEVICE_EXTENSION)DeviceObject->DeviceExtension;

    // Allocate an array for the list of interfaces
    // The number of elements must be one more than number of interfaces.
    interfaceList = (PUSBD_INTERFACE_LIST_ENTRY)ExAllocatePool (
        NonPagedPool, 
        sizeof(USBD_INTERFACE_LIST_ENTRY) *
        (deviceExtension->NumInterfaces + 1));

    if(!interfaceList)
    {
        //Failed to allocate memory
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    // Initialize the array by setting all members to NULL.
    RtlZeroMemory (interfaceList, sizeof (
        USBD_INTERFACE_LIST_ENTRY) *
        (deviceExtension->NumInterfaces + 1));

    // Enumerate interfaces in the configuration.
    for ( interfaceIndex = 0; 
        interfaceIndex < deviceExtension->NumInterfaces; 
        interfaceIndex++) 
    {
        interfaceDescriptor = USBD_ParseConfigurationDescriptorEx(
            ConfigurationDescriptor, 
            StartPosition, // StartPosition 
            -1,            // InterfaceNumber
            0,             // AlternateSetting
            -1,            // InterfaceClass
            -1,            // InterfaceSubClass
            -1);           // InterfaceProtocol

        if (!interfaceDescriptor) 
        {
            ntStatus = STATUS_INSUFFICIENT_RESOURCES;
            goto Exit;
        }

        // Set the interface entry
        interfaceList[interfaceIndex].InterfaceDescriptor = interfaceDescriptor;
        interfaceList[interfaceIndex].Interface = NULL;

        // Move the position to the next interface descriptor
        StartPosition = (PUCHAR)interfaceDescriptor + interfaceDescriptor->bLength;

    }

    // Make sure that the InterfaceDescriptor member of the last element to NULL.
    interfaceList[deviceExtension->NumInterfaces].InterfaceDescriptor = NULL;

    // Allocate and build an URB for the select-configuration request.
    ntStatus = USBD_SelectConfigUrbAllocateAndBuild(
        deviceExtension->UsbdHandle, 
        ConfigurationDescriptor, 
        interfaceList,
        &urb);

    if(!NT_SUCCESS(ntStatus)) 
    {
        goto Exit;
    }

    // Allocate the IRP to send the buffer down the USB stack.
    // The IRP will be freed by IO manager.
    irp = IoAllocateIrp((deviceExtension->NextDeviceObject->StackSize)+1, TRUE);  

    if (!irp)
    {
        //Irp could not be allocated.
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    ntStatus = SubmitUrbSync( 
        deviceExtension->NextDeviceObject, 
        irp, 
        urb, 
        CompletionRoutine);

    // Enumerate the pipes in the interface information array, which is now filled with pipe
    // information.

    for ( interfaceIndex = 0; 
        interfaceIndex < deviceExtension->NumInterfaces; 
        interfaceIndex++) 
    {
        ULONG i;

        Interface = interfaceList[interfaceIndex].Interface;

        for(i=0; i < Interface->NumberOfPipes; i++) 
        {
            pipeHandle = Interface->Pipes[i].PipeHandle;

            if (Interface->Pipes[i].PipeType == UsbdPipeTypeInterrupt)
            {
                deviceExtension->InterruptPipe = pipeHandle;
            }
            if (Interface->Pipes[i].PipeType == UsbdPipeTypeBulk && USB_ENDPOINT_DIRECTION_IN (Interface->Pipes[i].EndpointAddress))
            {
                deviceExtension->BulkInPipe = pipeHandle;
            }
            if (Interface->Pipes[i].PipeType == UsbdPipeTypeBulk && USB_ENDPOINT_DIRECTION_OUT (Interface->Pipes[i].EndpointAddress))
            {
                deviceExtension->BulkOutPipe = pipeHandle;
            }
        }
    }

Exit:

    if(interfaceList) 
    {
        ExFreePool(interfaceList);
        interfaceList = NULL;
    }

    if (urb)
    {
        USBD_UrbFree( deviceExtension->UsbdHandle, urb); 
    }


    return ntStatus;

}

NTSTATUS CompletionRoutine ( PDEVICE_OBJECT DeviceObject,
                            PIRP           Irp,
                            PVOID          Context)
{
    PKEVENT kevent;

    kevent = (PKEVENT) Context;

    if (Irp->PendingReturned == TRUE)
    {
        KeSetEvent(kevent, IO_NO_INCREMENT, FALSE);
    }

    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "Select-configuration request completed. \n" ));


    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

<a name="remarks"></a>备注
-------

**禁用的 USB 设备的配置：  **

若要禁用的 USB 设备，创建和提交包含 NULL 配置描述符的选择配置请求。 对于该类型的请求，可以重复使用你针对设备中选择一个配置的请求创建 URB。 或者，你可以通过调用来分配新 URB [ **USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)。 然后再提交请求，必须通过使用格式 URB [ **UsbBuildSelectConfigurationRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538968)宏，如下面的代码示例中所示。

```ManagedCPlusPlus
URB Urb;
UsbBuildSelectConfigurationRequest(
  &Urb,
  sizeof(_URB_SELECT_CONFIGURATION),
  NULL
);
```

## <a name="related-topics"></a>相关主题
[配置 Usbccgp.sys 选择非默认 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)  
[USB 设备配置](configuring-usb-devices.md)  
[分配和构建 URBs](how-to-add-xrb-support-for-client-drivers.md)  



