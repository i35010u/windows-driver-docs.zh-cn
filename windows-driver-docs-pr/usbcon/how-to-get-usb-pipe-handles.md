---
Description: 本主题概述了 USB 管道，并介绍了通过 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所必需的步骤。
title: 如何枚举 USB 管道
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789c7f5416592b7a5af94e2b5b98e29eaf95ff5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386264"
---
# <a name="how-to-enumerate-usb-pipes"></a>如何枚举 USB 管道


本主题概述了 USB 管道，并介绍了通过 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所必需的步骤。

一个*USB 终结点*是中的设备的客户端驱动程序将数据发送到或接收中的数据的缓冲区。 若要发送或接收数据，客户端驱动程序 I/O 传输会将请求提交到 USB 驱动程序堆栈提供了到主控制器的数据。 主机控制器然后遵循特定协议 (具体取决于终结点的类型： 大容量、 中断，或同步) 来构建到或从设备传输数据的请求。 客户端驱动程序提取的数据传输的所有详细信息。 只要客户端驱动程序提交格式正确的请求时，USB 驱动程序堆栈处理请求，并将数据传输到设备。

设备在配置期间，USB 驱动程序堆栈创建*USB 管道*（在主机端） 的每个 USB 接口和其活动的备用设置中定义的设备的终结点。 USB 管道是主控制器和终结点之间的通信通道。 对于客户端驱动程序，一个管道是终结点的逻辑抽象。 若要发送的数据传输，该驱动程序必须获取与所传输的目标的终结点相关联的管道句柄。 当驱动程序想中止传输或重置的管道，发生错误情况时，还有所需管道句柄。

管道的所有属性均都来自关联的终结点描述符。 例如，具体取决于终结点的类型，USB 驱动程序堆栈分配对管道的类型。 对于大容量端点，USB 驱动程序堆栈创建大容量管道;同步终结点，同步管道创建后，依次类推。 另一重要属性是主控制器可以将发送到的终结点点在请求中的数据量。 根据该值，客户端驱动程序必须确定传输缓冲区的布局。

Windows Driver Foundation (WDF) 中提供了专用的 I/O 目标对象[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)并[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)，客户端简化许多配置任务驱动程序。 通过使用这些对象，客户端驱动程序可以检索有关的当前配置，如数量的接口的信息，备用内每个接口，并为其终结点设置。 调用这些对象之一*目标管道对象*，执行与终结点相关的任务。 本主题介绍如何通过使用目标管道对象获取管道的信息。

有关 Windows 驱动程序模型 (WDM) 客户端驱动程序，USB 驱动程序堆栈返回的数组[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)结构。 数组中元素的数目取决于所选的配置中的接口的活动备用设置定义的终结点的数目。 每个元素包含有关针对特定终结点创建的管道信息。 有关选择一个配置和获取管道的信息的数组的信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)。

## <a name="what-you-need-to-know"></a>你需要了解的内容


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>系统必备

客户端驱动程序可以枚举管道之前，请确保满足这些要求：

