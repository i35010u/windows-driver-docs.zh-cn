---
description: 本主题概述了 USB 管道，并介绍了 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所需的步骤。
title: 如何枚举 USB 管道
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 250002cf18b82306549692f956e6f74dcc220fc9
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717464"
---
# <a name="how-to-enumerate-usb-pipes"></a>如何枚举 USB 管道


本主题概述了 USB 管道，并介绍了 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所需的步骤。

*USB 终结点*是设备中客户端驱动程序向其发送数据或从中接收数据的缓冲区。 若要发送或接收数据，客户端驱动程序会将 i/o 传输请求提交到 USB 驱动程序堆栈，该堆栈会向主机控制器提供数据。 然后，主机控制器遵循特定的协议 (，具体取决于终结点类型：批量、中断或同步) ，用于构建将数据传入或传出设备的请求。 数据传输的所有详细信息都是从客户端驱动程序中提取的。 只要客户端驱动程序提交格式正确的请求，USB 驱动程序堆栈就会处理请求，并将数据传输到设备。

在设备配置过程中，USB 驱动程序堆栈会在主机端) 为 USB 接口中定义的每个设备终结点及其活动的备用设置创建一个 *usb 管道* (。 USB 管道是主机控制器与终结点之间的信道。 对于客户端驱动程序，管道是端点的逻辑抽象。 为了发送数据传输，驱动程序必须获取与作为传输目标的终结点关联的管道句柄。 当驱动程序希望在出现错误情况时中止传输或重置管道时，还需要管道句柄。

管道的所有属性都是从关联的终结点描述符派生的。 例如，根据终结点的类型，USB 驱动程序堆栈为管道分配一个类型。 对于大容量终结点，USB 驱动程序堆栈会创建大容量管道;对于同步终结点，将创建一个同步管道，依此类推。 另一个重要属性是指主机控制器可以发送到请求中的终结点的数据量。 根据相应的值，客户端驱动程序必须确定传输缓冲区的布局。

Windows Driver Foundation (WDF) 在 [内核模式驱动程序框架](../wdf/index.md) 和 [用户模式驱动程序框架](../wdf/index.md) 中提供专用 i/o 目标对象，以简化客户端驱动程序的多个配置任务。 通过使用这些对象，客户端驱动程序可以检索有关当前配置的信息，如接口数、每个接口内的备用设置及其终结点。 其中一个对象（称为 *目标管道对象*）执行与终结点相关的任务。 本主题说明如何使用目标管道对象获取管道信息。

对于 Windows 驱动模型 (WDM) 客户端驱动程序，USB 驱动程序堆栈返回 [**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information) 结构的数组。 数组中的元素数取决于为所选配置中接口的活动备用设置定义的终结点的数量。 每个元素都包含有关为特定终结点创建的管道的信息。 有关选择配置和获取管道信息阵列的信息，请参阅如何为 [USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。

## <a name="what-you-need-to-know"></a>须知内容


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](../wdf/index.md)
-   [用户模式驱动程序框架](../wdf/index.md)

### <a name="prerequisites"></a>先决条件

在客户端驱动程序可以枚举管道之前，请确保满足以下要求：

-   客户端驱动程序必须已创建框架 USB 目标设备对象。

    如果使用 Microsoft Visual Studio Professional 2012 随附的 USB 模板，则模板代码会执行这些任务。 模板代码会获取目标设备对象的句柄并将其存储在设备上下文中。

    **KMDF 客户端驱动程序：**

    KMDF 客户端驱动程序必须调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) 方法来获取 WDFUSBDEVICE 句柄。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md) 中的“设备源代码”。

    **UMDF 客户端驱动程序：**

    UMDF 客户端驱动程序必须通过查询框架目标设备对象获取 [**IWDFUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) 指针。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构 (UMDF)](understanding-the-umdf-template-code-for-usb.md) 中的“[**IPnpCallbackHardware**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware) 实现和特定于 USB 的任务”。

