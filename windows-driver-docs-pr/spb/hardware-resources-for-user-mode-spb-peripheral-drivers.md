---
title: 用户模式下存储外围设备驱动程序的硬件资源
description: 代码示例外围设备上存储的 UMDF 驱动程序，并获取的硬件资源。
ms.assetid: 4D240011-1F4E-4C1E-8258-A2CF44BD3F06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ee90c56c37454e4892811d638f94a90a0fbf1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545447"
---
# <a name="hardware-resources-for-user-mode-spb-peripheral-drivers"></a>用户模式下存储外围设备驱动程序的硬件资源


此主题演示中的代码示例如何[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff560442)外围设备上的 (UMDF) 驱动程序[简单的外围总线](https://msdn.microsoft.com/library/windows/hardware/hh450903)（存储） 获取其运行所需的硬件资源设备。 这些资源中包含的是驱动程序使用建立的逻辑连接到设备的信息。 其他资源可能包括中断，以及一个或多个 GPIO 输入或输出插针。 (GPIO 引脚是已配置为输入或输出; 有关详细信息的通用 I/O 控制器设备上的 pin，请参阅[GPIO 控制器驱动程序](https://msdn.microsoft.com/library/windows/hardware/hh439512)。)与不同的是内存映射的设备，与存储连接的外围设备不需要的系统内存地址将映射到其寄存器的块。

此驱动程序实现[ **IPnpCallbackHardware2** ](https://msdn.microsoft.com/library/windows/hardware/hh439727)接口，并注册到此接口 UMDF 驱动程序的调用期间[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)方法。 该框架将调用的方法**IPnpCallbackHardware2**接口以通知中设备的电源状态更改的驱动程序。

电源恢复到存储连接的外围设备，驱动程序框架将调用[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)方法以通知此设备必须是该驱动程序准备使用。 在此调用，驱动程序将收到硬件资源的两个的列表作为输入参数。 *PWdfResourcesRaw*参数指向的原始资源的列表并*pWdfResourcesTranslated*参数指向的已翻译的资源的列表。 这两个参数是指向[ **IWDFCmResourceList** ](https://msdn.microsoft.com/library/windows/hardware/hh439762)对象。 翻译后的资源包括*连接 ID*存储外围设备驱动程序，需要建立与存储连接的外围设备的逻辑连接。 有关详细信息，请参阅[存储外围设备的连接 Id](https://msdn.microsoft.com/library/windows/hardware/hh698216)。

若要启用 UMDF 外围设备驱动程序以接收其资源的列表中的连接 Id，请安装该驱动程序的 INF 文件必须包含以下指令中其 WDF 特定**DDInstall**部分：

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**有关此指令的详细信息，请参阅[INF 文件中指定 WDF 指令](https://msdn.microsoft.com/library/windows/hardware/ff560526)。

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

前面的代码示例将与存储连接的外围设备的连接 ID 复制到一个名为变量`connectionId`。 下面的代码示例演示如何将连接 ID 合并到可用于标识外围设备的设备路径名称。

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

前面的代码示例将写入到存储连接的外围设备的路径名称`szTargetPath`数组。 下面的代码示例使用此设备路径名称以打开存储连接的外围设备的文件句柄。

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

在前面的代码示例中，`pRemoteTarget`变量是一个指向[ **IWDFRemoteTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff560247)对象。 如果在调用[ **IWDFRemoteTarget::OpenFileByName** ](https://msdn.microsoft.com/library/windows/hardware/ff560273)方法成功，驱动程序可以使用存储连接的外围设备**IWDFRemoteTarget**对象传递给将 I/O 请求发送到外围设备。 该驱动程序将读取、 写入或 IOCTL 请求发送到外围设备之前，该驱动程序将调用[ **IWDFRemoteTarget::FormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559233)， [ **IWDFRemoteTarget::FormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559236)，或[ **IWDFRemoteTarget::FormatRequestForIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff559230)方法来设置格式的 I/O 请求。 **IWDFRemoteTarget**接口继承从这三种方法[ **IWDFIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff559170)接口。 接下来，驱动程序调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)方法将 I/O 请求发送到存储连接的外围设备。

在下面的代码示例中，存储外围设备驱动程序将调用**发送**方法发送[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求到存储连接的外围设备。

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

前面的代码示例将执行以下操作：

1.  `pWdfDevice`变量是一个指向[ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917) framework 设备对象表示存储连接的外围设备的接口。 [ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)方法创建的 I/O 请求并封装在此请求[ **IWDFIoRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558985)通过指向接口实例`pWdfIoRequest`变量。
2.  `pWdfDriver`变量是一个指向[ **IWDFDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff558893) framework 驱动程序对象，表示存储外围设备驱动程序的接口。 `pInBuffer`和`inBufferSize`变量指定的地址和包含的数据写入请求的输入缓冲区的大小。 [ **IWDFDriver::CreatePreallocatedWdfMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff558902)方法创建输入缓冲区的 framework 内存对象，并指定**IWDFIoRequest**所指向的对象为通过`pWdfIoRequest`的内存对象的父对象，以便释放其父级时，会自动释放内存对象）。 驱动程序调用后**释放**方法释放的内存的本地引用对象，父持有对此对象的唯一引用。
3.  `pWdfRemoteTarget`变量也是通过一个远程目标指针**OpenFileByName**在前面的代码示例中调用。 [ **IWDFRemoteTarget::FormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559236)方法设置写操作的 I/O 请求。
4.  `fSynchronous`变量是**TRUE**如果写入并且该请求是同步发送**FALSE**它是否以异步方式发送。 `pCallback`变量是指向以前创建的指针[ **IRequestCallbackRequestCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556904)接口。 如果请求是要以异步方式调用发送[ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)方法注册此接口。 更高版本， [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)调用方法来请求以异步方式完成时通知该驱动程序。
5.  **发送**方法将格式化的写入请求发送到存储连接的外围设备。 `Flags`变量指示写入请求是要以同步方式还是以异步方式发送。
6.  如果同步发送请求[ **IWDFIoRequest::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)方法将删除指向这两个 I/O 请求对象`pWdfIoRequest`和子对象指向`pInputMemory`. **IWDFIoRequest**接口继承此方法从[ **IWDFObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560200)接口。 如果发送请求以异步方式调用**DeleteWdfObject**方法应在驱动程序的更高版本，发生**OnCompletion**方法。

前面的代码示例的备用实现可能会创建**IWDFIoRequest**并**IWDFMemory**对象在驱动程序初始化过程中，并重复使用这些相同的对象而不是创建和删除新对象每次发送的 I/O 请求。 有关详细信息，请参阅[ **IWDFIoRequest2::Reuse** ](https://msdn.microsoft.com/library/windows/hardware/ff559048)并[ **IWDFMemory::SetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff560162)。

此外，替代实现可能会检查 I/O 请求中的 I/O 状态代码，如果**发送**调用成功。 有关详细信息，请参阅[ **IWDFIoRequest::GetCompletionParams**](https://msdn.microsoft.com/library/windows/hardware/ff559084)。

 

 




