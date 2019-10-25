---
title: 用户模式 SPB 外设驱动程序的硬件资源
description: SPB 上外围设备的 UMDF 驱动程序的代码示例，并获取硬件资源。
ms.assetid: 4D240011-1F4E-4C1E-8258-A2CF44BD3F06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48c0e0dbbe16b774cad1beb96885bbe29cde3136
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844784"
---
# <a name="hardware-resources-for-user-mode-spb-peripheral-drivers"></a>用户模式 SPB 外设驱动程序的硬件资源


本主题中的代码示例演示了一个[简单外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))（SPB）上的外围设备的[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)（UMDF）驱动程序如何获得操作设备所需的硬件资源。 这些资源包含驱动程序用于建立到设备的逻辑连接的信息。 其他资源可能包括中断，以及一个或多个 GPIO 输入或输出插针。 （GPIO pin 是一般用途 i/o 控制器设备上的一个配置为输入或输出的 pin; 有关详细信息，请参阅[GPIO 控制器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)。）与内存映射的设备不同，由 SPB 连接的外围设备不需要系统内存地址块来将寄存器映射到。

此驱动程序实现了[**IPnpCallbackHardware2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware2)接口，并在调用驱动程序的[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法的过程中将此接口注册到 UMDF。 框架调用**IPnpCallbackHardware2**接口中的方法，以通知驱动程序设备电源状态发生的更改。

当电源恢复到连接到 SPB 的外围设备时，驱动程序框架将调用[**IPnpCallbackHardware2：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)方法，以通知驱动程序必须准备好使用此设备。 在此调用期间，驱动程序收到两个硬件资源列表作为输入参数。 *PWdfResourcesRaw*参数指向原始资源列表， *pWdfResourcesTranslated*参数指向已转换资源的列表。 这两个参数都是指向[**IWDFCmResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist)对象的指针。 已翻译的资源包括： SPB 外围设备驱动程序需要与连接到 SPB 的外围设备建立逻辑连接的*连接 ID* 。 有关详细信息，请参阅[SPB 外围设备的连接 id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)。

要使 UMDF 外设驱动程序能够在其资源列表中接收连接 Id，安装驱动程序的 INF 文件必须在其特定于 WDF 的**DDInstall**节中包含以下指令：

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**有关此指令的详细信息，请参阅[在 INF 文件中指定 WDF 指令](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)。

下面的代码示例演示驱动程序的**OnPrepareHardware**方法如何从*pWdfResourcesTranslated*参数获取连接 ID。

```cpp
BOOLEAN fConnectIdFound = FALSE;
BOOLEAN fDuplicateFound = FALSE;
LARGE_INTEGER connectionId = 0;
ULONG resourceCount;

resourceCount = pWdfResourcesTranslated->GetCount();

// Loop through the resources and save the relevant ones.
for (ULONG ix = 0; ix < resourceCount; ix++)
{
    PCM_PARTIAL_RESOURCE_DESCRIPTOR pDescriptor;

    pDescriptor = pWdfResourcesTranslated->GetDescriptor(ix);

    if (pDescriptor == NULL)
    {
        hr = E_POINTER;
        break;
    }

    // Determine the resource type.
    switch (pDescriptor->Type)
    {
    case CmResourceTypeConnection:
        {
            // Check against the expected connection types.
            UCHAR Class = pDescriptor->u.Connection.Class;
            UCHAR Type = pDescriptor->u.Connection.Type;

            if (Class == CM_RESOURCE_CONNECTION_CLASS_SERIAL)
            {
                if (Type == CM_RESOURCE_CONNECTION_TYPE_SERIAL_I2C)
                {
                    if (fConnIdFound == FALSE)
                    {
                        // Save the SPB connection ID.
                        connectionId.LowPart = pDescriptor->u.Connection.IdLowPart;
                        connectionId.HighPart = pDescriptor->u.Connection.IdHighPart;
                        fConnectIdFound = TRUE;
                    }
                    else
                    {
                        fDuplicateFound = TRUE;
                    }
                }
            }

            if (Class == CM_RESOURCE_CONNECTION_CLASS_GPIO)
            {
                // Check for GPIO pin resource.
                ...
            }
        }
        break;

    case CmResourceTypeInterrupt:
        {
            // Check for interrupt resources.
            ...
        }
        break;

    default:
        // Ignore all other resource descriptors.
        break;
    }
}
```

前面的代码示例将与 SPB 连接的外围设备的连接 ID 复制到名为 `connectionId`的变量中。 下面的代码示例演示如何将连接 ID 合并为可用于识别外围设备的设备路径名称。

```cpp
WCHAR szTargetPath[100];
HRESULT hres;

// Create the device path using the well-known resource hub
// path name and the connection ID.
//
// TODO: Replace this hardcoded string with the appropriate
//       helper method from Reshub.h when available.
hres = StringCbPrintfW(&szTargetPath[0],
                       sizeof(szTargetPath),
                       L"\\\\.\\RESOURCE_HUB\\%0*I64x",
                       (size_t)(sizeof(LARGE_INTEGER) * 2),
                       connectionId.QuadPart);
if (FAILED(hres))
{
     // Error handling
     ...
}
```

前面的代码示例将与 SPB 连接的外围设备的路径名称写入 `szTargetPath` 数组。 下面的代码示例使用此设备路径名称打开与 SPB 连接的外围设备的文件句柄。

```cpp
UMDF_IO_TARGET_OPEN_PARAMS openParams;

openParams.dwShareMode = 0;
openParams.dwCreationDisposition = OPEN_EXISTING;
openParams.dwFlagsAndAttributes = FILE_FLAG_OVERLAPPED;
hres = pRemoteTarget->OpenFileByName(&szTargetPath[0],
                                     (GENERIC_READ | GENERIC_WRITE),
                                     &openParams);
if (FAILED(hres))
{
    // Error handling
    ...
}
```

在上面的代码示例中，`pRemoteTarget` 变量是指向[**IWDFRemoteTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)对象的指针。 如果对[**IWDFRemoteTarget：： OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)方法的调用成功，则与 SPB 连接的外围设备的驱动程序可以使用**IWDFRemoteTarget**对象将 i/o 请求发送到外围设备。 驱动程序将读取、写入或 IOCTL 请求发送到外围设备之前，驱动程序将调用[**IWDFRemoteTarget：： FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)、 [**IWDFRemoteTarget：： FormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)或[**IWDFRemoteTarget：：** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)用于格式化 i/o 请求的 FormatRequestForIoctl 方法。 **IWDFRemoteTarget**接口从[**IWDFIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)接口继承这三个方法。 接下来，驱动程序调用[**IWDFIoRequest：： send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)方法将 i/o 请求发送到 SPB 连接的外围设备。

在下面的代码示例中，SPB 外设驱动程序调用**send**方法将[**IRP\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求发送到已连接到 SPB 的外围设备。

```cpp
HRESULT hres;
IWDFMemory *pInputMemory = NULL;
IWDFRemoteTarget *pWdfIoRequest = NULL;

// Create a new I/O request.
if (SUCCEEDED(hres))
{
    hres = pWdfDevice->CreateRequest(NULL, 
                                     pWdfDevice, 
                                     &pWdfIoRequest);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

// Allocate memory for the input buffer.
if (SUCCEEDED(hres))
{
    hres = pWdfDriver->CreatePreallocatedWdfMemory(pInBuffer, 
                                                   inBufferSize, 
                                                   NULL,
                                                   pWdfIoRequest,
                                                   &pInputMemory);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }

    // After this call, the parent holds the only reference.
    pWdfMemory->Release();
}

// Format the I/O request for a write operation.
if (SUCCEEDED(hres))
{
    hres = pRemoteTarget->FormatRequestForWrite(pWdfIoRequest,
                                                NULL,
                                                pInputMemory, 
                                                NULL, 
                                                0);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

// Send the request to the SPB controller.
if (SUCCEEDED(hres))
{
    ULONG Flags = fSynchronous ? WDF_REQUEST_SEND_OPTION_SYNCHRONOUS : 0;

    // Set the I/O completion callback.
    if (!fSynchronous)
    {
        pWdfIoRequest->SetCompletionCallback(pCallback, NULL);
    }

    hres = pWdfIoRequest->Send(pRemoteTarget, Flags, 0);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

if (fSynchronous || FAILED(hres))
{
    pWdfIoRequest->DeleteWdfObject();
    SAFE_RELEASE(pWdfIoRequest);
}
```

前面的代码示例执行以下操作：

1.  `pWdfDevice` 变量是指向框架设备对象的[**IWDFDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)接口的指针，该接口表示连接到 SPB 的外围设备。 [**IWDFDevice：： CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)方法创建 i/o 请求，并在由 `pWdfIoRequest` 变量指向的[**IWDFIoRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)接口实例中封装此请求。
2.  `pWdfDriver` 变量是指向框架驱动程序对象的[**IWDFDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)接口的指针，该接口表示 SPB 外围设备驱动程序。 `pInBuffer` 和 `inBufferSize` 变量指定包含写入请求数据的输入缓冲区的地址和大小。 [**IWDFDriver：： CreatePreallocatedWdfMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)方法为输入缓冲区创建框架内存对象，并通过将 `pWdfIoRequest` 的**IWDFIoRequest**对象指定为内存对象的父对象（以便将该内存对象在释放其父项时自动释放）。 驱动程序调用**release**方法以释放其对内存对象的本地引用后，父对象将保留对该对象的唯一引用。
3.  `pWdfRemoteTarget` 变量是在前面的代码示例中从**OpenFileByName**调用获得的远程目标指针。 [**IWDFRemoteTarget：： FormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)方法格式化写入操作的 i/o 请求。
4.  如果要同步发送写入请求，则 `fSynchronous` 变量为**TRUE** ; 如果要以异步方式发送此请求，则为**FALSE** 。 `pCallback` 变量是指向之前创建的[**IRequestCallbackRequestCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)接口的指针。 如果请求是异步发送的，则对[**IWDFIoRequest：： SetCompletionCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)方法的调用将注册此接口。 稍后，将调用[**IRequestCallbackRequestCompletion：： OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)方法，以便在请求异步完成时通知驱动程序。
5.  **Send**方法将格式化写入请求发送到已连接到 SPB 的外围设备。 `Flags` 变量指示是以同步方式还是以异步方式发送写入请求。
6.  如果请求是同步发送的，则[**IWDFIoRequest：:D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)方法会同时删除 `pWdfIoRequest` 的 i/o 请求对象和 `pInputMemory`指向的子对象。 **IWDFIoRequest**接口从[**IWDFObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)接口继承此方法。 如果请求是异步发送的，则应在驱动程序的**OnCompletion**方法中，稍后对**DeleteWdfObject**方法的调用。

前面的代码示例的替代实现可能会在驱动程序初始化过程中创建**IWDFIoRequest**和**IWDFMemory**对象，并重复使用这些相同的对象，而不是在每次 i/o请求已发送。 有关详细信息，请参阅[**IWDFIoRequest2：：重用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)和[**IWDFMemory：： SetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfmemory-setbuffer)。

此外，如果**发送**调用成功，其他实现可能会检查 i/o 请求中的 i/o 状态代码。 有关详细信息，请参阅[**IWDFIoRequest：： GetCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcompletionparams)。

 

 