-   设备必须具有活动配置。

    如果使用的是 USB 模板，则代码将选择每个接口中的第一个配置和默认备用设置。 有关如何更改此默认设置的信息，请参阅 [如何在 USB 接口中选择替代设置](select-a-usb-alternate-setting.md)。

    **KMDF 客户端驱动程序：**

    KMDF 客户端驱动程序必须调用 [**WdfUsbTargetDeviceSelectConfig**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) 方法。

    **UMDF 客户端驱动程序：**

    对于 UMDF 客户端驱动程序，框架为该配置中的每个接口选择第一个配置和默认备用设置。

<a name="instructions"></a>Instructions
------------

### <a name="getting-usb-pipe-handles---kmdf-client-driver"></a>获取 USB 管道句柄-KMDF 客户端驱动程序

此框架表示由 USB 驱动程序堆栈打开的每个管道，作为 USB 目标管道对象。 KMDF 客户端驱动程序可以访问目标管道对象的方法，以获取有关管道的信息。 若要执行数据传输，客户端驱动程序必须具有 WDFUSBPIPE 管道句柄。 若要获取管道句柄，驱动程序必须枚举活动配置的接口和备用设置，然后枚举每个设置中定义的终结点。 对于每个数据传输，执行枚举操作可能很昂贵。 因此，一种方法是在配置设备后获取管道句柄，并将其存储在驱动程序定义的设备上下文中。 当驱动程序收到数据传输请求时，驱动程序可以从设备上下文中检索所需的管道句柄，并使用它们来发送请求。 如果客户端驱动程序更改了设备的配置，例如，选择备用设置，则驱动程序还必须使用新的管道句柄刷新设备上下文。 否则，驱动程序可能会错误地将传输请求发送到陈旧的管道句柄。

**注意**  控制传输不需要管道句柄。
若要发送控制传输请求，WDF 客户端驱动程序将调用由框架设备对象公开的 **WdfUsbDevicexxxx** 方法。 这些方法需要 WDFUSBDEVICE 句柄来启动面向默认终结点的控制传输。 对于此类传输，请求的 i/o 目标是默认终结点，由 WDFUSBPIPE 句柄抽象的 WDFIOTARGET 句柄表示。 在设备级别，WDFUSBDEVICE 句柄是对默认终结点的 WDFUSBPIPE 句柄的抽象。

有关发送控制传输和 KMDF 方法的信息，请参阅 [如何发送 USB 控件传输](usb-control-transfer.md)。



1.  扩展设备上下文结构以存储管道句柄。

    如果知道设备中的终结点，请添加 WDFUSBPIPE 成员来存储关联的 USB 管道句柄，从而扩展设备上下文结构。 例如，可以扩展设备上下文结构，如下所示：

    ```cpp
    typedef struct _DEVICE_CONTEXT {  
        WDFUSBDEVICE    UsbDevice;  
        WDFUSBINTERFACE UsbInterface;  
        WDFUSBPIPE      BulkReadPipe;   // Pipe opened for the bulk IN endpoint.
        WDFUSBPIPE      BulkWritePipe;  // Pipe opened for the bulk IN endpoint.
        WDFUSBPIPE      InterruptPipe;  // Pipe opened for the interrupt IN endpoint.
        WDFUSBPIPE      StreamInPipe;   // Pipe opened for stream IN endpoint.
        WDFUSBPIPE      StreamOutPipe;  // Pipe opened for stream OUT endpoint.
        UCHAR           NumberConfiguredPipes;  // Number of pipes opened.
        ...
        ...                                     // Other members. Not shown.

    } DEVICE_CONTEXT, *PDEVICE_CONTEXT;  
    ```

