---
title: 将 UMDF 外设驱动程序连接到串行端口
description: 适用于 SerCx2 管理的串行端口上的外围设备的 UMDF 驱动程序需要某些硬件资源才能运行设备。 这些资源包含驱动程序打开串行端口逻辑连接所需的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044f770460d3756b421767f106651ee86e821285
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812049"
---
# <a name="connecting-a-umdf-peripheral-driver-to-a-serial-port"></a>将 UMDF 外设驱动程序连接到串行端口

适用于 SerCx2 管理的串行端口上的外围设备的 UMDF 驱动程序需要某些硬件资源才能运行设备。 这些资源包含驱动程序打开串行端口逻辑连接所需的信息。 其他资源可能包括中断，以及一个或多个 GPIO 输入或输出插针。

此驱动程序实现了 [**IPnpCallbackHardware2**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware2) 接口，并在调用驱动程序的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法的过程中向 Windows 驱动程序框架注册此接口。 框架调用 **IPnpCallbackHardware2** 接口中的方法，以通知驱动程序设备电源状态发生的更改。

在串行连接的外围设备进入未初始化的 D0 设备电源状态之后，驱动程序框架将调用驱动程序的 [**IPnpCallbackHardware2：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware) 方法来告知驱动程序准备此设备以供使用。 在此调用期间，驱动程序收到两个硬件资源列表作为输入参数。 *PWdfResourcesRaw* 参数指向原始资源列表， *pWdfResourcesTranslated* 参数指向已转换资源的列表。 这两个参数都是指向 [**IWDFCmResourceList**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist) 对象的指针。 翻译的资源包括连接 ID，外围设备驱动程序需要建立与串行连接的外围设备的逻辑连接。

要使 UMDF 外设驱动程序能够在其资源列表中接收连接 Id，安装驱动程序的 INF 文件必须在其特定于 WDF 的 **DDInstall** 节中包含以下指令：

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess** 有关此指令的详细信息，请参阅 [在 INF 文件中指定 WDF 指令](../wdf/specifying-wdf-directives-in-inf-files.md)。 有关 INX 文件的示例， (用于生成使用此指令的相应 INF 文件) ，请参阅 [WDK 驱动程序示例](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)中的 SpbAccelerometer。

下面的代码示例演示驱动程序的 **OnPrepareHardware** 方法如何从 *pWdfResourcesTranslated* 参数获取连接 ID。

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

前面的代码示例将串行连接外围设备的连接 ID 复制到名为的变量中 `connectionId` 。 下面的代码示例演示如何将连接 ID 合并到可用于识别外围设备连接到的串行控制器的设备路径名称中。

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

前面的代码示例将串行控制器的设备路径名称写入到数组中 `szTargetPath` 。 下面的代码示例使用此路径名称打开串行控制器的文件句柄。

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

在上面的代码示例中， `pRemoteTarget` 参数是指向 [**IWDFRemoteTarget**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget) 对象的指针。 如果对 [**IWDFRemoteTarget：： OpenFileByName**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname) 方法的调用成功，则串行连接的外围设备的驱动程序可以使用 **IWDFRemoteTarget** 对象将 i/o 请求发送到串行控制器。

若要向外围设备发送读取或写入请求，驱动程序首先会调用此对象的 [**IWDFRemoteTarget：： FormatRequestForRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread) 或 [**IWDFRemoteTarget：： FormatRequestForWrite**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite) 方法来格式化请求。  (**IWDFRemoteTarget** 接口从 [**IWDFIoTarget**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget) 接口继承这两种方法。 ) 

若要将 i/o 控制请求发送到串行控制器，驱动程序首先会调用 [**IWDFRemoteTarget：： FormatRequestForIoctl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) 方法来格式化请求。  (**IWDFRemoteTarget** 接口从 **IWDFIoTarget** 接口继承此方法。 ) 接下来，驱动程序调用 **IWDFIoRequest：： send** 方法将 i/o 控制请求发送到串行连接的外围设备。

在下面的代码示例中，外围设备驱动程序向串行控制器发送 i/o 控制请求。

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

前面的代码示例执行以下操作：

1.  `pWdfDevice`变量是指向框架设备对象的 [**IWDFDevice**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)接口的指针，该接口表示串行连接的外围设备。 [**IWDFDevice：： CreateRequest**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)方法创建 i/o 请求，并在参数指向的 [**IWDFIoRequest**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)接口实例中封装此请求 `pWdfIoRequest` 。 稍后会删除 i/o 请求 (参见步骤 6) 。 此实现在某种程度上有些低效，因为它会创建并删除每个发送的 i/o 请求的 request 对象。 一种更有效的方法是对一系列 i/o 请求重复使用相同的请求对象。 有关详细信息，请参阅 [重复使用框架请求对象](../wdf/reusing-framework-request-objects.md)。
2.  `pWdfDriver`变量是指向框架驱动程序对象的 [**IWDFDriver**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)接口的指针，该接口表示外围设备驱动程序。 `pInBuffer`和 `inBufferSize` 变量指定 i/o 控制请求的输入缓冲区的地址和大小。 [**IWDFDriver：： CreatePreallocatedWdfMemory**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)方法为输入缓冲区创建框架内存对象，并将指向的 **IWDFIoRequest** 对象指定 `pWdfIoRequest` 为内存对象的父对象。
3.  `pWdfRemoteTarget`变量是在前面的代码示例中从 **OpenFileByName** 调用获取的远程目标指针。 [**IWDFRemoteTarget：： FormatRequestForIoctl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)方法格式化 i/o 控制操作的请求。 此 `ioctlCode` 变量设置为 [串行 I/o 请求接口](serial-i-o-request-interface.md)的表中列出的 i/o 控制代码之一。
4.  `fSynchronous`如果 i/o 控制请求是同步发送的，则该变量为 **TRUE** ; 如果要以异步方式发送，则为 **FALSE** 。 `pCallback`变量是指向之前创建的 [**IRequestCallbackRequestCompletion**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)接口的指针。 如果请求是异步发送的，则对 [**IWDFIoRequest：： SetCompletionCallback**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback) 方法的调用将注册此接口。 稍后，将调用 [**IRequestCallbackRequestCompletion：： OnCompletion**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion) 方法，以便在请求异步完成时通知驱动程序。
5.  **Send** 方法将格式化写入请求发送到串行连接的外围设备。 `Flags`变量指示是以同步方式还是以异步方式发送写入请求。
6.  如果以同步方式发送请求， [**IWDFIoRequest：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 方法会同时删除指向的 i/o 请求对象和指向的 `pWdfIoRequest` 子对象 `pInputMemory` 。 **IWDFIoRequest** 接口从 [**IWDFObject**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)接口继承此方法。 如果请求是异步发送的，则应在驱动程序的 **OnCompletion** 方法中，稍后对 **DeleteWdfObject** 方法的调用。