-   客户端驱动程序必须已创建的 framework USB 目标设备对象。

    如果使用 Microsoft Visual Studio Professional 2012 使用提供的 USB 模板，模板代码执行这些任务。 模板代码获取目标设备对象的句柄，并将存储在设备上下文中。

    \* * KMDF 客户端驱动程序: * *

    KMDF 客户端驱动程序必须通过调用获取 WDFUSBDEVICE 句柄[ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法。 详细信息，请参阅"设备源代码"中[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)。

    \* * UMDF 客户端驱动程序: * *

    UMDF 客户端驱动程序必须获取[ **IWDFUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)通过查询框架目标设备对象的指针。 有关详细信息，请参阅"[**IPnpCallbackHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"中[了解 USB 客户端驱动程序代码结构 (UMDF)](understanding-the-umdf-template-code-for-usb.md)。

-   设备必须具有活动的配置。

    如果使用的 USB 模板，该代码将在每个接口中选择的第一个配置和默认值替代设置。 有关如何更改该默认设置的信息，请参阅[如何在 USB 界面中选择一项备用设置](select-a-usb-alternate-setting.md)。

    \* * KMDF 客户端驱动程序: * *

    KMDF 客户端驱动程序必须调用[ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)方法。

    \* * UMDF 客户端驱动程序: * *

    UMDF 客户端驱动程序，该框架选择该配置中的第一个配置和每个接口的默认备用设置。

<a name="instructions"></a>说明
------------

### <a name="getting-usb-pipe-handles---kmdf-client-driver"></a>获取 USB 管道句柄的 KMDF 客户端驱动程序

框架表示每个管道，打开的 USB 驱动程序堆栈，为 USB 目标管道对象。 KMDF 客户端驱动程序可以访问目标管道对象，若要获取有关管道的信息的方法。 若要执行数据传输，客户端驱动程序必须具有 WDFUSBPIPE 管道句柄。 若要获取管道句柄，该驱动程序必须枚举活动配置的接口和备用设置，以及然后枚举中的每个设置定义的终结点。 执行枚举操作，为每次数据传输，可能很昂贵。 因此，一种方法是在设备配置后，获取管道句柄并将其存储在驱动程序定义的设备上下文中。 当驱动程序收到的数据传输请求时，该驱动程序可以从设备上下文中，检索所需的管道句柄并使用它们来发送请求。 如果客户端驱动程序更改设备的配置，例如，选择备用设置，该驱动程序必须还刷新具有新的管道句柄的设备上下文。 否则，驱动程序错误地可以对过时的管道句柄发送传输请求。

**请注意**管道句柄不需要的控制转移。
若要发送控制传输请求，WDF 客户端驱动程序调用**WdfUsbDevicexxxx**公开 framework 设备对象的方法。 这些方法需要 WDFUSBDEVICE 句柄来启动控制传输该目标的默认终结点。 对于此类传输，请求的 I/O 目标是默认终结点，并且由 WDFIOTARGET 控点，它抽象 WDFUSBPIPE 句柄。 在设备级别 WDFUSBDEVICE 句柄是默认终结点的 WDFUSBPIPE 句柄的抽象。

有关将控件传输和 KMDF 方法发送的信息，请参阅[如何发送 USB 控制传输](usb-control-transfer.md)。



1.  扩展您的设备上下文结构来存储管道句柄。

    如果您知道在你的设备中的终结点，通过添加要存储相关联的 USB 管道句柄的 WDFUSBPIPE 成员扩展您的设备上下文结构。 例如，你可以扩展设备上下文结构如下所示：

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

    每个管道可以在调用另一个结构中存储终结点相关的特征*管道上下文*。 类似于设备上下文，管道上下文是数据定义的结构 （由客户端驱动程序） 用于存储有关 pipes 与终结点关联的信息。 设备在配置期间，客户端驱动程序将指针传递给其管道上下文框架。 框架中分配的基础结构的大小的内存块，并存储到该 framework USB 目标管道对象使用的内存位置的指针。 客户端驱动程序可以使用指针来访问和管道上下文的成员中存储的管道信息。

    ```cpp
    typedef struct _PIPE_CONTEXT {  

        ULONG MaxPacketSize;
        ULONG MaxStreamsSupported;
        PUSBD_STREAM_INFORMATION StreamInfo;
    } PIPE_CONTEXT, *PPIPE_CONTEXT;  

    WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(PIPE_CONTEXT, GetPipeContext)  

    ```

    在此示例中，管道上下文存储的最大可以在一次传输发送的字节数。 客户端驱动程序可以使用该值来确定传输缓冲区的大小。 声明还包括[ **WDF\_DECLARE\_上下文\_类型\_WITH\_名称**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-context-type-with-name)宏，生成内联函数，GetPipeContext。 客户端驱动程序可以调用该函数可检索到的存储的管道上下文的内存块的指针。

    有关上下文的详细信息，请参阅[框架对象上下文空间](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-context-space)。

    若要将指针传递到框架中，客户端驱动程序先初始化其管道上下文通过调用[ **WDF\_对象\_特性\_INIT\_上下文\_类型**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-object-attributes-init-context-type). 然后，将指针传递给管道上下文，而调用[ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) （用于选择一种配置） 或[ **WdfUsbInterfaceSelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting) （用于选择一项备用设置）。

3.  设备配置请求完成后，枚举接口，并获取用于配置管道的管道句柄。 你将需要此集的信息：

    -   包含当前设置的接口 WDFUSBINTERFACE 句柄。 可以通过枚举在活动配置中的接口来获取该句柄。 或者，如果提供一个指向[ **WDF\_USB\_设备\_选择\_配置\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_device_select_config_params)中结构[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)，就可以从该句柄**Type.SingleInterface.ConfiguredUsbInterface** （适用于单个接口设备） 的成员或**Type.MultiInterface.Pairs.UsbInterface** （适用于多个接口设备） 的成员。
    -   管道中的当前设置的终结点可供使用的数。 可以通过调用特定接口上获取该数字[ **WdfUsbInterfaceGetNumConfiguredPipes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetnumconfiguredpipes)方法。
    -   所有已配置管道的 WDFUSBPIPE 句柄。 可以通过调用获取的句柄[ **WdfUsbInterfaceGetConfiguredPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)方法。

    获取管道句柄后, 客户端驱动程序可以调用方法来确定类型和方向的管道。 该驱动程序可以获取有关终结点，信息[ **WDF\_USB\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)结构。 该驱动程序可以通过调用获取填充的结构[ **WdfUsbTargetPipeGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)方法。 或者，驱动程序可以提供指向中结构的指针[ **WdfUsbInterfaceGetConfiguredPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)调用。

下面的代码示例枚举通过管道传入的当前设置。 它获取为设备的大容量和中断终结点的管道句柄，并将其存储在驱动程序的设备上下文结构。 它将在关联的管道上下文中存储每个终结点的最大数据包大小。 如果终结点支持流，它会通过调用 OpenStreams 例程打开静态流。 在显示的 OpenStreams 实现[如何打开和关闭 USB 大容量终结点中的静态流](how-to-open-streams-in-a-usb-endpoint.md)。

若要确定特定的大容量终结点是否支持静态流，客户端驱动程序将检查终结点描述符。 该代码是名为 RetrieveStreamInfoFromEndpointDesc 下, 一步的代码块中所示的帮助器例程中实现的。

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

下面的代码示例显示了帮助器例程名为 RetrieveStreamInfoFromEndpointDesc，枚举管道时，调用客户端驱动程序。

在以下代码示例中，客户端驱动程序调用上述帮助器例程 RetrieveStreamInfoFromEndpointDesc，枚举管道时。 例程将检查第一次获得配置描述符和对其检索终结点的描述符进行分析。 如果管道的终结点描述符包含 USB\_SUPERSPEED\_终结点\_配套\_描述符\_类型描述符，驱动程序检索流支持的最大数目终结点。

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

### <a name="getting-pipe-handles---umdf-client-driver"></a>获取管道句柄的 UMDF 客户端驱动程序

UMDF 客户端驱动程序使用 COM 基础结构，并实现 COM 回调类 framework 设备对象与配对的。 类似于 KMDF 驱动程序，UMDF 客户端驱动程序之后，可以仅获取管道的信息配置该设备。 若要获取客户端的管道信息驱动程序必须获取一个指向[ **IWDFUsbTargetPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)框架接口对象包含的活动设置的接口。 通过使用接口指针，该驱动程序可以枚举通过管道传入该设置，以获取**IWDFUsbTargetPipe**接口公开的 framework 目标管道对象的指针。

该驱动程序开始枚举管道之前，该驱动程序必须知道有关设备配置和受支持的端点。 根据该信息，该驱动程序可以将管道对象存储为类成员变量。

下面的代码示例扩展了随 Visual Studio Professional 2012 一起提供的 USB UMDF 模板。 起始代码的说明，请参阅"[**IPnpCallbackHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"中[了解 USB 客户端驱动程序代码结构 (UMDF)](understanding-the-umdf-template-code-for-usb.md).

扩展 CDevice 类声明，如下所示。 此示例代码假定该设备是 OSR FX2 板。 有关其描述符布局的信息，请参阅[USB 设备布局](usb-device-layout.md)。

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

在 CDevice 类定义中，实现一个名为 CreateUsbIoTargets 的帮助器方法。 该驱动程序已获取指向目标设备对象的指针后，将从 IPnpCallbackHardware::OnPrepareHardware 实现调用此方法。

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

在 UMDF，客户端驱动程序使用管道索引以将数据传输请求发送。 管道索引是在设置中打开的终结点的管道时，USB 驱动程序堆栈分配的数字。 若要获取管道索引，请调用[**IWDFUsbTargetPipe::GetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)方法。 该方法填充[ **WINUSB\_管道\_信息**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)结构。 **PipeId**值指示管道索引。

一种方法执行的读取和写入目标管道上的操作是调用[ **IWDFUsbInterface::GetWinUsbHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)若要获取 WinUSB 句柄，然后调用[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb). 例如，驱动程序可以调用[ **WinUsb\_ReadPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)或[ **WinUsb\_WritePipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)函数。 在这些函数调用，该驱动程序必须指定管道索引。 有关详细信息，请参阅[如何访问由使用 WinUSB 函数 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

<a name="remarks"></a>备注
-------

### <a name="pipe-handles-for-wdm-based-client-drivers"></a>WDM 基于客户端驱动程序的管道句柄

选择一种配置后，USB 驱动程序堆栈设置为每个设备的终结点的管道。 USB 驱动程序堆栈返回的数组[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)结构。 数组中元素的数目取决于所选的配置中的接口的活动备用设置定义的终结点的数目。 每个元素包含有关针对特定终结点创建的管道信息。 有关获取管道句柄的详细信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)。

若要生成的 I/O 传输请求，客户端驱动程序必须具有与该终结点相关联的管道的句柄。 客户端驱动程序可以获取从管道句柄**PipeHandle**的成员[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)数组中。

除了管道句柄，客户端驱动程序还需要管道类型。 客户端驱动程序可以通过检查来确定管道类型**PipeType**成员。

根据终结点类型，USB 驱动程序堆栈支持不同类型的管道。 客户端驱动程序可以通过检查来确定管道类型**PipeType**的成员[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)。 不同的管道类型需要不同类型的 USB 请求块 (URBs) 来执行 I/O 事务。

然后，客户端驱动程序将提交到 USB 驱动程序堆栈 URB。 USB 驱动程序堆栈处理请求，并将指定的数据发送到请求的目标管道。

URB 包含有关目标的管道句柄、 传输缓冲区和其长度等请求的信息。 中的每个结构[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)联合共享某些成员：**TransferFlags**， **TransferBuffer**， **TransferBufferLength**，并且**TransferBufferMDL**。 有在特定于类型的标志**TransferFlags**对应于每个 URB 类型的成员。 所有数据将都传输 URBs，USBD\_都传输\_方向\_中的 IN 标志**TransferFlags**指定都传输的方向。 客户端驱动程序设置 USBD\_传输\_方向\_中标志，用于从设备读取数据。 驱动程序，请清除此标志，以将数据发送到设备。 数据可能会读取或写入到驻留在内存中的任一的缓冲区或 MDL。 在任一情况下，该驱动程序指定的缓冲区的大小**TransferBufferLength**成员。 该驱动程序提供了中的常驻缓冲区**TransferBuffer**成员和在 MDL **TransferBufferMDL**成员。 无论哪一个驱动程序提供了另一个必须为 NULL。

## <a name="related-topics"></a>相关主题
[USB I/O 传输](usb-device-i-o.md)  
[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)  
[如何在 USB 界面中选择一项备用设置](select-a-usb-alternate-setting.md)  
[USB 客户端驱动程序的常见任务](wdk-resources-for-usb-driver-development.md)  