2.  声明管道上下文结构。

    每个管道都可以在另一个称为 *管道上下文*的结构中存储终结点相关的特征。 与设备上下文类似，管道上下文是由客户端驱动程序定义的数据结构 () 用于存储与终结点关联的管道的信息。 在设备配置过程中，客户端驱动程序会将其管道上下文的指针传递到框架。 框架根据结构的大小分配内存块，并使用框架 USB 目标管道对象存储指向该内存位置的指针。 客户端驱动程序可以使用指针在管道上下文的成员中访问和存储管道信息。

    ```cpp
    typedef struct _PIPE_CONTEXT {  

        ULONG MaxPacketSize;
        ULONG MaxStreamsSupported;
        PUSBD_STREAM_INFORMATION StreamInfo;
    } PIPE_CONTEXT, *PPIPE_CONTEXT;  

    WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(PIPE_CONTEXT, GetPipeContext)  

    ```

    在此示例中，管道上下文存储可以在一次传输中发送的最大字节数。 客户端驱动程序可以使用该值来确定传输缓冲区的大小。 声明还包括 [**具有 NAME 宏的 WDF \_ DECLARE \_ 上下文类型，该 \_ 类型 \_ 用于 \_ **](../wdf/wdf-declare-context-type-with-name.md) 生成内联函数 GetPipeContext。 客户端驱动程序可调用该函数来检索指向存储管道上下文的内存块的指针。

    有关上下文的详细信息，请参阅 [框架对象上下文空间](../wdf/framework-object-context-space.md)。

    若要将指针传递到框架，客户端驱动程序首先通过调用 [**WDF \_ 对象 \_ 属性 \_ INIT \_ 上下文 \_ 类型**](../wdf/wdf-object-attributes-init-context-type.md)来初始化其管道上下文。 然后，在调用 [**WdfUsbTargetDeviceSelectConfig**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) (时，将指针传递给管道上下文以选择配置) 或 [**WdfUsbInterfaceSelectSetting**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting) (以便选择备用设置) 。

3.  设备配置请求完成后，枚举接口并获取已配置管道的管道句柄。 你将需要以下信息集：

    -   包含当前设置的接口的 WDFUSBINTERFACE 句柄。 可以通过在活动配置中枚举接口来获取该句柄。 或者，如果在 WdfUsbTargetDeviceSelectConfig 中提供了指向[**WDF \_ USB \_ 设备 \_ \_ \_ **](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_select_config_params)的指针，请在[**WdfUsbTargetDeviceSelectConfig**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)中获取单接口设备的 (的句**Type.SingleInterface.Config**柄，) 或**MultiInterface UsbInterface**成员 (用于多接口设备) 。
    -   为当前设置中的终结点打开的管道的数目。 可以通过调用 [**WdfUsbInterfaceGetNumConfiguredPipes**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumconfiguredpipes) 方法在特定接口上获取该数字。
    -   所有已配置管道的 WDFUSBPIPE 句柄。 可以通过调用 [**WdfUsbInterfaceGetConfiguredPipe**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe) 方法获取该句柄。

    获取管道句柄之后，客户端驱动程序可以调用方法来确定管道的类型和方向。 此驱动程序可以在 [**WDF \_ USB \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information) 结构中获取有关该终结点的信息。 驱动程序可以通过调用 [**WdfUsbTargetPipeGetInformation**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation) 方法来获取填充的结构。 或者，驱动程序可以在 [**WdfUsbInterfaceGetConfiguredPipe**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe) 调用中提供指向结构的指针。

下面的代码示例枚举当前设置中的管道。 它获取设备的大容量和中断终结点的管道句柄，并将其存储在驱动程序的设备上下文结构中。 它将每个终结点的最大数据包大小存储在关联的管道上下文中。 如果终结点支持流，它将通过调用 OpenStreams 例程打开静态流。 OpenStreams 的实现显示在如何在 [USB 大容量终结点中打开和关闭静态流](how-to-open-streams-in-a-usb-endpoint.md)中。

若要确定特定大容量终结点是否支持静态流，客户端驱动程序将检查终结点描述符。 在名为 RetrieveStreamInfoFromEndpointDesc 的 helper 例程中实现该代码，如以下代码块中所示。

