---
Description: This topic describes the WDF-provided continuous reader object. The procedures in this topic provide step-by-step instructions about how to configure the object and use it to read data from a USB pipe.
title: 如何使用连续读取器从 USB 管道读取数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1189bc0a691e605083181a55538c1d76a2970d6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576225"
---
# <a name="how-to-use-the-continuous-reader-for-reading-data-from-a-usb-pipe"></a>如何使用连续读取器从 USB 管道读取数据


本主题介绍 WDF 提供持续的读取器对象。 本主题中的过程提供有关如何配置对象并使用它从 USB 管道读取数据的分步说明。

Windows 驱动程序框架 (WDF) 提供了一个专用的对象，调用*连续读取器*。 此对象使 USB 客户端驱动程序，连续从大容量和中断终结点读取数据，只要没有可用的数据。 若要使用读取器，客户端驱动程序必须具有与该驱动程序从中读取数据的终结点相关联的 USB 目标管道对象的句柄。 终结点必须在活动配置中。 您可以使配置处于活动状态中有两种： 通过选择 USB 配置或更改当前配置中的备用设置。 有关这些操作的详细信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)并[如何在 USB 界面中选择一项备用设置](select-a-usb-alternate-setting.md)。

在创建后持续读取器，客户端驱动程序可以启动和停止读取器，以及在必要时。 始终确保读取的请求始终可在目标管道对象和客户端驱动程序上的连续读取器已准备好从终结点接收数据。

持续读取器不会自动电源管理框架。 这意味着客户端驱动程序必须停止读取器，当设备进入低功率状态并重新启动读取器，当设备进入工作状态。

## <a name="what-you-need-to-know"></a>你需要了解的内容


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>先决条件

客户端驱动程序可以使用连续读取器之前，请确保满足这些要求：

