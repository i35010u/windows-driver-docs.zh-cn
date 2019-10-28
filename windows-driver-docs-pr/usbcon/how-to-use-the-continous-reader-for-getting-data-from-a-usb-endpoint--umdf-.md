---
Description: 本主题介绍 WDF 提供的连续读取器对象。 本主题中的过程提供了有关如何配置对象并使用它从 USB 管道读取数据的分步说明。
title: 如何使用连续读取器从 USB 管道读取数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b00563d9357dc9791250f91362eaece03f87748c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837543"
---
# <a name="how-to-use-the-continuous-reader-for-reading-data-from-a-usb-pipe"></a>如何使用连续读取器从 USB 管道读取数据


本主题介绍 WDF 提供的连续读取器对象。 本主题中的过程提供了有关如何配置对象并使用它从 USB 管道读取数据的分步说明。

Windows 驱动程序框架（WDF）提供名为 "*连续读取器*" 的专用对象。 只要有数据可用，此对象就使 USB 客户端驱动程序可以连续地从大容量和中断终结点读取数据。 为了使用读取器，客户端驱动程序必须具有与驱动程序从中读取数据的终结点相关联的 USB 目标管道对象的句柄。 终结点必须处于活动配置。 可以通过以下两种方式之一使配置处于活动状态：选择 USB 配置，或更改当前配置中的替代设置。 有关这些操作的详细信息，请参阅[如何为 Usb 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)以及[如何在 usb 接口中选择替代设置](select-a-usb-alternate-setting.md)。

创建连续读取器后，客户端驱动程序可以在必要时启动和停止读取器。 连续的读取器，可确保目标管道对象上始终有一个读取请求，客户端驱动程序始终可以从终结点接收数据。

持续读取器不会自动由框架进行电源管理。 这意味着，当设备进入工作状态时，客户端驱动程序必须停止读取器，并在设备进入工作状态时重新启动读取器。

## <a name="what-you-need-to-know"></a>你需要了解的内容


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>必备条件

在客户端驱动程序可以使用连续读取器之前，请确保满足以下要求：

-   USB 设备上必须有一个终结点。 检查[USBView](https://docs.microsoft.com/windows-hardware/drivers/debugger/usbview)中的设备配置。 Usbview 是一个应用程序，它允许你浏览所有 USB 控制器和连接到它们的 USB 设备。 通常情况下，USBView 安装在 Windows 驱动程序工具包（WDK）中的 "**调试器**" 文件夹中。
-   客户端驱动程序必须已创建框架 USB 目标设备对象。

    如果使用的是随 Microsoft Visual Studio Professional 2012 一起提供的 USB 模板，则模板代码将执行这些任务。 模板代码获取目标设备对象的句柄，并将其存储在设备上下文中。

    **KMDF 客户端驱动程序：**

    KMDF 客户端驱动程序必须通过调用[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法获取 WDFUSBDEVICE 句柄。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构（KMDF）中的](understanding-the-kmdf-template-code-for-usb.md)"设备源代码"。

    **UMDF 客户端驱动程序：**

    UMDF 客户端驱动程序必须通过查询框架目标设备对象来获取[**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)指针。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构（UMDF）](understanding-the-umdf-template-code-for-usb.md)中的 "[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"。

-   设备必须具有活动配置。

    如果使用的是 USB 模板，则代码将选择每个接口中的第一个配置和默认备用设置。 有关如何更改备用设置的信息，请参阅[如何在 USB 接口中选择替代设置](select-a-usb-alternate-setting.md)。

    **KMDF 客户端驱动程序：**

    KMDF 客户端驱动程序必须调用[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)方法。

    **UMDF 客户端驱动程序：**

    对于 UMDF 客户端驱动程序，框架为该配置中的每个接口选择第一个配置和默认备用设置。

-   客户端驱动程序必须具有 "IN" 终结点的框架目标管道对象的句柄。 有关详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

<a name="instructions"></a>说明
------------

### <a name="using-the-continuous-reader---kmdf-client-driver"></a>使用持续读取器-KMDF 客户端驱动程序