```cpp
NTSTATUS  
    FX3EnumeratePipes(  
    _In_ WDFDEVICE Device)

{  

    NTSTATUS                    status;  
    PDEVICE_CONTEXT             pDeviceContext;  

    UCHAR                       i; 

    PPIPE_CONTEXT               pipeContext;

    WDFUSBPIPE                  pipe; 

    WDF_USB_PIPE_INFORMATION    pipeInfo;  

    PAGED_CODE();  

    pDeviceContext = GetDeviceContext(Device);

    // Get the number of pipes in the current altenrate setting.
    pDeviceContext->NumberConfiguredPipes = WdfUsbInterfaceGetNumConfiguredPipes(
        pDeviceContext->UsbInterface);

    if (pDeviceContext->NumberConfiguredPipes == 0)
    {
        status = USBD_STATUS_BAD_NUMBER_OF_ENDPOINTS;
        goto Exit;
    }
    else
    {
        status = STATUS_SUCCESS;
    }

    // Enumerate the pipes and get pipe information for each pipe.
    for (i = 0; i < pDeviceContext->NumberConfiguredPipes; i++) 
    {
        WDF_USB_PIPE_INFORMATION_INIT(&pipeInfo); 

        pipe =  WdfUsbInterfaceGetConfiguredPipe(
            pDeviceContext->UsbInterface,  
            i, 
            &pipeInfo); 

        if (pipe == NULL)
        {
            continue;
        }

        pipeContext = GetPipeContext (pipe);

        // If the pipe is a bulk endpoint that supports streams, 
        // If the host controller supports streams, open streams.
        // Use the endpoint as an IN bulk endpoint.
        // Store the maximum packet size.

        if ((WdfUsbPipeTypeBulk == pipeInfo.PipeType) &&
            WdfUsbTargetPipeIsInEndpoint (pipe))
        {

            // Check if this is a streams IN endpoint. If it is,
            // Get the maximum number of streams and store
            // the value in the pipe context.
            RetrieveStreamInfoFromEndpointDesc (
                Device,
                pipe);

            if ((pipeContext->IsStreamsCapable) &&
                (pipeContext->MaxStreamsSupported > 0))
            {           
                status = OpenStreams (
                    Device,
                    pipe);

                if (status != STATUS_SUCCESS)
                {
                    TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                        "%!FUNC! Could not open streams.");

                    pDeviceContext->StreamInPipe = NULL;
                }
                else
                {
                    pDeviceContext->StreamInPipe = pipe;

                    pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

                }
            }
            else
            {
                pDeviceContext->BulkReadPipe = pipe;

                pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

            }

            continue;
        }

        if ((WdfUsbPipeTypeBulk == pipeInfo.PipeType) &&
            WdfUsbTargetPipeIsOutEndpoint (pipe))
        {
            // Check if this is a streams IN endpoint. If it is,
            // Get the maximum number of streams and store
            // the value in the pipe context.
            RetrieveStreamInfoFromEndpointDesc (
                Device,
                pipe);

            if ((pipeContext->IsStreamsCapable) &&
                (pipeContext->MaxStreamsSupported > 0))
            {           
                status = OpenStreams (
                    Device,
                    pipe);

                if (status != STATUS_SUCCESS)
                {
                    TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                        "%!FUNC! Could not open streams.");

                    pDeviceContext->StreamOutPipe = NULL;
                }
                else
                {
                    pDeviceContext->StreamOutPipe = pipe;

                    pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

                }
            }
            else
            {
                pDeviceContext->BulkWritePipe = pipe;

                pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

            }

            continue;
        }

        if ((WdfUsbPipeTypeInterrupt == pipeInfo.PipeType) &&
            WdfUsbTargetPipeIsInEndpoint (pipe))
        {
            pDeviceContext->InterruptPipe = pipe;

            pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

            continue;
        }

    }  


Exit:
    return status;

}
```

下面的代码示例演示一个名为 RetrieveStreamInfoFromEndpointDesc 的 helper 例程，该例程在枚举管道时调用。

在下面的代码示例中，客户端驱动程序将调用前面的 helper 例程 RetrieveStreamInfoFromEndpointDesc，同时枚举管道。 例程首先检查获取配置描述符，并将其分析为检索终结点描述符。 如果管道的终结点描述符包含 USB \_ SUPERSPEED \_ 终结点 \_ 伴随 \_ 描述符 \_ 类型描述符，则驱动程序将检索终结点支持的最大流数。

