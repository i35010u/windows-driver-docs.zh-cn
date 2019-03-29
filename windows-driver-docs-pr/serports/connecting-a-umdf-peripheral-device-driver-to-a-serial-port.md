---
title: 将 UMDF 外设驱动程序连接到串行端口
description: 外围设备 SerCx2 托管的串行端口上的 UMDF 驱动程序需要特定硬件资源操作设备。 这些资源中包含的是该驱动程序必须打开的逻辑连接到串行端口的信息。
ms.assetid: 75FC5E79-59E9-4C07-9119-A4FE81CC318E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87dec0cb81cf16e100621063c2eb6ad4738d2c8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349636"
---
# <a name="connecting-a-umdf-peripheral-driver-to-a-serial-port"></a>将 UMDF 外设驱动程序连接到串行端口


外围设备 SerCx2 托管的串行端口上的 UMDF 驱动程序需要特定硬件资源操作设备。 这些资源中包含的是该驱动程序必须打开的逻辑连接到串行端口的信息。 其他资源可能包括中断，以及一个或多个 GPIO 输入或输出插针。

此驱动程序实现[ **IPnpCallbackHardware2** ](https://msdn.microsoft.com/library/windows/hardware/hh439727)接口，并在此接口向 Windows 驱动程序框架注册到驱动程序的调用期间[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)方法。 该框架将调用的方法**IPnpCallbackHardware2**接口以通知中设备的电源状态更改的驱动程序。

按顺序连接的外围设备进入未初始化的 D0 设备电源状态后，驱动程序框架会调用驱动程序的[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)方法，以便通知若要准备用于此设备驱动程序。 在此调用，驱动程序将收到硬件资源的两个的列表作为输入参数。 *PWdfResourcesRaw*参数指向的原始资源的列表并*pWdfResourcesTranslated*参数指向的已翻译的资源的列表。 这两个参数是指向[ **IWDFCmResourceList** ](https://msdn.microsoft.com/library/windows/hardware/hh439762)对象。 翻译后的资源包括外围设备驱动程序所需建立串行连接的外围设备的逻辑连接的连接 ID。

若要启用 UMDF 外围设备驱动程序以接收其资源的列表中的连接 Id，请安装该驱动程序的 INF 文件必须包含以下指令中其 WDF 特定**DDInstall**部分：

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**有关此指令的详细信息，请参阅[INF 文件中指定 WDF 指令](https://msdn.microsoft.com/library/windows/hardware/ff560526)。 使用此指令的 INX 文件 （用来生成相应的 INF 文件） 的示例，请参阅[SpbAccelerometer 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)。

下面的代码示例演示如何在驱动程序**OnPrepareHardware**方法获取的连接 ID *pWdfResourcesTranslated*参数。

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
                    if (Type == CM_RESOURCE_CONNECTION_TYPE_SERIAL_UART)
                    {
                        if (fConnIdFound == FALSE)
                        {
                            // Save the serial controller's connection ID.
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

前面的代码示例将按顺序连接的外围设备的连接 ID 复制到一个名为变量`connectionId`。 下面的代码示例演示如何将连接 ID 合并到可用于识别串行外围设备连接到的控制器的设备路径名称。

```cpp
WCHAR szTargetPath[100];
HRESULT hres;

// Create the device path using the well-known resource hub
// path name and the connection ID.
//
hres = StringCbPrintfW(&szTargetPath[0],
                       sizeof(DevicePath),
                       L"\\\\.\\RESOURCE_HUB\\%0*I64x",
                       (size_t)(sizeof(LARGE_INTEGER) * 2),
                       connectionId.QuadPart);
if (FAILED(hres))
{
     // Error handling
     ...
}
```

前面的代码示例将写入到的串行控制器的设备路径名称`szTargetPath`数组。 下面的代码示例使用此路径名称以打开串行控制器的文件句柄。

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

在前面的代码示例中，`pRemoteTarget`参数是指向指针[ **IWDFRemoteTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff560247)对象。 如果在调用[ **IWDFRemoteTarget::OpenFileByName** ](https://msdn.microsoft.com/library/windows/hardware/ff560273)方法成功，驱动程序可以使用串行连接的外围设备**IWDFRemoteTarget**要将输入/输出请求发送到串行控制器对象。

若要发送读取或写入到外围设备的请求，该驱动程序，首先调用此对象的[ **IWDFRemoteTarget::FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)或[ **IWDFRemoteTarget::FormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559236)方法来设置格式的请求。 ( **IWDFRemoteTarget**接口继承从这两种方法[ **IWDFIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff559170)接口。)

若要发送到串行控制器、 驱动程序的 I/O 控制请求第一个调用[ **IWDFRemoteTarget::FormatRequestForIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff559230)方法来设置格式的请求。 ( **IWDFRemoteTarget**接口继承此方法从**IWDFIoTarget**接口。)接下来，驱动程序调用**IWDFIoRequest::Send**方法将发送到串行连接的外围设备的 I/O 控制请求。

在下面的代码示例中，外围设备驱动程序将 I/O 控制请求发送到串行控制器。

```cpp
HRESULT hres;
IWDFMemory *pInputMemory = NULL;

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
}

// Format the request to be an I/O control request.
if (SUCCEEDED(hres))
{
    hres = pRemoteTarget->FormatRequestForIoctl(pWdfIoRequest,
                                                ioctlCode,
                                                NULL,
                                                pInputMemory, 
                                                NULL, 
                                                NULL,
                                                NULL);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

// Send the request to the serial controller.
if (SUCCEEDED(hres))
{
    ULONG Flags = fSynchronous ? WDF_REQUEST_SEND_OPTION_SYNCHRONOUS : 0;

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

前面的代码示例将执行以下操作：

1.  `pWdfDevice`变量是一个指向[ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917) framework 设备对象，表示按顺序连接的外围设备的接口。 [ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)方法创建的 I/O 请求并封装在此请求[ **IWDFIoRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558985)通过指向接口实例`pWdfIoRequest`参数。 更高版本删除的 I/O 请求 （请参阅步骤 6）。 此实现是某种程度上效率低下，因为它会创建并删除每个 I/O 请求发送一个请求对象。 更有效的方法是重复使用一系列的 I/O 请求的同一请求对象。 有关详细信息，请参阅[重用 Framework 请求对象](https://msdn.microsoft.com/library/windows/hardware/ff544600)。
2.  `pWdfDriver`变量是一个指向[ **IWDFDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff558893) framework 驱动程序对象，表示外围设备驱动程序的接口。 `pInBuffer`和`inBufferSize`变量指定的地址和 I/O 控制请求的输入缓冲区的大小。 [ **IWDFDriver::CreatePreallocatedWdfMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff558902)方法创建输入缓冲区的 framework 内存对象，并指定**IWDFIoRequest**所指向的对象为通过`pWdfIoRequest`作为内存对象的父对象。
3.  `pWdfRemoteTarget`变量也是通过一个远程目标指针**OpenFileByName**在前面的代码示例中调用。 [ **IWDFRemoteTarget::FormatRequestForIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff559230)方法设置格式的 I/O 控制操作的请求。 `ioctlCode`变量设置为一个表中列出的 I/O 控制代码[串行 I/O 请求接口](serial-i-o-request-interface.md)。
4.  `fSynchronous`变量是**TRUE**如果 I/O 控制并且该请求是同步发送**FALSE**它是否以异步方式发送。 `pCallback`变量是指向以前创建的指针[ **IRequestCallbackRequestCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556904)接口。 如果请求是要以异步方式调用发送[ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)方法注册此接口。 更高版本， [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)调用方法来请求以异步方式完成时通知该驱动程序。
5.  **发送**方法将格式化的写入请求发送到串行连接的外围设备。 `Flags`变量指示写入请求是要以同步方式还是以异步方式发送。
6.  如果同步发送请求[ **IWDFIoRequest::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)方法将删除指向这两个 I/O 请求对象`pWdfIoRequest`和子对象指向`pInputMemory`. **IWDFIoRequest**接口继承此方法从[ **IWDFObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560200)接口。 如果发送请求以异步方式调用**DeleteWdfObject**方法应在驱动程序的更高版本，发生**OnCompletion**方法。

 

 




