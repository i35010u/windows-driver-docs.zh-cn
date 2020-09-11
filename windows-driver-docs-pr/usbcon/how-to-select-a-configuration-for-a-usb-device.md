---
description: 在本主题中，你将了解如何在通用串行总线 (USB) 设备中选择配置。
title: 如何选择 USB 设备的配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55644793e3bf33b2c25919798ed62111b2a84d4d
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009949"
---
# <a name="how-to-select-a-configuration-for-a-usb-device"></a>如何选择 USB 设备的配置


在本主题中，你将了解如何在通用串行总线 (USB) 设备中选择配置。

若要为 USB 设备选择一个配置，设备的客户端驱动程序必须至少选择一个受支持的配置，并指定要使用的每个接口的备用设置。 客户端驱动程序将这些选项打包在 *选择配置请求* 中，并将请求发送到 Microsoft 提供的 usb 驱动程序堆栈，具体而言， (USB 集线器 PDO) 的 usb 总线驱动程序。 USB 总线驱动程序选择指定配置中的每个接口，并为接口中的每个终结点设置一个信道或 *管道*。 请求完成后，客户端驱动程序将接收所选配置的句柄，并为每个接口的活动备用设置中定义的终结点接收管道句柄。 然后，客户端驱动程序可以使用接收的句柄来更改配置设置，以及向特定终结点发送 i/o 读取和写入请求。

客户端驱动程序在 [USB 请求块 ](communicating-with-a-usb-device.md) 中发送选择配置请求 (URB) 类型 URB \_ 函数 \_ 选择 \_ 配置。 本主题中的过程介绍如何使用 [**USBD \_ SelectConfigUrbAllocateAndBuild**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild) 例程来构建该 URB。 例程为 URB 分配内存，为选择配置请求设置 URB 的格式，并向客户端驱动程序返回 URB 的地址。

或者，您可以分配一个 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 结构，然后手动或通过调用 [**USBBUILDSELECTCONFIGURATIONREQUEST**](/previous-versions/ff538968(v=vs.85)) 宏设置 URB 的格式。

### <a name="prerequisites"></a>先决条件

-   在 Windows 8 中， [**USBD \_ SelectConfigUrbAllocateAndBuild**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild) 替换 [**USBD \_ CreateConfigurationRequestEx**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)。
-   在发送选择配置请求之前，必须为客户端驱动程序的注册 USBD 句柄，并使用 USB 驱动程序堆栈。 若要创建 USBD 句柄，请调用 [**USBD \_ CreateHandle**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)。
-   请确保已获取配置描述符 ([**USB \_ 配置 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor) 结构) 要选择的配置。 通常，你可以从设备 (中提交类型 URB \_ 函数 GET 描述符的 URB， \_ \_ \_ \_ 请参阅[** \_ URB \_ 控制 \_ 描述符 \_ 请求**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)) 以检索有关设备配置的信息。 有关详细信息，请参阅 [USB 配置描述符](usb-configuration-descriptors.md)。

<a name="instructions"></a>Instructions
------------

### <a name="step-1-create-an-array-of-usbd_interface_list_entry-structures"></a><a href="" id="create-an-array-of-usbd-interface-list-entry-structures-"></a>步骤1：创建 USBD \_ 接口 \_ 列表 \_ 条目结构的数组。

1.  获取配置中的接口数。 此信息包含在[**USB \_ 配置 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)结构的**bNumInterfaces**成员中。
2.  创建 [**USBD \_ 接口 \_ 列表 \_ 项**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry) 结构的数组。 数组中的元素数必须比接口数量多一个。 通过调用 [**RtlZeroMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)初始化数组。

    客户端驱动程序在 [**USBD \_ interface \_ LIST \_ 条目**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry) 结构的数组中指定要启用的每个接口中的备用设置。

    -   每个结构的 **InterfaceDescriptor** 成员指向包含替代设置的接口描述符。
    -   每个结构的 **接口** 成员指向 [**USBD \_ 接口 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information) 结构，该结构包含其 **管道** 成员中的管道信息。 **管道** 存储有关在备用设置中定义的每个终结点的信息。