```cpp
/*++

Routine Description:

This routine parses the configuration descriptor and finds the endpoint
with which the specified pipe is associated.
It then retrieves the maximum number of streams supported by the endpoint.
It stores maximum number of streams in the pipe context.

Arguments:

Device - WDFUSBDEVICE handle to the target device object. 
The driver obtained that handle in a previous call to
WdfUsbTargetDeviceCreateWithParameters.

Pipe - WDFUSBPIPE handle to the target pipe object.

Return Value:

NTSTATUS
++*/

VOID RetrieveStreamInfoFromEndpointDesc (
    WDFDEVICE Device,
    WDFUSBPIPE Pipe)
{
    PDEVICE_CONTEXT                                 deviceContext                = NULL;
    PUSB_CONFIGURATION_DESCRIPTOR                   configDescriptor             = NULL;
    WDF_USB_PIPE_INFORMATION                        pipeInfo;
    PUSB_COMMON_DESCRIPTOR                          pCommonDescriptorHeader      = NULL;
    PUSB_INTERFACE_DESCRIPTOR                       pInterfaceDescriptor         = NULL;
    PUSB_ENDPOINT_DESCRIPTOR                        pEndpointDescriptor          = NULL;
    PUSB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR   pEndpointCompanionDescriptor = NULL;
    ULONG                                           maxStreams;
    ULONG                                           index;
    BOOLEAN                                         found                        = FALSE;
    UCHAR                                           interfaceNumber = 0;
    UCHAR                                           alternateSetting = 1;
    PPIPE_CONTEXT                                   pipeContext = NULL;
    NTSTATUS                                        status;

    PAGED_CODE();

    deviceContext = GetDeviceContext (Device);

    pipeContext = GetPipeContext (Pipe);


    // Get the configuration descriptor of the currently selected configuration
    status = FX3RetrieveConfigurationDescriptor (
        deviceContext->UsbDevice,
        &deviceContext->ConfigurationNumber,
        &configDescriptor);

    if (!NT_SUCCESS (status))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor.");

        status = USBD_STATUS_INAVLID_CONFIGURATION_DESCRIPTOR;

        goto Exit;
    }

    if (deviceContext->ConfigurationNumber == 1)
    {
        alternateSetting = 1;
    }
    else
    {
        alternateSetting = 0;
    }

    // Get the Endpoint Address of the pipe
    WDF_USB_PIPE_INFORMATION_INIT(&pipeInfo);  
    WdfUsbTargetPipeGetInformation (Pipe, &pipeInfo);


    // Parse the ConfigurationDescriptor (including all Interface and
    // Endpoint Descriptors) and locate a Interface Descriptor which
    // matches the InterfaceNumber, AlternateSetting, InterfaceClass,
    // InterfaceSubClass, and InterfaceProtocol parameters.  

    pInterfaceDescriptor = USBD_ParseConfigurationDescriptorEx(
        configDescriptor,
        configDescriptor,
        interfaceNumber,  //Interface number is 0.
        alternateSetting,  // Alternate Setting is 1
        -1, // InterfaceClass, ignore
        -1, // InterfaceSubClass, ignore
        -1  // InterfaceProtocol, ignore
        );

    if (pInterfaceDescriptor == NULL ) 
    {
        // USBD_ParseConfigurationDescriptorEx failed to retrieve Interface Descriptor.
        goto Exit;
    }

    pCommonDescriptorHeader = (PUSB_COMMON_DESCRIPTOR) pInterfaceDescriptor;

    for(index = 0; index < pInterfaceDescriptor->bNumEndpoints; index++) 
    {

        pCommonDescriptorHeader = USBD_ParseDescriptors(
            configDescriptor,
            configDescriptor->wTotalLength,
            pCommonDescriptorHeader,
            USB_ENDPOINT_DESCRIPTOR_TYPE);

        if (pCommonDescriptorHeader == NULL) 
        {
            // USBD_ParseDescriptors failed to retrieve Endpoint Descriptor unexpectedly.
            goto Exit;

        }

        pEndpointDescriptor = (PUSB_ENDPOINT_DESCRIPTOR) pCommonDescriptorHeader;

        // Search an Endpoint Descriptor that matches the EndpointAddress
        if (pEndpointDescriptor->bEndpointAddress == pipeInfo.EndpointAddress)
        {

            found = TRUE;

            break;

        }

        // Skip the current Endpoint Descriptor and search for the next.
        pCommonDescriptorHeader = (PUSB_COMMON_DESCRIPTOR)(((PUCHAR)pCommonDescriptorHeader) 
            + pCommonDescriptorHeader->bLength);

    }

    if (found) 
    {
        // Locate the SuperSpeed Endpoint Companion Descriptor 
        // associated with the endpoint descriptor
        pCommonDescriptorHeader = USBD_ParseDescriptors (
            configDescriptor,
            configDescriptor->wTotalLength,
            pEndpointDescriptor,
            USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR_TYPE);

        if (pCommonDescriptorHeader != NULL) 
        {
            pEndpointCompanionDescriptor = 
                (PUSB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR) pCommonDescriptorHeader;

            maxStreams = pEndpointCompanionDescriptor->bmAttributes.Bulk.MaxStreams;

            if (maxStreams == 0) 
            {

                pipeContext->MaxStreamsSupported = 0;

                pipeContext->IsStreamsCapable = FALSE;
            } 
            else 
            {
                pipeContext->IsStreamsCapable = TRUE;

                pipeContext->MaxStreamsSupported = 1 << maxStreams;

            }

        } 
        else 
        {
            KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, 
                "USBD_ParseDescriptors failed to retrieve SuperSpeed Endpoint Companion Descriptor unexpectedly.\n" ));        
        }

    }
    else
    {
        pipeContext->MaxStreamsSupported = 0;

        pipeContext->IsStreamsCapable = FALSE;
    }

Exit:
    if (configDescriptor)
    {
        ExFreePoolWithTag (configDescriptor, USBCLIENT_TAG);
    }

    return;
}
```