1.  配置连续读取器。

    1.  [ **\_连续\_读取器\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)结构，通过调用[**wdf\_** ](https://msdn.microsoft.com/library/windows/hardware/ff552561_init)\_\_INIT 宏\_\_
    2.  在[**WDF\_USB\_连续\_读取器\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)结构中指定其配置选项。
    3.  调用[**WdfUsbTargetPipeConfigContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)方法。

    下面的示例代码为指定的目标管道对象配置持续读取器。

    ```cpp
    NTSTATUS FX3ConfigureContinuousReader(
        _In_ WDFDEVICE Device,
        _In_ WDFUSBPIPE Pipe)
    {
        NTSTATUS status;

        PDEVICE_CONTEXT                     pDeviceContext;       

        WDF_USB_CONTINUOUS_READER_CONFIG    readerConfig;

        PPIPE_CONTEXT                       pipeContext;  

        PAGED_CODE();

        pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);

        pipeContext = GetPipeContext (Pipe);

        WDF_USB_CONTINUOUS_READER_CONFIG_INIT(  
            &readerConfig,  
            FX3EvtReadComplete,  
            pDeviceContext,  
            pipeContext->MaxPacketSize);  

        readerConfig.EvtUsbTargetPipeReadersFailed=FX3EvtReadFailed;  

        status = WdfUsbTargetPipeConfigContinuousReader(  
            Pipe,  
            &readerConfig);  

        if (!NT_SUCCESS (status))
        {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                "%!FUNC! WdfUsbTargetPipeConfigContinuousReader failed 0x%x", status);

            goto Exit;
        }


    Exit:
        return status;
    }
    ```

通常，客户端驱动程序会在[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数中枚举活动设置中的目标管道对象之后配置连续读取器。

在前面的示例中，客户端驱动程序通过两种方式指定其配置选项。 首先，通过调用[**wdf\_usb\_连续\_读取器\_CONFIG\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_continuous_reader_config_init) ，然后通过设置[**WDF\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)\_ 请注意**WDF\_USB\_连续\_读取器的参数\_CONFIG\_INIT**。 这些值是必需的。 在此示例中，客户端驱动程序指定：

-   指向驱动程序实现的完成例程的指针。 框架在完成读取请求时调用此例程。 在完成例程中，驱动程序可以访问包含读取的数据的内存位置。 完成例程的实现将在步骤2中讨论。
-   指向驱动程序定义的上下文的指针。
-   单个传输中可以从设备中读取的字节数。 客户端驱动程序可以通过调用[**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)或[**WdfUsbTargetPipeGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)方法，在[**WDF\_USB\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)结构中获取该信息。 有关详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

[**WDF\_USB\_连续\_读取器\_CONFIG\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_continuous_reader_config_init)将连续读取器配置为使用*NumPendingReads*的默认值。 该值确定框架添加到挂起队列的读取请求数。 已确定默认值，可为许多处理器配置的多个设备提供合理的性能。

除了在 Wdf 中指定的配置参数[ **\_USB\_连续\_读取器\_CONFIG\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_continuous_reader_config_init)，此示例还在 WDF 中设置故障例程[ **\_\_连续\_读取器\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)。 此失败例程是可选的。

除了失败例程以外，WDF 中还有其他成员[ **\_USB\_连续\_读取器\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config) ，客户端驱动程序可以使用该配置器指定传输缓冲区的布局。 例如，假设有一个使用连续读取器来接收网络数据包的网络驱动程序。 每个数据包都包含标头、负载和页脚数据。 若要描述数据包，驱动程序必须先指定数据包的调用[ **\_USB\_连续\_读取器\_CONFIG\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552561_init)中的数据包大小。 然后，驱动程序必须通过设置 WDF 的**HeaderLength**和**TrailerLength**成员来指定页眉和页脚的长度 **\_USB\_连续\_读取器\_CONFIG**。 框架使用这些值来计算有效负载两侧的字节偏移量。 从终结点读取负载数据时，框架会将该数据存储在偏移量之间的缓冲区部分。

2.  实现完成例程。

    每次完成请求时，框架都会调用客户端驱动程序实现的完成例程。 该框架将传递所读取的字节数，以及一个 WDFMEMORY 对象，其缓冲区包含从管道读取的数据。

    下面的示例代码演示了完成例程实现。

    ```cpp
    EVT_WDF_USB_READER_COMPLETION_ROUTINE FX3EvtReadComplete;

    VOID FX3EvtReadComplete(
        __in  WDFUSBPIPE Pipe,
        __in  WDFMEMORY Buffer,
        __in  size_t NumBytesTransferred,
        __in  WDFCONTEXT Context
        )
    {

        PDEVICE_CONTEXT  pDeviceContext;  
        PVOID  requestBuffer;    

        pDeviceContext = (PDEVICE_CONTEXT)Context;

        if (NumBytesTransferred == 0)
        {
            return;
        }

        requestBuffer = WdfMemoryGetBuffer(Buffer, NULL);

        if (Pipe == pDeviceContext->InterruptPipe)
        {
            KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL,
                                    "Interrupt endpoint: %s.\n", 
                                    requestBuffer )); 
        }


        return;
    }

    ```

每次完成请求时，框架都会调用客户端驱动程序实现的完成例程。 框架为每个读取操作分配一个内存对象。 在完成例程中，框架将读取的字节数和 WDFMEMORY 句柄传递到内存对象。 内存对象缓冲区包含从管道读取的数据。 客户端驱动程序不能释放内存对象。 框架在每个完成例程返回后释放对象。 如果客户端驱动程序要存储接收的数据，则驱动程序必须在完成例程中复制缓冲区的内容。

3.  实现失败例程。

    框架调用客户端驱动程序实现的失败例程，以通知驱动程序在处理读取请求时持续读取器报告了一个错误。 框架将指针传递到请求失败的目标管道对象和错误代码值。 根据这些错误代码值，驱动程序可以实现其错误恢复机制。 驱动程序还必须返回相应的值，指示框架是否应重新启动持续读取器。

    下面的示例代码演示了一个失败例程实现。

    ```cpp
    EVT_WDF_USB_READERS_FAILED FX3EvtReadFailed;  

    BOOLEAN  
    FX3EvtReadFailed(  
        WDFUSBPIPE      Pipe,  
        NTSTATUS        Status,  
        USBD_STATUS     UsbdStatus  
        )  
    {      
        UNREFERENCED_PARAMETER(Status);  

        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                "%!FUNC! ReadersFailedCallback failed NTSTATUS 0x%x, UsbdStatus 0x%x\n", 
                     status,
                     UsbdStatus);

        return TRUE;  
    }  
    ```

在前面的示例中，驱动程序返回 TRUE。 此值向框架指示它必须重置管道，然后重新启动持续读取器。

或者，如果管道上出现卡住的情况，则客户端驱动程序可能返回 FALSE 并提供错误恢复机制。 例如，驱动程序可以检查 USBD 状态，并发出重置管道请求以清除延迟情况。

有关管道中的错误恢复的信息，请参阅[如何从 USB 管道恢复错误](how-to-recover-from-usb-pipe-errors.md)。

4.  指示框架在设备进入工作状态时启动连续读取器;当设备离开工作状态时停止读取器。 调用这些方法，并将目标管道对象指定为 i/o 目标对象。

    -   [**WdfIoTargetStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)
    -   [**WdfIoTargetStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)

    持续读取器不会自动由框架进行电源管理。 因此，当设备的电源状态更改时，客户端驱动程序必须显式启动或停止目标管道对象。 驱动程序会在驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)实现中调用[**WdfIoTargetStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart) 。 此调用可确保队列仅在设备处于工作状态时才传递请求。 相反，驱动程序会在驱动程序[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)实现中调用[**WdfIoTargetStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) ，以便在设备进入低功率状态时队列停止传递请求。

下面的示例代码为指定的目标管道对象配置持续读取器。

```cpp

EVT_WDF_DEVICE_D0_ENTRY FX3EvtDeviceD0Entry;

NTSTATUS FX3EvtDeviceD0Entry(
    __in  WDFDEVICE Device,
    __in  WDF_POWER_DEVICE_STATE PreviousState
    )
{
    PDEVICE_CONTEXT  pDeviceContext;

    NTSTATUS status;

    PAGED_CODE();

    pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);


    status = WdfIoTargetStart (WdfUsbTargetPipeGetIoTarget (pDeviceContext->InterruptPipe));

    if (!NT_SUCCESS (status))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not start interrupt pipe failed 0x%x", status);
    }

}

EVT_WDF_DEVICE_D0_EXIT FX3EvtDeviceD0Exit;

NTSTATUS FX3EvtDeviceD0Exit(
    __in  WDFDEVICE Device,
    __in  WDF_POWER_DEVICE_STATE TargetState
    )
{
    PDEVICE_CONTEXT  pDeviceContext;      

    NTSTATUS status;

    PAGED_CODE();

    pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);


    WdfIoTargetStop (WdfUsbTargetPipeGetIoTarget (pDeviceContext->InterruptPipe), WdfIoTargetCancelSentIo));

}
```

前面的示例演示[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)和[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调例程的实现。 [**WdfIoTargetStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)的 action 参数允许客户端驱动程序在设备离开工作状态时决定队列中挂起的请求的操作。 在此示例中，驱动程序指定了**WdfIoTargetCancelSentIo**。 该选项指示框架取消队列中所有挂起的请求。 或者，驱动程序可以指示框架在停止 i/o 目标之前等待挂起的请求完成，或在 i/o 目标重新启动时保留挂起的请求并继续。

### <a name="using-the-continuous-reader---umdf-client-driver"></a>使用持续读取器-UMDF 客户端驱动程序

开始使用连续读取器之前，必须在[**IPnpCallbackHardware：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)方法的实现中配置读取器。 获取指向与中的终结点关联的目标管道对象的[**IWDFUsbTargetPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)接口的指针后，请执行以下步骤：

**配置连续读取器**

1.  在目标管道对象（[**IWDFUsbTargetPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)）上调用**QueryInterface** ，并查询[**IWDFUsbTargetPipe2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)接口。
2.  在设备回调对象上调用**QueryInterface** ，并查询[**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)接口。 若要使用连续读取器，必须实现 IUsbTargetPipeContinuousReaderCallbackReadComplete。 本主题后面将介绍实现。
3.  如果实现了失败回调，请对设备回调对象调用**QueryInterface**并查询[IUsbTargetPipeContinuousReaderCallbackReadersFailed](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)接口。 本主题后面将介绍实现。
4.  调用[**IWDFUsbTargetPipe2：： ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)方法并指定配置参数，如标头、尾部、挂起的请求数，以及对完成和失败回调方法的引用。

    方法为目标管道对象配置连续读取器。 连续读取器会创建队列，用于管理从目标管道对象发送和接收的一组读取请求。

下面的示例代码为指定的目标管道对象配置持续读取器。 该示例假设调用方指定的目标管道对象与一个 IN 终结点相关联。 连续读取器配置为读取 USBD\_默认\_最大\_传输\_大小字节数;若要使用框架使用的默认挂起请求数，则为;调用客户端驱动程序提供的完成和失败回调方法。 接收的缓冲区将不包含任何标头或尾部数据。

```cpp
HRESULT CDeviceCallback::ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe)
{
    if (!pFxPipe)
    {
        return E_INVALIDARG;
    }

    IUsbTargetPipeContinuousReaderCallbackReadComplete *pOnCompletionCallback = NULL;
    IUsbTargetPipeContinuousReaderCallbackReadersFailed *pOnFailureCallback = NULL;
    IWDFUsbTargetPipe2* pFxUsbPipe2 = NULL;

    HRESULT hr = S_OK;

    // Set up the continuous reader to read from the target pipe object.

    //Get a pointer to the target pipe2 object.
    hr = pFxPipe->QueryInterface(IID_PPV_ARGS(&pFxUsbPipe2));
    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

    //Get a pointer to the completion callback.
    hr = QueryInterface(IID_PPV_ARGS(&pOnCompletionCallback));
    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

    //Get a pointer to the failure callback.
    hr = QueryInterface(IID_PPV_ARGS(&pOnFailureCallback));
    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

    //Get a pointer to the target pipe2 object.
    hr = pFxUsbPipe2->ConfigureContinuousReader (    
        USBD_DEFAULT_MAXIMUM_TRANSFER_SIZE, //size of data to be read
        0, //Header
        0, //Trailer
        0, // Number of pending requests queued by WDF
        NULL, // Cleanup callback. Not provided.
        pOnCompletionCallback, //Completion routine.
        NULL, //Completion routine context. Not provided.
        pOnFailureCallback); //Failure routine. Not provided

    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

ConfigureContinuousReaderExit:

    if (pOnFailureCallback)
    {
        pOnFailureCallback->Release();
        pOnFailureCallback = NULL;
    }

    if (pOnCompletionCallback)
    {
        pOnCompletionCallback->Release();
        pOnCompletionCallback = NULL;
    }

    if (pFxUsbPipe2)
    {
        pFxUsbPipe2->Release();
        pFxUsbPipe2 = NULL;
    }

    return hr;
}
```

接下来，在设备进入并退出工作状态（**D0**）时，指定目标管道对象的状态。

如果客户端驱动程序使用电源管理的队列将请求发送到管道，则只有在设备处于**D0**状态时，队列才会传递请求。 如果设备的电源状态从**d0**更改为较低的电源状态（在**D0**出口上），则目标管道对象完成挂起的请求，并且队列停止向目标管道对象提交请求。 因此，不需要客户端驱动程序启动和停止目标管道对象。

连续读取器不使用电源管理的队列提交请求。 因此，当设备的电源状态更改时，必须显式启动或停止目标管道对象。 若要更改目标管道对象的状态，可以使用由该框架实现的[**IWDFIoTargetStateManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)接口。 获取指向与中的终结点关联的目标管道对象的[**IWDFUsbTargetPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)接口的指针后，请执行以下步骤：

**实现状态管理**

1.  在[**IPnpCallbackHardware：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)的实现中，对目标管道对象（[**IWDFUsbTargetPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)）调用 [**QueryInterface** ，并查询[**IWDFIoTargetStateManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)接口。 将引用存储在设备回调类的成员变量中。
2.  实现设备回调对象上的[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)接口。
3.  在[**IPnpCallback：： OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)方法的实现中，调用[**IWDFIoTargetStateManagement：： start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)以启动连续读取器。
4.  在[**IPnpCallback：： OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)方法的实现中，调用[**IWDFIoTargetStateManagement：： stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)以停止连续读取器。

设备进入工作状态（**D0**）后，框架将调用客户端驱动程序提供的 D0 输入回调方法，该方法可启动目标管道对象。 当设备离开**d0**状态时，框架将调用 d0 退出回调方法。 目标管道对象完成由客户端驱动程序配置的挂起的读取请求数，并停止接受新请求。
下面的示例代码实现了设备回调对象上的[IPnpCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)接口。

```cpp
class CDeviceCallback : 
    public IPnpCallbackHardware, 
    public IPnpCallback,
{
public:
    CDeviceCallback();
    ~CDeviceCallback();
    virtual HRESULT STDMETHODCALLTYPE QueryInterface(REFIID riid, VOID** ppvObject);
    virtual ULONG STDMETHODCALLTYPE AddRef();
    virtual ULONG STDMETHODCALLTYPE Release();

    virtual HRESULT STDMETHODCALLTYPE OnPrepareHardware(IWDFDevice* pDevice);
    virtual HRESULT STDMETHODCALLTYPE OnReleaseHardware(IWDFDevice* pDevice); 

    virtual HRESULT STDMETHODCALLTYPE OnD0Entry(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual HRESULT STDMETHODCALLTYPE OnD0Exit(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual void STDMETHODCALLTYPE OnSurpriseRemoval(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryRemove(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryStop(IWDFDevice*  pWdfDevice);    

private:
    LONG m_cRefs;
    IWDFUsbTargetPipe* m_pFxUsbPipe;
    IWDFIoTargetStateManagement* m_pFxIoTargetInterruptPipeStateMgmt;

    HRESULT CreateUSBTargetDeviceObject (IWDFDevice* pFxDevice, IWDFUsbTargetDevice** ppUSBTargetDevice);
    HRESULT ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe);
};
```

下面的示例代码演示如何获取指向 IPnpCallback：： OnPrepareHardware 方法中目标 pipe 对象的 IWDFIoTargetStateManagement 接口的指针

```cpp
   //Enumerate the endpoints and get the interrupt pipe.

    for (UCHAR index = 0; index < NumEndpoints; index++)
    {
        hr = pFxInterface->RetrieveUsbPipeObject(index, &pFxPipe);

        if (SUCCEEDED (hr) && pFxPipe)
        {
            if ((pFxPipe->IsInEndPoint()) && (pFxPipe->GetType()==UsbdPipeTypeInterrupt))
            {
                //Pipe is for an interrupt IN endpoint.

                hr = pFxPipe->QueryInterface(IID_PPV_ARGS(&m_pFxIoTargetInterruptPipeStateMgmt));

                if (m_pFxIoTargetInterruptPipeStateMgmt)
                {               
                    m_pFxUsbPipe = pFxPipe;

                    break;
                }

            }
            else
            {
                //Pipe is NOT for an interrupt IN endpoint.

                pFxPipe->Release();
                pFxPipe = NULL;
            }
        }
        else
        {
             //Pipe not found.
        }
    }
```

下面的示例代码演示如何获取指向[**IPnpCallbackHardware：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)方法中目标 pipe 对象的[**IWDFIoTargetStateManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)接口的指针。

```cpp
 HRESULT CDeviceCallback::OnD0Entry(
    IWDFDevice*  pWdfDevice,
    WDF_POWER_DEVICE_STATE  previousState
    )
{

    if (!m_pFxIoTargetInterruptPipeStateMgmt)
    {
        return E_FAIL;
    }

    HRESULT hr = m_pFxIoTargetInterruptPipeStateMgmt->Start();

    if (FAILED (hr))
    {
        goto OnD0EntryExit;
    }

OnD0EntryExit:
    return hr;
}

HRESULT CDeviceCallback::OnD0Exit(
    IWDFDevice*  pWdfDevice,
    WDF_POWER_DEVICE_STATE  previousState
    )
{
    if (!m_pFxIoTargetInterruptPipeStateMgmt)
    {
        return E_FAIL;
    }

    // Stop the I/O target always succeeds.

    (void)m_pFxIoTargetInterruptPipeStateMgmt->Stop(WdfIoTargetCancelSentIo);

    return S_OK;
}
```

连续读取器完成读取请求后，客户端驱动程序必须提供一种方法，以便在请求成功完成读取请求时获得通知。 客户端驱动程序必须将此代码添加到设备回叫对象。

**通过实现 IUsbTargetPipeContinuousReaderCallbackReadComplete 提供完成回调**

1.  实现设备回调对象上的[**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)接口。
2.  请确保设备回调对象的**QueryInterface**实现递增回调对象的引用计数，然后返回[**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)接口指针。
3.  在[**IUsbTargetPipeContinuousReaderCallbackReadComplete：： OnReaderCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion)方法的实现中，访问从管道读取的数据读取。 *PMemory*参数指向包含数据的框架所分配的内存。 可以调用[**IWDFMemory：： GetDataBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetdatabuffer)以获取包含数据的缓冲区。 缓冲区包含标头，但**OnReaderCompletion**的*NumBytesTransferred*参数指示的数据长度不包括标头长度。 标头长度由客户端驱动程序指定，同时在驱动程序对[**IWDFUsbTargetPipe2：： ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)的调用中配置连续读取器。
4.  在[**IWDFUsbTargetPipe2：： ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)方法的*pOnCompletion*参数中提供一个指向完成回调的指针。

每次数据在设备上的终结点上可用时，目标管道对象将完成读取请求。 如果读取请求成功完成，则框架将调用[**IUsbTargetPipeContinuousReaderCallbackReadComplete：： OnReaderCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion)，通知客户端驱动程序。 否则，当目标管道对象报告读取请求上的错误时，框架会调用客户端驱动程序提供的错误回调。

下面的示例代码实现了设备回调对象上的[**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)接口。

```cpp
class CDeviceCallback : 
    public IPnpCallbackHardware, 
    public IPnpCallback,   
    public IUsbTargetPipeContinuousReaderCallbackReadComplete

{
public:
    CDeviceCallback();
    ~CDeviceCallback();
    virtual HRESULT STDMETHODCALLTYPE QueryInterface(REFIID riid, VOID** ppvObject);
    virtual ULONG STDMETHODCALLTYPE AddRef();
    virtual ULONG STDMETHODCALLTYPE Release();

    virtual HRESULT STDMETHODCALLTYPE OnPrepareHardware(IWDFDevice* pDevice);
    virtual HRESULT STDMETHODCALLTYPE OnReleaseHardware(IWDFDevice* pDevice); 

    virtual HRESULT STDMETHODCALLTYPE OnD0Entry(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual HRESULT STDMETHODCALLTYPE OnD0Exit(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual void STDMETHODCALLTYPE OnSurpriseRemoval(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryRemove(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryStop(IWDFDevice*  pWdfDevice);    

    virtual VOID STDMETHODCALLTYPE OnReaderCompletion(IWDFUsbTargetPipe* pPipe, IWDFMemory* pMemory, SIZE_T NumBytesTransferred, PVOID Context);    


private:
    LONG m_cRefs;
    IWDFUsbTargetPipe* m_pFxUsbPipe;
    IWDFIoTargetStateManagement* m_pFxIoTargetInterruptPipeStateMgmt;

    HRESULT CreateUSBTargetDeviceObject (IWDFDevice* pFxDevice, IWDFUsbTargetDevice** ppUSBTargetDevice);
    HRESULT ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe);
};
```

下面的示例代码演示设备回调对象的 QueryInterface 实现。

```cpp
HRESULT CDeviceCallback::QueryInterface(REFIID riid, LPVOID* ppvObject)
{
    if (ppvObject == NULL)
    {
        return E_INVALIDARG;
    }

    *ppvObject = NULL;

    HRESULT hr = E_NOINTERFACE;

    if(  IsEqualIID(riid, __uuidof(IPnpCallbackHardware))   ||  IsEqualIID(riid, __uuidof(IUnknown))  )
    {  
        *ppvObject = static_cast<IPnpCallbackHardware*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IPnpCallback)))
    {  
        *ppvObject = static_cast<IPnpCallback*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IUsbTargetPipeContinuousReaderCallbackReadComplete)))
    {  
        *ppvObject = static_cast<IUsbTargetPipeContinuousReaderCallbackReadComplete*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    return hr;
}
```

下面的示例代码演示如何从[**IUsbTargetPipeContinuousReaderCallbackReadComplete：： OnReaderCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion)返回的缓冲区中获取数据。 当目标管道对象每次成功完成读取请求时，框架将调用**OnReaderCompletion**。 该示例获取 containsng 数据并在调试器输出上打印内容的缓冲区。

```cpp
 VOID CDeviceCallback::OnReaderCompletion(
    IWDFUsbTargetPipe* pPipe,
    IWDFMemory* pMemory,
    SIZE_T NumBytesTransferred,
    PVOID Context)
{        
    if (pPipe != m_pFxUsbInterruptPipe)
    {
        return;
    }

    if (NumBytesTransferred == 0) 
    {
        // NumBytesTransferred is zero.

        return;
    }

    PVOID pBuff = NULL;
    LONG CurrentData = 0;
    char data[20];

    pBuff = pMemory->GetDataBuffer(NULL);

    if (pBuff)
    {
        CopyMemory(&CurrentData, pBuff, sizeof(CurrentData));
        sprintf_s(data, 20, "%d\n", CurrentData);
        OutputDebugString(data);
        pBuff = NULL;
    }
    else
    {
        OutputDebugString(TEXT("Unable to get data buffer."));
    }
}
```

当完成读取请求时，如果目标管道对象出现故障，则客户端驱动程序可以从框架获取通知。 若要获取通知，客户端驱动程序必须实现失败回调，并在配置持续读取器时提供指向回调的指针。 下面的过程介绍如何实现失败回调。

**通过实现 IUsbTargetPipeContinuousReaderCallbackReadersFailed 提供失败回调**

1.  实现设备回调对象上的[**IUsbTargetPipeContinuousReaderCallbackReadersFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)接口。
2.  请确保设备回调对象的**QueryInterface**实现递增回调对象的引用计数，然后返回[**IUsbTargetPipeContinuousReaderCallbackReadersFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)接口指针。
3.  在[**IUsbTargetPipeContinuousReaderCallbackReadersFailed：： OnReaderFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)方法的实现中，提供失败读取请求的错误处理。

    如果连续读取器无法完成读取请求，且客户端驱动程序提供了失败回调，则框架将调用[**IUsbTargetPipeContinuousReaderCallbackReadersFailed：： OnReaderFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)方法。 此框架在*hrStatus*参数中提供一个 HRESULT 值，用于指示目标管道对象中发生的错误代码。 根据该错误代码，您可能会提供特定的错误处理。 例如，如果想要框架重置管道，然后重启连续读取器，请确保回调返回 TRUE。

    **注意** 不要在失败回调中调用[**IWDFIoTargetStateManagement：： Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)和[**IWDFIoTargetStateManagement：： Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop) 。



4.  提供一个指针，指向[**IWDFUsbTargetPipe2：： ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)方法的*pOnFailure*参数中的失败回调。

下面的示例代码实现了设备回调对象上的[**IUsbTargetPipeContinuousReaderCallbackReadersFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)接口。

```cpp
class CDeviceCallback : 
    public IPnpCallbackHardware, 
    public IPnpCallback,
    public IUsbTargetPipeContinuousReaderCallbackReadComplete,
    public IUsbTargetPipeContinuousReaderCallbackReadersFailed
{
public:
    CDeviceCallback();
    ~CDeviceCallback();
    virtual HRESULT STDMETHODCALLTYPE QueryInterface(REFIID riid, VOID** ppvObject);
    virtual ULONG STDMETHODCALLTYPE AddRef();
    virtual ULONG STDMETHODCALLTYPE Release();

    virtual HRESULT STDMETHODCALLTYPE OnPrepareHardware(IWDFDevice* pDevice);
    virtual HRESULT STDMETHODCALLTYPE OnReleaseHardware(IWDFDevice* pDevice); 

    virtual HRESULT STDMETHODCALLTYPE OnD0Entry(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual HRESULT STDMETHODCALLTYPE OnD0Exit(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual void STDMETHODCALLTYPE OnSurpriseRemoval(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryRemove(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryStop(IWDFDevice*  pWdfDevice);    

    virtual VOID STDMETHODCALLTYPE OnReaderCompletion(IWDFUsbTargetPipe* pPipe, IWDFMemory* pMemory, SIZE_T NumBytesTransferred, PVOID Context);    
    virtual BOOL STDMETHODCALLTYPE OnReaderFailure(IWDFUsbTargetPipe * pPipe, HRESULT hrCompletion);

private:
    LONG m_cRefs;
    IWDFUsbTargetPipe* m_pFxUsbInterruptPipe;
    IWDFIoTargetStateManagement* m_pFxIoTargetInterruptPipeStateMgmt;

    HRESULT CreateUSBTargetDeviceObject (IWDFDevice* pFxDevice, IWDFUsbTargetDevice** ppUSBTargetDevice);
    HRESULT RetrieveUSBDeviceDescriptor (IWDFUsbTargetDevice* pUSBTargetDevice, PUSB_DEVICE_DESCRIPTOR DescriptorHeader, PULONG cbDescriptor);
    HRESULT ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe);
};
```

下面的示例代码演示设备回调对象的 QueryInterface 实现。

```cpp
HRESULT CDeviceCallback::QueryInterface(REFIID riid, LPVOID* ppvObject)
{
    if (ppvObject == NULL)
    {
        return E_INVALIDARG;
    }

    *ppvObject = NULL;

    HRESULT hr = E_NOINTERFACE;

    if(  IsEqualIID(riid, __uuidof(IPnpCallbackHardware))   ||  IsEqualIID(riid, __uuidof(IUnknown))  )
    {  
        *ppvObject = static_cast<IPnpCallbackHardware*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IPnpCallback)))
    {  
        *ppvObject = static_cast<IPnpCallback*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IUsbTargetPipeContinuousReaderCallbackReadComplete)))
    {  
        *ppvObject = static_cast<IUsbTargetPipeContinuousReaderCallbackReadComplete*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;
    }

    if(  IsEqualIID(riid, __uuidof(IUsbTargetPipeContinuousReaderCallbackReadersFailed)))
    {  
        *ppvObject = static_cast<IUsbTargetPipeContinuousReaderCallbackReadersFailed*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;
    }

    return hr;
}
```

下面的示例代码演示了失败回调的实现。 如果读取请求失败，则该方法将打印调试器中的框架报告的错误代码，并指示框架重置管道，然后重新启动持续读取器。

```cpp
 BOOL CDeviceCallback::OnReaderFailure(
    IWDFUsbTargetPipe * pPipe,
    HRESULT hrCompletion
    )
{
    UNREFERENCED_PARAMETER(pPipe);  
    UNREFERENCED_PARAMETER(hrCompletion);     

    return TRUE;
}
```

如果客户端驱动程序未提供故障回调并发生错误，则该框架将重置 USB 管道并重新启动持续读取器。

## <a name="related-topics"></a>相关主题
[USB i/o 传输](usb-device-i-o.md)  
[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)  
[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)  
[如何在 USB 接口中选择备用设置](select-a-usb-alternate-setting.md)  
[USB 客户端驱动程序的常见任务](wdk-resources-for-usb-driver-development.md)  