3.  获取每个接口的接口描述符 (或) 在配置中的备用设置。 可以通过调用 [**USBD \_ ParseConfigurationDescriptorEx**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)获取这些接口描述符。

    **关于 USB 复合设备的函数驱动程序：  **

    如果 USB 设备是复合设备，则由 Microsoft 提供的 [Usb 通用父驱动程序](usb-common-class-generic-parent-driver.md) ( # A0) 选择该配置。 客户端驱动程序是复合设备的一个函数驱动程序，无法更改配置，但驱动程序仍可以通过 Usbccgp.sys 发送一个选择配置请求。

    在发送该请求之前，客户端驱动程序必须 \_ \_ \_ \_ 从设备请求提交 URB 函数 GET 描述符 \_ 。 作为响应，Usbccgp.sys 会检索 *部分配置描述符* ，其中仅包含与要为其加载客户端驱动程序的特定函数相关的接口描述符和其他说明符。 部分配置描述符的 **bNumInterfaces** 字段中报告的接口数小于为整个 USB 复合设备定义的接口总数。 此外，在部分配置描述符中，接口描述符的 **bInterfaceNumber** 指示相对于整个设备的实际接口号。 例如，Usbccgp.sys 可能会报告第一个接口的 **bNumInterfaces** 值为2且 **bInterfaceNumber** 值为4的部分配置描述符。 请注意，接口号大于所报告的接口数。

    枚举部分配置中的接口时，请避免通过基于接口数量计算接口号来搜索接口。 在前面的示例中，如果在从零开始的循环中调用 [**USBD \_ ParseConfigurationDescriptorEx**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex) ，则在 `(bNumInterfaces - 1)` 每次迭代中的 *InterfaceNumber* 参数) 中指定 (的接口索引，然后，例程将无法获取正确的接口。 相反，请确保在 *InterfaceNumber*中通过传递-1 搜索配置描述符中的所有接口。 有关实现的详细信息，请参阅本节中的代码示例。

    有关 Usbccgp.sys 如何处理客户端驱动程序发送的选择配置请求的信息，请参阅 [配置 Usbccgp.sys 以选择非默认的 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)。

4.  对于数组中最后一个元素) 之外的每个元素 (，请将 **InterfaceDescriptor** 成员设置为接口描述符的地址。 对于数组中的第一个元素，将 **InterfaceDescriptor** 成员设置为表示配置中第一个接口的接口描述符的地址。 同样，对于数组中的第 *n*个元素，将 **InterfaceDescriptor** 成员设置为表示配置中第 *n*个接口的接口描述符的地址。
5.  最后一个元素的 **InterfaceDescriptor** 成员必须设置为 NULL。

### <a name="step-2-get-a-pointer-to-an-urb-allocated-by-the-usb-driver-stack"></a><a href="" id="get-a-pointer-to-an-urb-allocated-by-the-usb-driver-stack-"></a>步骤2：获取指向 USB 驱动程序堆栈所分配的 URB 的指针。

接下来，通过指定要选择的配置以及已填充的[**USBD \_ 接口 \_ 列表 \_ 项**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)结构数组，来调用[**USBD \_ SelectConfigUrbAllocateAndBuild**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild) 。 例程执行以下任务：

-   创建 URB 并使用有关指定配置、其接口和终结点的信息进行填充，并将请求类型设置为 URB \_ 函数 \_ 选择 \_ 配置。
-   在该 URB 中，为客户端驱动程序指定的每个接口描述符分配一个 [**USBD \_ 接口 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information) 结构。
-   将调用方提供的[**USBD \_ 接口 \_ 列表 \_ 项**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)数组的第*n*个元素的**接口**成员设置为 URB 中对应[**USBD \_ 接口 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)结构的地址。
-   初始化 **InterfaceNumber**、 **AlternateSetting**、 **NumberOfPipes**、 **管道 \[ i \] 。MaximumTransferSize**和 **管道 \[ i \] 。PipeFlags** 成员。

    **注意**   在 Windows 7 和早中，客户端驱动程序通过调用[**USBD \_ CreateConfigurationRequestEx**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)为选择配置请求创建了 URB。 在 Windows 2000 **USBD \_ CreateConfigurationRequestEx** 中初始化 **管道 \[ i \] 。MaximumTransferSize** 为单个 URB 读/写请求的默认最大传输大小。 客户端驱动程序可以在管道 i 中指定不同的最大传输大小 ** \[ \] 。MaximumTransferSize**。 在 Windows XP、Windows Server 2003 和更高版本的操作系统中，USB stack 将忽略此值。 有关 **MaximumTransferSize**的详细信息，请参阅 " [usb 带宽分配](usb-bandwidth-allocation.md)" 中的 "设置 Usb 传输和数据包大小"。

### <a name="step-3-submit-the-urb-to-the-usb-driver-stack"></a><a href="" id="submit-the-urb-to-the-usb-driver-stack-"></a>步骤3：将 URB 提交到 USB 驱动程序堆栈。

若要将 URB 提交到 USB 驱动程序堆栈，客户端驱动程序必须发送 [**IOCTL \_ 内部 \_ USB \_ submit \_ URB**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) i/o 控制请求。 有关提交 URB 的信息，请参阅 how [To Submit AN URB](send-requests-to-the-usb-driver-stack.md)。

收到 URB 后，USB 驱动程序堆栈会填充每个 [**USBD \_ 接口 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information) 结构的其余成员。 特别是， **管道** 数组成员用有关与接口的终结点相关联的管道的信息进行填充。

### <a name="step-4-on-request-completion-inspect-the-usbd_interface_information-structures-and-the-urb"></a><a href="" id="on-request-completion--inspect-the-usbd-interface-information-structures-and-the-urb-"></a>步骤4：在请求完成时，请检查 USBD \_ 接口 \_ 信息结构和 URB。

USB 驱动程序堆栈完成请求的 IRP 后，堆栈返回 [**USBD \_ 接口 \_ 列表 \_ 项**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry) 数组中的备用设置和相关接口的列表。

1.  每个[**USBD \_ 接口 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)结构的**Pipes**成员指向一组[**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)结构，其中包含与特定接口的每个终结点相关联的管道的相关信息。 客户端驱动程序可以从管道 i 获取管道句柄 ** \[ \] 。PipeHandle** 并使用它们向特定管道发送 i/o 请求。 **管道 \[ i \] 。PipeType**成员指定该管道支持的终结点和传输的类型。

2.  在 URB 的**UrbSelectConfiguration**成员中，USB 驱动程序堆栈返回一个句柄，可使用该句柄，通过提交类型 URB \_ 函数 \_ select \_ interface () *select-interface request*的另一 URB 来选择备用接口设置。 若要分配并生成该请求的 URB 结构，请调用 [**USBD \_ SelectInterfaceUrbAllocateAndBuild**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)。

    如果带宽不足，无法支持启用的接口中的同步、控制和中断端点，则选择配置请求和选择接口请求可能会失败。 在这种情况下，USB 总线驱动程序将 URB 标头的 **status** 成员设置为 USBD \_ 状态 " \_ 无带宽" \_ 。

下面的示例代码演示如何创建 [**USBD \_ 接口 \_ 列表 \_ 项**](/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry) 结构的数组并调用 [**USBD \_ SelectConfigUrbAllocateAndBuild**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)。 该示例通过调用 SubmitUrbSync 来同步发送请求。 若要查看 SubmitUrbSync 的代码示例，请参阅 how [To Submit AN URB](send-requests-to-the-usb-driver-stack.md)。

```C++
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

**禁用 USB 设备的配置：**

若要禁用 USB 设备，请创建并提交包含空配置描述符的选择配置请求。 对于这种类型的请求，可以重复使用为在设备中选择了配置的请求而创建的 URB。 或者，可以通过调用 [**USBD \_ UrbAllocate**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)来分配新的 URB。 提交请求之前，必须使用 [**UsbBuildSelectConfigurationRequest**](/previous-versions/ff538968(v=vs.85)) 宏格式化 URB，如下面的示例代码所示。

```C++
URB Urb;
UsbBuildSelectConfigurationRequest(
  &Urb,
  sizeof(_URB_SELECT_CONFIGURATION),
  NULL
);
```

## <a name="related-topics"></a>相关主题
[配置 Usbccgp.sys，选择非默认 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)  
[USB 设备配置](configuring-usb-devices.md)  
[分配和构建 URB](how-to-add-xrb-support-for-client-drivers.md)