### <a name="getting-pipe-handles---umdf-client-driver"></a>获取管道句柄-UMDF 客户端驱动程序

UMDF 客户端驱动程序使用 COM 基础结构并实现与框架设备对象配对的 COM 回调类。 与 KMDF 驱动程序类似，UMDF 客户端驱动程序在配置设备后只能获取管道信息。 若要获取管道信息，客户端驱动程序必须获取指向包含活动设置的 framework interface 对象的 [**IWDFUsbTargetPipe**](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe) 接口的指针。 使用接口指针，驱动程序可以枚举该设置中的管道，以获取框架目标管道对象公开的 **IWDFUsbTargetPipe** 接口指针。

驱动程序开始枚举管道之前，驱动程序必须知道设备配置和支持的终结点。 根据该信息，驱动程序可以将管道对象存储为类成员变量。

下面的代码示例扩展了随 Visual Studio Professional 2012 一起提供的 USB UMDF 模板。 有关起始代码的说明，请参阅[了解 USB 客户端驱动程序代码结构 (UMDF) ](understanding-the-umdf-template-code-for-usb.md)中的 "[**IPnpCallbackHardware**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"。

扩展 CDevice 类声明，如下所示。 此代码示例假定设备是 OSR FX2 板。 有关描述符布局的信息，请参阅 [USB 设备布局](usb-device-layout.md)。

```cpp
class CMyDevice :
    public CComObjectRootEx<CComMultiThreadModel>,
    public IPnpCallbackHardware
{

public:

    DECLARE_NOT_AGGREGATABLE(CMyDevice)

    BEGIN_COM_MAP(CMyDevice)
        COM_INTERFACE_ENTRY(IPnpCallbackHardware)
    END_COM_MAP()

    CMyDevice() :
        m_FxDevice(NULL),
        m_IoQueue(NULL),
        m_FxUsbDevice(NULL)
    {
    }

    ~CMyDevice()
    {
    }

private:

    IWDFDevice *            m_FxDevice;

    CMyIoQueue *            m_IoQueue;

    IWDFUsbTargetDevice *   m_FxUsbDevice;

    IWDFUsbInterface *      m_pIUsbInterface;  //Pointer to the target interface object.

    IWDFUsbTargetPipe *     m_pIUsbInputPipe;  // Pointer to the target pipe object for the bulk IN endpoint.

    IWDFUsbTargetPipe *     m_pIUsbOutputPipe; // Pointer to the target pipe object for the bulk OUT endpoint.

    IWDFUsbTargetPipe *     m_pIUsbInterruptPipe; // Pointer to the target pipe object for the interrupt endpoint.

private:

    HRESULT
    Initialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit
        );

public:

    static
    HRESULT
    CreateInstanceAndInitialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit,
        __out CMyDevice **Device
        );

    HRESULT
    Configure(
        VOID
        );

    HRESULT                     // Declare a helper function to enumerate pipes.
    ConfigureUsbPipes(  
        );
public:

    // IPnpCallbackHardware methods

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnPrepareHardware(
            __in IWDFDevice *FxDevice
            );

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnReleaseHardware(
        __in IWDFDevice *FxDevice
        );

};
```