-   USB 设备必须在终结点。 签入的设备配置[USBView](https://msdn.microsoft.com/library/ff560019(VS.85).aspx)。 Usbview.exe 是允许您浏览所有 USB 控制器和连接到它们的 USB 设备的应用程序。 通常，在安装 USBView**调试器**文件夹 Windows Driver Kit (WDK) 中。
-   客户端驱动程序必须已创建的 framework USB 目标设备对象。

    如果使用 Microsoft Visual Studio Professional 2012 使用提供的 USB 模板，模板代码执行这些任务。 模板代码获取目标设备对象的句柄，并将存储在设备上下文中。

    **KMDF 客户端驱动程序：**

    KMDF 客户端驱动程序必须通过调用获取 WDFUSBDEVICE 句柄[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)方法。 详细信息，请参阅"设备源代码"中[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)。

    **UMDF 客户端驱动程序：**

    UMDF 客户端驱动程序必须获取[ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)通过查询框架目标设备对象的指针。 有关详细信息，请参阅"[**IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)实现和特定于 USB 的任务"中[了解 USB 客户端驱动程序代码结构 (UMDF)](understanding-the-umdf-template-code-for-usb.md)。

-   设备必须具有活动的配置。

    如果使用的 USB 模板，该代码将在每个接口中选择的第一个配置和默认值替代设置。 有关如何更改替代设置的信息，请参阅[如何在 USB 界面中选择一项备用设置](select-a-usb-alternate-setting.md)。

    **KMDF 客户端驱动程序：**

    KMDF 客户端驱动程序必须调用[ **WdfUsbTargetDeviceSelectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff550101)方法。

    **UMDF 客户端驱动程序：**

    UMDF 客户端驱动程序，该框架选择该配置中的第一个配置和每个接口的默认备用设置。

-   客户端驱动程序必须在终结点的 framework 目标管道对象的句柄。 有关详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

<a name="instructions"></a>说明
------------

### <a name="using-the-continuous-reader---kmdf-client-driver"></a>使用连续的读取器-KMDF 客户端驱动程序

1.  配置持续读取器。

    1.  初始化[ **WDF\_USB\_CONTINUOUS\_读取器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552561)结构通过调用[ **WDF\_USB\_连续\_读取器\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552561_init)宏。
    2.  指定在其配置选项[ **WDF\_USB\_CONTINUOUS\_读取器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552561)结构。
    3.  调用[ **WdfUsbTargetPipeConfigContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff551130)方法。

    下面的示例代码配置指定的目标的管道对象的持续读取器。

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

客户端驱动程序配置中的连续读取器通常[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数中之后，枚举活动设置中的目标的管道对象。

在前面的示例中，客户端驱动程序指定以下两种方式及其配置选项。 通过调用第一个[ **WDF\_USB\_CONTINUOUS\_读取器\_配置\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552566) ，然后通过设置[ **WDF\_USB\_连续\_读取器\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552561)成员。 请注意，为参数**WDF\_USB\_连续\_读取器\_CONFIG\_INIT**。 这些值是必需的。 在此示例中，客户端驱动程序指定：

-   指向该驱动程序实现完成例程的指针。 在完成读取的请求时，框架将调用此例程。 在完成例程，该驱动程序可以访问包含已读取的数据的内存位置。 完成例程的实现是在步骤 2 中所述。
-   指向驱动程序定义的上下文的指针。
-   可以从单个传输中的设备读取的字节数。 客户端驱动程序可以获取该信息[ **WDF\_USB\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff553037)结构通过调用[ **WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)或[ **WdfUsbTargetPipeGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff551142)方法。 有关详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

[**WDF\_USB\_连续\_读取器\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552566)配置持续读取器中，若要使用的默认值为*NumPendingReads*. 此值确定框架将添加到挂起队列的读取请求的数。 已确定的默认值在多处理器配置提供很多设备的合理的良好性能。

除了中指定的配置参数[ **WDF\_USB\_CONTINUOUS\_读取器\_配置\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552566)、示例还将设置失败例程[ **WDF\_USB\_CONTINUOUS\_读取器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552561)。 此失败例程是可选的。

除了失败例程，还有中的其他成员[ **WDF\_USB\_CONTINUOUS\_读取器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552561)的客户端驱动程序可以使用指定的传输缓冲区布局。 例如，考虑使用持续读取器接收网络数据包的网络驱动程序。 每个数据包中包含标头、 有效负载和表尾数据。 若要描述该数据包，该驱动程序必须首先指定数据包大小中对其调用[ **WDF\_USB\_CONTINUOUS\_读取器\_配置\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552561_init). 然后，该驱动程序必须通过设置指定页眉和页脚的长度**HeaderLength**并**TrailerLength**的成员**WDF\_USB\_连续\_读取器\_CONFIG**。 该框架使用这些值来计算字节偏移量有效负载的任意一侧。 有效负载数据读取时从终结点，框架会将这些数据存储在缓冲区之间的偏移量的一部分。

2.  实现完成例程。

    框架调用客户端驱动程序实现完成例程每次完成一个请求。 框架将传递读取字节并其缓冲区包含从管道读取数据的 WDFMEMORY 对象的数。

    下面的代码示例显示了完成例程实现。

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

框架调用客户端驱动程序实现完成例程每次完成一个请求。 该框架为每次读取操作分配的内存对象。 在完成例程中，框架将读取字节并 WDFMEMORY 句柄数传递到内存对象。 内存对象缓冲区包含从管道读取的数据。 客户端驱动程序必须释放该内存对象。 每个完成例程返回后，框架将释放对象。 如果客户端驱动程序想要存储所接收的数据，该驱动程序必须将缓冲区的内容复制完成例程中。

3.  实现失败例程。

    框架调用以通知持续读取器处理读取的请求时报告了错误的驱动程序的客户端驱动程序实现失败例程。 此框架传递到目标管道指针对象上的请求失败，这和错误代码值。 这些错误代码值为基础的驱动程序可以实现其错误恢复机制。 该驱动程序还必须返回适当的值，该值指示 framework 框架是否应重新启动持续读取器。

    下面的代码示例显示了失败例程实现。

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

在前面的示例中，该驱动程序返回 TRUE。 此值指示框架，它必须重置管道，然后重新启动持续读取器。

或者，客户端驱动程序可以返回 FALSE，并提供错误恢复机制，如果在管道上出现停滞情况。 例如，驱动程序可以检查 USBD 状态并发出重置管道请求以清除停滞条件。

有关在管道中的错误恢复的信息，请参阅[如何从 USB 管道错误中恢复](how-to-recover-from-usb-pipe-errors.md)。

4.  指示框架将在设备进入工作状态，则时启动持续读取器当设备离开工作状态时，请停止读取器。 调用这些方法并为 I/O 目标对象指定目标管道对象。

    -   [**WdfIoTargetStart**](https://msdn.microsoft.com/library/windows/hardware/ff548677)
    -   [**WdfIoTargetStop**](https://msdn.microsoft.com/library/windows/hardware/ff548680)

    持续读取器不会自动电源管理框架。 因此，客户端驱动程序必须显式启动或停止目标管道对象，该设备的电源状态更改时。 驱动程序调用[ **WdfIoTargetStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548677)中的驱动程序[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)实现。 此调用可确保队列提供的请求，仅当设备处于工作状态。 相反，该驱动程序调用[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)驱动程序中[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)实现，以便停止队列当设备进入低功率状态时，请提供请求。

下面的示例代码配置指定的目标的管道对象的持续读取器。

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

前面的示例显示了为实现[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)并[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调例程。 操作参数[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)将允许客户端驱动程序决定在队列中挂起的请求的操作，当设备离开工作状态。 在示例中，指定驱动程序**WdfIoTargetCancelSentIo**。 该选项指示要取消所有挂起的请求在队列中的框架。 或者，驱动程序可以指示要等待挂起的请求，以获取停止 I/O 目标之前完成或者保持挂起的请求并恢复 I/O 目标重新启动时的框架。

### <a name="using-the-continuous-reader---umdf-client-driver"></a>使用连续的读取器-UMDF 客户端驱动程序

在开始使用连续读取器之前，必须配置的实现中的读取器[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)方法。 获取一个指向后[ **IWDFUsbTargetPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff560391)目标管道对象的接口与 IN 终结点相关联，请执行以下步骤：

**配置持续读取器**

1.  调用**QueryInterface**的目标的管道对象 ([**IWDFUsbTargetPipe**](https://msdn.microsoft.com/library/windows/hardware/ff560391)) 和查询[ **IWDFUsbTargetPipe2**](https://msdn.microsoft.com/library/windows/hardware/ff560394)接口。
2.  调用**QueryInterface**上的设备的回调对象和查询[ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)接口。 若要使用连续读取器，必须实现 IUsbTargetPipeContinuousReaderCallbackReadComplete。 实现是在本主题后面所述。
3.  调用**QueryInterface**上的设备的回调对象和查询[IUsbTargetPipeContinuousReaderCallbackReadersFailed](https://msdn.microsoft.com/library/windows/hardware/ff556914)如果已实现失败回调的接口。 实现是在本主题后面所述。
4.  调用[ **IWDFUsbTargetPipe2::ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)方法并指定配置参数，如标头、 尾端、 挂起的请求，以及对完成的引用数和失败回调方法。

    该方法将配置目标管道对象的持续读取器。 持续读取器创建的队列的管理组读取请求被发送并接收来自目标的管道对象。

下面的示例代码配置指定的目标的管道对象的持续读取器。 该示例假定由调用方指定的目标的管道对象是与 IN 终结点相关联。 配置为连续的读取器读取 USBD\_默认\_最大\_传输\_大小字节; 若要使用挂起的请求，由框架; 用于调用客户端驱动程序所提供的默认值数完成和失败回调方法。 接收的缓冲区将不包含任何标头或尾部数据。

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

接下来，当设备进入和退出工作状态时指定的目标的管道对象的状态 (**D0**)。

如果客户端驱动程序使用电源管理队列将请求发送到管道，队列传递请求，仅当设备中时，才**D0**状态。 如果从设备的电源状态更改**D0**到较低的电源状态 (在**D0**退出)、 目标管道对象完成挂起的请求和队列停止提交到目标管道对象的请求. 因此，客户端驱动程序不需要启动和停止目标管道对象。

持续读取器不使用电源管理队列来提交请求。 因此，您必须显式启动或停止目标管道对象，该设备的电源状态更改时。 有关更改目标管道对象的状态，可以使用[ **IWDFIoTargetStateManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff559198)由该框架实现的接口。 获取一个指向后[ **IWDFUsbTargetPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff560391)目标管道对象的接口与 IN 终结点相关联，请执行以下步骤：

**实现状态管理**

1.  中的实现[ **IPnpCallbackHardware::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556766)，调用 [**QueryInterface**目标管道对象 ([ **IWDFUsbTargetPipe**](https://msdn.microsoft.com/library/windows/hardware/ff560391)) 和查询[ **IWDFIoTargetStateManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff559198)接口。 在您的设备回调类的成员变量中存储引用。
2.  实现[ **IPnpCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff556762)设备回调对象的接口。
3.  在实现中的[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)方法中，调用[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)启动持续读取器。
4.  在实现中的[ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)方法中，调用[ **IWDFIoTargetStateManagement::Stop** ](https://msdn.microsoft.com/library/windows/hardware/ff559217)停止持续读取器。

在设备进入工作状态后 (**D0**)，框架将调用客户端驱动程序提供启动目标的 D0 入口回调方法通过管道传递对象。 当设备离开**D0**状态中时，框架将调用 D0 退出回调方法。 目标管道对象完成挂起的读取请求，由客户端驱动程序配置的次数，并停止接受新请求。
下面的代码示例实现[IPnpCallback](https://msdn.microsoft.com/library/windows/hardware/ff556762)设备回调对象的接口。

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

下面的代码示例演示如何获取一个指向目标管道对象的 IWDFIoTargetStateManagement 接口在 IPnpCallback::OnPrepareHardware 方法

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

下面的代码示例演示如何获取一个指向[ **IWDFIoTargetStateManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff559198)中的目标的管道对象的接口[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)方法。

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

持续读取器完成读取的请求后，客户端驱动程序必须提供一种方法，以便在请求成功完成的读取的请求时获得通知。 客户端驱动程序必须将此代码添加到设备回调对象。

**通过实现 IUsbTargetPipeContinuousReaderCallbackReadComplete 提供完成回调**

1.  实现[ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)设备回调对象的接口。
2.  请确保**QueryInterface**的设备回调对象实现的回调对象的引用计数，然后返回[ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)接口指针。
3.  在实现中的[ **IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556910)方法，从管道读取读取数据的访问。 *PMemory*参数指向的框架的包含的数据分配的内存。 您可以调用[ **IWDFMemory::GetDataBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff562631)获取包含数据的缓冲区。 缓冲区包含标头的数据的长度由但是*NumBytesTransferred*的参数**OnReaderCompletion**不包括标头长度。 配置对驱动程序的调用中的连续读取器时由客户端驱动程序指定标头长度[ **IWDFUsbTargetPipe2::ConfigureContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff560395)。
4.  提供指向中的完成回调*pOnCompletion*的参数[ **IWDFUsbTargetPipe2::ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)方法。

数据是可在设备上的终结点上每次目标管道对象完成的读取的请求。 如果读取的请求已成功完成，该框架将通知客户端驱动程序通过调用[ **IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff556910)。 否则，框架在调用客户端驱动程序提供失败回调时目标管道对象读取请求将报告错误。

下面的代码示例实现[ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)设备回调对象的接口。

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

下面的代码示例显示了设备回调对象的 QueryInterface 实现。

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

下面的示例代码演示如何将数据从返回的缓冲区[ **IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff556910)。 每次目标管道对象完成读取时请求成功，框架将调用**OnReaderCompletion**。 示例将获取该 containsng 数据的缓冲区并在调试器输出打印内容。

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

完成的读取的请求时，目标管道对象中发生故障时，客户端驱动程序可以从框架获取通知。 若要获取通知，客户端驱动程序必须实现失败回调并配置持续读取器时提供给回调的指针。 以下过程介绍如何实现失败的回调。

**通过实现 IUsbTargetPipeContinuousReaderCallbackReadersFailed 提供失败回调，**

1.  实现[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed** ](https://msdn.microsoft.com/library/windows/hardware/ff556914)设备回调对象的接口。
2.  请确保**QueryInterface**的设备回调对象实现的回调对象的引用计数，然后返回[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed** ](https://msdn.microsoft.com/library/windows/hardware/ff556914)接口指针。
3.  在实现中的[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://msdn.microsoft.com/library/windows/hardware/ff556915)方法，提供错误处理的失败的读取请求。

    如果连续读取器无法完成读取的请求和客户端驱动程序提供了失败回调，框架将调用[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure**](https://msdn.microsoft.com/library/windows/hardware/ff556915)方法。 该框架提供了中的 HRESULT 值*hrStatus*参数，用于指示目标管道对象中发生的错误代码。 根据错误代码，可能会提供特定错误处理。 例如，如果你想要重置管道，然后重新启动持续读取器的框架，请确保在回调返回 TRUE。

    **请注意**不要调用[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)并[ **IWDFIoTargetStateManagement::Stop** ](https://msdn.microsoft.com/library/windows/hardware/ff559217)中的失败回调。



4.  提供指向中的失败回调*pOnFailure*的参数[ **IWDFUsbTargetPipe2::ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)方法。

下面的代码示例实现[ **IUsbTargetPipeContinuousReaderCallbackReadersFailed** ](https://msdn.microsoft.com/library/windows/hardware/ff556914)设备回调对象的接口。

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

下面的代码示例显示了设备回调对象的 QueryInterface 实现。

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

下面的代码示例显示了失败回调的实现。 如果读取的请求失败，该方法将输出由框架在调试器中报告的错误代码，并指示 framework 重置管道，然后重新启动持续读取器。

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

如果客户端驱动程序不提供失败回调，并出现错误时，框架将重置 USB 管道，并重新启动持续读取器。

## <a name="related-topics"></a>相关主题
[USB I/O 传输](usb-device-i-o.md)  
[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)  
[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)  
[如何在 USB 界面中选择一项备用设置](select-a-usb-alternate-setting.md)  
[USB 客户端驱动程序的常见任务](wdk-resources-for-usb-driver-development.md)  