在 CDevice 类定义中，实现名为 CreateUsbIoTargets 的帮助器方法。 当驱动程序获取指向目标设备对象的指针后，将从 IPnpCallbackHardware：： OnPrepareHardware 实现调用此方法。

```cpp

HRESULT  CMyDevice::CreateUsbIoTargets()  

    HRESULT                 hr;  
    UCHAR                   NumEndPoints = 0;  

    IWDFUsbInterface *      pIUsbInterface = NULL;  
    IWDFUsbTargetPipe *     pIUsbPipe = NULL;  


    if (SUCCEEDED(hr))   
    {  
        UCHAR NumInterfaces = pIUsbTargetDevice->GetNumInterfaces();  

        WUDF_TEST_DRIVER_ASSERT(1 == NumInterfaces);  

        hr = pIUsbTargetDevice->RetrieveUsbInterface(0, &pIUsbInterface);  
        if (FAILED(hr))  
        {  
            TraceEvents(TRACE_LEVEL_ERROR,   
                        TEST_TRACE_DEVICE,   
                        "%!FUNC! Unable to retrieve USB interface from USB Device I/O Target %!HRESULT!",  
                        hr  
                        );          
        }  
        else  
        {  
            m_pIUsbInterface = pIUsbInterface;  

            DriverSafeRelease (pIUsbInterface); //release creation reference                                
        }
     }  

    if (SUCCEEDED(hr))   
    {  
        NumEndPoints = pIUsbInterface->GetNumEndPoints();  

        if (NumEndPoints != NUM_OSRUSB_ENDPOINTS) 
        {  
            hr = E_UNEXPECTED;  
            TraceEvents(TRACE_LEVEL_ERROR,   
                        TEST_TRACE_DEVICE,   
                        "%!FUNC! Has %d endpoints, expected %d, returning %!HRESULT! ",   
                        NumEndPoints,  
                        NUM_OSRUSB_ENDPOINTS,  
                        hr  
                        );  
        }  
    }  

    if (SUCCEEDED(hr))   
    {  
        for (UCHAR PipeIndex = 0; PipeIndex < NumEndPoints; PipeIndex++)  
        {  
            hr = pIUsbInterface->RetrieveUsbPipeObject(PipeIndex,   
                                                  &pIUsbPipe);  

            if (FAILED(hr))  
            {  
                TraceEvents(TRACE_LEVEL_ERROR,   
                            TEST_TRACE_DEVICE,   
                            "%!FUNC! Unable to retrieve USB Pipe for PipeIndex %d, %!HRESULT!",  
                            PipeIndex,  
                            hr  
                            );          
            }  
            else  
            {  
                if ( pIUsbPipe->IsInEndPoint() )  
                {  
                    if ( UsbdPipeTypeInterrupt == pIUsbPipe->GetType() )  
                    {  
                        m_pIUsbInterruptPipe = pIUsbPipe;  
                    }  
                    else if ( UsbdPipeTypeBulk == pIUsbPipe->GetType() )  
                    {  
                        m_pIUsbInputPipe = pIUsbPipe;  
                    }  
                    else  
                    {  
                        pIUsbPipe->DeleteWdfObject();  
                    }                        
                }  
                else if ( pIUsbPipe->IsOutEndPoint() && (UsbdPipeTypeBulk == pIUsbPipe->GetType()) )  
                {  
                    m_pIUsbOutputPipe = pIUsbPipe;  
                }  
                else  
                {  
                    pIUsbPipe->DeleteWdfObject();  
                }  

                DriverSafeRelease(pIUsbPipe);  //release creation reference
            }  
        }  

        if (NULL == m_pIUsbInputPipe || NULL == m_pIUsbOutputPipe)  
        {  
            hr = E_UNEXPECTED;  
            TraceEvents(TRACE_LEVEL_ERROR,   
                        TEST_TRACE_DEVICE,   
                        "%!FUNC! Input or output pipe not found, returning %!HRESULT!",  
                        hr  
                        );          
        }  
    }  

    return hr;  
}  
```

在 UMDF 中，客户端驱动程序使用管道索引发送数据传输请求。 当管道索引为设置中的终结点打开管道时，它由 USB 驱动程序堆栈分配。 若要获取管道索引，请调用[**IWDFUsbTargetPipe：： GetInformation**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation) 方法。 方法填充 [**WINUSB \_ 管道 \_ 信息**](/windows/win32/api/winusbio/ns-winusbio-_winusb_pipe_information) 结构。 **PipeId**值指示管道索引。

在目标管道上执行读取和写入操作的一种方法是调用 [**IWDFUsbInterface：： GetWinUsbHandle**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle) 以获取 WinUSB 句柄，然后调用 [WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)。 例如，驱动程序可以调用 [**WinUsb \_ ReadPipe**](/windows/win32/api/winusb/nf-winusb-winusb_readpipe) 或 [**WinUsb \_ WritePipe**](/windows/win32/api/winusb/nf-winusb-winusb_writepipe) 函数。 在这些函数调用中，驱动程序必须指定管道索引。 有关详细信息，请参阅 [如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

<a name="remarks"></a>备注
-------

### <a name="pipe-handles-for-wdm-based-client-drivers"></a>基于 WDM 的客户端驱动程序的管道句柄

选择配置后，USB 驱动程序堆栈会将管道设置为设备的每个终结点。 USB 驱动程序堆栈返回 [**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information) 结构的数组。 数组中的元素数取决于为所选配置中接口的活动备用设置定义的终结点的数量。 每个元素都包含有关为特定终结点创建的管道的信息。 有关获取管道句柄的详细信息，请参阅 [如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。

若要生成 i/o 传输请求，客户端驱动程序必须具有与该终结点关联的管道的句柄。 客户端驱动程序可以从数组中[**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)的**PipeHandle**成员获取管道句柄。

除了管道句柄外，客户端驱动程序还需要管道类型。 客户端驱动程序可以通过检查 **PipeType** 成员来确定管道类型。

基于终结点类型，USB 驱动程序堆栈支持不同类型的管道。 客户端驱动程序可以通过检查[**USBD \_ 管道 \_ 信息**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)的**PipeType**成员来确定管道类型。 不同的管道类型需要不同类型的 USB 请求块 (URBs) 执行 i/o 事务。

然后，客户端驱动程序将 URB 提交到 USB 驱动程序堆栈。 USB 驱动程序堆栈处理请求，并将指定数据发送到请求的目标管道。

URB 包含请求的相关信息，例如目标管道句柄、传输缓冲区和长度。 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)联合中的每个结构共享某些成员： **TransferFlags**、 **TransferBuffer**、 **TransferBufferLength**和**TransferBufferMDL**。 **TransferFlags**成员中存在与每个 URB 类型相对应的类型特定标志。 对于所有数据传输 URBs， \_ \_ TransferFlags 中标志的 USBD 传输方向 \_ 指定传输方向。 **TransferFlags** 客户端驱动程序将 USBD \_ 传输 \_ 方向设置 \_ 为标记，以从设备读取数据。 驱动程序清除此标志，将数据发送到设备。 数据可以从驻留在内存中的缓冲区中读取数据或将数据写入该缓冲区。 在任一情况下，驱动程序都会在 **TransferBufferLength** 成员中指定缓冲区的大小。 驱动程序在 **TransferBuffer** 成员中提供常驻缓冲区，并在 **TransferBufferMDL** 成员中提供 MDL。 驱动程序提供的任何一个，另一个必须为 NULL。

## <a name="related-topics"></a>相关主题
[USB i/o 传输](usb-device-i-o.md)  
[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)  
[如何在 USB 界面中选择备用设置](select-a-usb-alternate-setting.md)  
[USB 客户端驱动程序的常见任务](wdk-resources-for-usb-driver-development.md)