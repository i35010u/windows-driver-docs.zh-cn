---
Description: 从 Windows 8.1，组 WinUSB 函数都允许在桌面应用程序传输数据传入和传出的 USB 设备的同步终结点的 Api。 对于此类应用程序，由 Microsoft 提供 Winusb.sys 必须是设备驱动程序。
title: 发送来自 UWP 桌面应用的 USB 常时等量传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ee3bdbfda312481de0cd532a37a5ec23f7ed155
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386276"
---
# <a name="send-usb-isochronous-transfers-from-a-winusb-desktop-app"></a>发送来自 UWP 桌面应用的 USB 常时等量传输


**摘要**

-   同步传输的简要概述。
-   传输缓冲区计算基于终结点间隔值。
-   发送传输的读取和写入使用同步数据[WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)。

**重要的 API**

-   [**WinUsb\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)
-   [**WinUsb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)

从 Windows 8.1 的一套[WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)都允许在桌面应用程序传输数据传入和传出的 USB 设备的同步终结点的 Api。 对于此类应用程序，由 Microsoft 提供 Winusb.sys 必须是设备驱动程序。

USB 设备可以支持同步终结点将依赖于时间的数据以稳定速率，如与音频/视频流式处理。 没有任何有保证的传递。 很好的连接不应删除的任何数据包，不正常或预期丢失的数据包，但同步协议是容错的这种损失。

主控制器发送或接收数据总线上的时间的保留期，被称为*总线间隔*。 总线间隔的单位取决于总线速度。 为完整的速度，1 毫秒帧、 高速度和 SuperSpeed，它是 250 毫秒 microframes。

主控制器在固定的时间间隔轮询设备。 对于读取操作，当该终结点已准备好发送数据，设备做出响应通过总线时间间隔内发送数据。 若要写入该设备，主机控制器发送数据。

**应用程序在一个服务间隔内可以发送多少数据**

术语*同步数据包*本主题中引用的一个服务间隔中传输的数据量。 该值通过 USB 驱动程序堆栈和查询管道属性时，应用程序可以获取的值。

同步数据包的大小确定应用程序分配的传输缓冲区的大小。 缓冲区必须在帧边界处结束。 数据应用程序想要发送或接收的多少取决于传输的总大小。 传输启动应用后，主机 packetizes 传输缓冲区，以便在每个间隔中，主机可以发送或接收允许每个间隔的最大字节数。

对于数据传输，需要使用不是所有的总线时间间隔。 在本主题中，称为使用的总线间隔*服务的时间间隔*。

**如何计算中的数据传输的帧**

应用程序可以选择在两种方式之一中指定的框架：

-   是自动的。 在此模式下，应用程序指示 USB 驱动程序堆栈中的下一步的相应帧发送传输。 应用程序还必须指定，以便驱动程序堆栈可以计算开始帧缓冲区是否是连续的流。
-   指定晚于当前帧的起始帧。 应用程序应考虑应用程序启动传输和 USB 驱动程序堆栈处理的时间之间的延迟。

**代码示例讨论**

本主题中的示例演示使用这些[WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md):

-   [**WinUsb\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)
-   [**WinUsb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)
-   [**WinUsb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)
-   [**WinUsb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)
-   [**WinUsb\_WriteIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)
-   [**WinUsb\_ReadIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)
-   [**WinUsb\_GetCurrentFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)
-   [**WinUsb\_GetAdjustedFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)

在本主题中，我们将对读写 30 毫秒为单位的数据在三个传输高速设备。 管道是能够在每个服务间隔中传输 1024 字节。 轮询间隔为 1，因为数据传输在每个 microframe 帧中。 总共 30 帧将携带 30\*8\*1024 字节。

该函数将调用用于发送读取和写入传输量都是类似。 应用程序分配一个足够大以容纳所有三个传输的传输缓冲区。 该应用将通过调用注册的特定管道的缓冲区[ **WinUsb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)。 调用返回的注册句柄，用于发送传输。 对于后续传输会重用缓冲区和缓冲区中的偏移量进行调整，以发送或接收下一个数据集。

在示例中的所有传输是异步都发送。 为此，应用程序分配的数组[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/shobjidl/ns-shobjidl-_overlapped)具有三个元素的结构，对应于每次传输一个。 应用程序提供了事件，以便传输完成并检索操作的结果时获得通知。 为此，在每个**OVERLAPPED**结构数组，该应用程序中的分配一个事件并设置的句柄**hEvent**成员。

下图显示了三个通过使用读取传输[ **WinUsb\_ReadIsochPipeAsap** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)函数。 调用指定偏移量和长度的每次传输。 *ContinueStream*参数值为 FALSE 以指示新的流。 之后，应用请求的前一个请求，以便持续流式处理的数据的最后一帧后立即安排后续传输。 同步数据包数计算为每个框架的数据包\*帧数; 8\*10。 对于此调用，该应用程序无需担心计算开始的帧号码。

![同步读取传输的 winusb 函数](images/isoch-app-read.png)

下图显示了三个使用编写传输[ **WinUsb\_WriteIsochPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)函数。 调用指定偏移量和长度的每次传输。 在这种情况下，应用程序必须计算主机控制器可以在其中开始发送数据的帧号码。 在输出时，该函数收到遵循在上一个传输中使用的最后一帧的帧的帧号码。 若要获取当前帧时，应用程序调用[ **WinUsb\_GetCurrentFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)。 此时，应用程序必须确保传输的下一步开始帧是晚于当前的帧，以便 USB 驱动程序堆栈不会删除后期数据包。 若要执行此操作，应用程序调用[ **WinUsb\_GetAdjustedFrameNumber** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)获取实际的当前帧数 （这是接收到的当前帧数比更高版本）。 为了安全起见，应用程序添加五个帧，并随后将发送传输。

![等时写入传输 winusb 函数](images/isoch-app-write.png)

每次传输完成后，应用程序通过调用来获取传输的结果[ **WinUsb\_GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getoverlappedresult)。 *BWait*参数设置为 TRUE，以便在调用不返回直到完成该操作。 用于读取和写入传输， *lpNumberOfBytesTransferred*参数始终是 0。 写入传输，应用假设如果操作成功完成，已传输的所有字节。 读取传输，**长度**成员的每个同步的数据包 ([**USBD\_ISO\_数据包\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_iso_packet_descriptor))，包含在该数据包，每个间隔中传输的字节数。 若要获取的总长度，该应用将添加所有**长度**值。

应用程序完成后，通过调用释放等时缓冲区句柄[ **WinUsb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)。

## <a name="before-you-start"></a>开始之前...


请确保，

-   设备驱动程序是由 Microsoft 提供的驱动程序：WinUSB (Winusb.sys)。 该驱动程序包含在\\Windows\\System32\\文件夹。 有关详细信息，请参阅[WinUSB (Winusb.sys) 安装](winusb-installation.md)。

-   你以前通过调用获取设备的 WinUSB 接口句柄[ **WinUsb\_初始化**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)。 通过使用该句柄执行所有操作。 读取[如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

-   活动接口设置了同步终结点。 否则，不能访问的目标终结点的管道。

## <a name="step-1-find-the-isochronous-pipe-in-the-active-setting"></a>第 1 步：查找同步管道中活动设置


1.  获取通过调用了同步的终结点的 USB 接口[ **WinUsb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)。
2.  枚举定义的终结点的接口设置的管道。
3.  对于每个终结点中获取相关的管道属性[ **WINUSB\_管道\_信息\_EX** ](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)结构通过调用[ **WinUsb\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)。 检索到**WINUSB\_管道\_信息\_EX**结构，其中包含有关同步管道的信息。 该结构包含有关管道、 其类型、 id 和等等的信息。
4.  检查以确定它是否是必须用于传输管道的结构成员。 如果是，存储**PipeId**值。 在模板代码中，将成员添加到设备\_Device.h 中定义的数据结构。

此示例演示如何确定活动设置是否已同步的终结点并获取有关它们的信息。 在此示例中该设备是 SuperMUTT 设备。 设备的默认接口，备用设置 1 中有两个同步终结点。

```ManagedCPlusPlus

typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];
    UCHAR                   IsochOutPipe;
    UCHAR                   IsochInPipe;

} DEVICE_DATA, *PDEVICE_DATA;

HRESULT
       GetIsochPipes(
       _Inout_ PDEVICE_DATA DeviceData
       )
{
       BOOL result;
       USB_INTERFACE_DESCRIPTOR usbInterface;
       WINUSB_PIPE_INFORMATION_EX pipe;
       HRESULT hr = S_OK;
       UCHAR i;

       result = WinUsb_QueryInterfaceSettings(DeviceData->WinusbHandle,
              0,
              &usbInterface);

       if (result == FALSE)
       {
              hr = HRESULT_FROM_WIN32(GetLastError());
              printf(_T("WinUsb_QueryInterfaceSettings failed to get USB interface.\n"));
              CloseHandle(DeviceData->DeviceHandle);
              return hr;
       }

       for (i = 0; i < usbInterface.bNumEndpoints; i++)
       {
              result = WinUsb_QueryPipeEx(
                     DeviceData->WinusbHandle,
                     1,
                     (UCHAR) i,
                     &pipe);

              if (result == FALSE)
              {
                     hr = HRESULT_FROM_WIN32(GetLastError());
                     printf(_T("WinUsb_QueryPipeEx failed to get USB pipe.\n"));
                     CloseHandle(DeviceData->DeviceHandle);
                     return hr;
              }

              if ((pipe.PipeType == UsbdPipeTypeIsochronous) && (!(pipe.PipeId == 0x80)))
              {
                     DeviceData->IsochOutPipe = pipe.PipeId;
              }
              else if (pipe.PipeType == UsbdPipeTypeIsochronous)
              {
                     DeviceData->IsochInPipe = pipe.PipeId;
              }
       }

       return hr;
}
```

SuperMUTT 设备在定义中的默认接口，其同步终结点设置 1。 前面的代码中获取**PipeId**值，并将其存储在设备\_数据结构。

## <a name="step-2-get-interval-information-about-the-isochronous-pipe"></a>步骤 2：获取有关同步管道的时间间隔信息


接下来，获取有关您在调用中获得的管道的详细信息[ **WinUsb\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)。

-   **传输大小**

    1.  从检索[ **WINUSB\_管道\_信息\_EX** ](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)结构，请获取**MaximumBytesPerInterval**和**间隔**值。
    2.  具体的同步数据量取决于你想要发送或接收，计算的传输大小。 例如，考虑此计算：

        ` TransferSize = ISOCH_DATA_SIZE_MS * pipeInfoEx.MaximumBytesPerInterval * (8 / pipeInfoEx.Interval);             `

        在示例中，同步数据的 10 毫秒计算传输大小。

-   **等时数据包数**例如，考虑此计算：

    若要计算的同步保存整个传输所需的数据包总数。 此信息是必需的读取传输和计算， `>IsochInTransferSize / pipe.MaximumBytesPerInterval;             `。

此示例显示了将代码添加到步骤 1 的示例，并获取等时管道的时间间隔值。

```ManagedCPlusPlus

#define ISOCH_DATA_SIZE_MS   10

typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];
                UCHAR                   IsochOutPipe;
                UCHAR                   IsochInPipe;
                ULONG                   IsochInTransferSize;
                ULONG                   IsochOutTransferSize;
                ULONG                   IsochInPacketCount;

} DEVICE_DATA, *PDEVICE_DATA;


...

if ((pipe.PipeType == UsbdPipeTypeIsochronous) && (!(pipe.PipeId == 0x80)))
{
       DeviceData->IsochOutPipe = pipe.PipeId;

       if ((pipe.MaximumBytesPerInterval == 0) || (pipe.Interval == 0))
       {
         hr = E_INVALIDARG;             
             printf("Isoch Out: MaximumBytesPerInterval or Interval value is 0.\n");
             CloseHandle(DeviceData->DeviceHandle);
             return hr;
       }
       else
       {
             DeviceData->IsochOutTransferSize = 
                 ISOCH_DATA_SIZE_MS * 
                 pipe.MaximumBytesPerInterval *
                 (8 / pipe.Interval);
       }
}
else if (pipe.PipeType == UsbdPipeTypeIsochronous)
{
       DeviceData->IsochInPipe = pipe.PipeId;

       if (pipe.MaximumBytesPerInterval == 0 || (pipe.Interval == 0))
       {
         hr = E_INVALIDARG;    
             printf("Isoch Out: MaximumBytesPerInterval or Interval value is 0.\n");
             CloseHandle(DeviceData->DeviceHandle);
             return hr;
       }
       else
       {
             DeviceData->IsochInTransferSize = 
                 ISOCH_DATA_SIZE_MS * 
                 pipe.MaximumBytesPerInterval * 
                 (8 / pipe.Interval);

             DeviceData->IsochInPacketCount = 
                  DeviceData->IsochInTransferSize / pipe.MaximumBytesPerInterval;
       }
}

...
```

在前面的代码中，应用程序将获取**间隔**并**MaximumBytesPerInterval**从[ **WINUSB\_管道\_信息\_EX** ](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)来计算的传输大小和数量的同步所需的读取传输的数据包。 对于这两个同步终结点，**间隔**为 1。 该值指示框架的所有 microframes 都携带数据。 基础，若要发送的数据，10 毫秒需要 10 个帧，总传输大小为 10\*1024年\*8 个字节和 80 同步数据包，每个 1024 个字节。

## <a name="step-3-send-a-write-transfer-to-send-data-to-an-isochronous-out-endpoint"></a>步骤 3:发送的写入传送，以将数据发送到同步输出终结点


此过程总结了用于将数据写入等时终结点的步骤。

1.  分配缓冲区，其中包含要发送的数据。
2.  如果以异步方式发送数据时，分配并初始化[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/shobjidl/ns-shobjidl-_overlapped)结构，其中包含调用方分配的事件对象的句柄。 该结构必须初始化为零，否则调用将失败。
3.  通过调用注册缓冲区[ **WinUsb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)。
4.  通过调用开始传输[ **WinUsb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)。 如果你想要手动指定的框架中的数据将传输，请调用[ **WinUsb\_WriteIsochPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)相反。
5.  获取传输的结果，通过调用[ **WinUsb\_GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getoverlappedresult)。
6.  完成后，通过调用释放缓冲区句柄[ **WinUsb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)，重叠的事件句柄，并传输缓冲区。

下面是一个示例，演示如何发送写入传输。

```ManagedCPlusPlus
#define ISOCH_TRANSFER_COUNT   3

VOID
    SendIsochOutTransfer(
    _Inout_ PDEVICE_DATA DeviceData,
    _In_ BOOL AsapTransfer
    )
{
    PUCHAR writeBuffer;
    LPOVERLAPPED overlapped;
    ULONG numBytes;
    BOOL result;
    DWORD lastError;
    WINUSB_ISOCH_BUFFER_HANDLE isochWriteBufferHandle;
    ULONG frameNumber;
    ULONG startFrame;
    LARGE_INTEGER timeStamp;
    ULONG i;
    ULONG totalTransferSize;

    isochWriteBufferHandle = INVALID_HANDLE_VALUE;
    writeBuffer = NULL;
    overlapped = NULL;

    printf(_T("\n\nWrite transfer.\n"));

    totalTransferSize = DeviceData->IsochOutTransferSize * ISOCH_TRANSFER_COUNT;

    if (totalTransferSize % DeviceData->IsochOutBytesPerFrame != 0)
    {
        printf(_T("Transfer size must end at a frame boundary.\n"));
        goto Error;
    }

    writeBuffer = new UCHAR[totalTransferSize];

    if (writeBuffer == NULL)
    {
        printf(_T("Unable to allocate memory.\n"));
        goto Error;
    }

    ZeroMemory(writeBuffer, totalTransferSize);

    overlapped = new OVERLAPPED[ISOCH_TRANSFER_COUNT];
    if (overlapped == NULL)
    {
        printf("Unable to allocate memory.\n");
        goto Error;

    }

    ZeroMemory(overlapped, (sizeof(OVERLAPPED) * ISOCH_TRANSFER_COUNT));

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        overlapped[i].hEvent = CreateEvent(NULL, TRUE, FALSE, NULL);

        if (overlapped[i].hEvent == NULL)
        {
            printf("Unable to set event for overlapped operation.\n");
            goto Error;

        }
    }

    result = WinUsb_RegisterIsochBuffer(
        DeviceData->WinusbHandle,
        DeviceData->IsochOutPipe,
        writeBuffer,
        totalTransferSize,
        &isochWriteBufferHandle);

    if (!result)
    {
        printf(_T("Isoch buffer registration failed.\n"));
        goto Error;
    }

    result = WinUsb_GetCurrentFrameNumber(
                DeviceData->WinusbHandle,
                &frameNumber,
                &timeStamp);

    if (!result)
    {
        printf(_T("WinUsb_GetCurrentFrameNumber failed.\n"));
        goto Error;
    }

    startFrame = frameNumber + 5;

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {

        if (AsapTransfer)
        {
            result = WinUsb_WriteIsochPipeAsap(
                isochWriteBufferHandle,
                DeviceData->IsochOutTransferSize * i,
                DeviceData->IsochOutTransferSize,
                (i == 0) ? FALSE : TRUE,
                &overlapped[i]);

            printf(_T("Write transfer sent by using ASAP flag.\n"));
        }
        else
        {

            printf("Transfer starting at frame %d.\n", startFrame);

            result = WinUsb_WriteIsochPipe(
                isochWriteBufferHandle,
                i * DeviceData->IsochOutTransferSize,
                DeviceData->IsochOutTransferSize,
                &startFrame,
                &overlapped[i]);

            printf("Next transfer frame %d.\n", startFrame);

        }

        if (!result)
        {
            lastError = GetLastError();

            if (lastError != ERROR_IO_PENDING)
            {
                printf("Failed to send write transfer with error %x\n", lastError);
            }
        }
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        result = WinUsb_GetOverlappedResult(
            DeviceData->WinusbHandle,
            &overlapped[i],
            &numBytes,
            TRUE);

        if (!result)
        {
            lastError = GetLastError();

            printf("Write transfer %d with error %x\n", i, lastError);
        }
        else
        {
            printf("Write transfer %d completed. \n", i);

        }
    }




Error:
    if (isochWriteBufferHandle != INVALID_HANDLE_VALUE)
    {
        result = WinUsb_UnregisterIsochBuffer(isochWriteBufferHandle);
        if (!result)
        {
            printf(_T("Failed to unregister isoch write buffer. \n"));
        }
    }

    if (writeBuffer != NULL)
    {
        delete [] writeBuffer;
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        if (overlapped[i].hEvent != NULL)
        {
            CloseHandle(overlapped[i].hEvent);
        }

    }

    if (overlapped != NULL)
    {
        delete [] overlapped;
    }


    return;
}
```

## <a name="step-4-send-a-read-transfer-to-receive-data-from-an-isochronous-in-endpoint"></a>步骤 4：发送以接收来自终结点中同步数据读取的传输


此过程总结了用于从同步终结点读取数据的步骤。

1.  分配将接收传输末尾处的数据的传输缓冲区。 缓冲区的大小必须基于在步骤 2 中的大小计算上传输。 传输缓冲区必须在帧边界处结束。
2.  如果以异步方式发送数据时，将分配[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/shobjidl/ns-shobjidl-_overlapped)结构，其中包含调用方分配的事件对象的句柄。 该结构必须初始化为零，否则调用将失败。
3.  通过调用注册缓冲区[ **WinUsb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)。
4.  基于同步数计算步骤 2 中的数据包分配同步数据包的数组 ([**USBD\_ISO\_数据包\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_iso_packet_descriptor))。
5.  通过调用开始传输[ **WinUsb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)。 如果你想要手动指定起始帧中的数据将传输，请调用[ **WinUsb\_ReadIsochPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)相反。
6.  获取传输的结果，通过调用[ **WinUsb\_GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getoverlappedresult)。
7.  完成后，通过调用释放缓冲区句柄[ **WinUsb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)、 重叠的事件句柄、 同步数据包的数组和传输缓冲区。

下面是一个示例，演示如何将读取的传输发送通过调用 WinUsb\_ReadIsochPipeAsap 和 WinUsb\_ReadIsochPipe。

```ManagedCPlusPlus
#define ISOCH_TRANSFER_COUNT   3

VOID
    SendIsochInTransfer(
    _Inout_ PDEVICE_DATA DeviceData,
    _In_ BOOL AsapTransfer
    )
{
    PUCHAR readBuffer;
    LPOVERLAPPED overlapped;
    ULONG numBytes;
    BOOL result;
    DWORD lastError;
    WINUSB_ISOCH_BUFFER_HANDLE isochReadBufferHandle;
    PUSBD_ISO_PACKET_DESCRIPTOR isochPackets;
    ULONG i;
    ULONG j;

    ULONG frameNumber;
    ULONG startFrame;
    LARGE_INTEGER timeStamp;

    ULONG totalTransferSize;

    readBuffer = NULL;
    isochPackets = NULL;
    overlapped = NULL;
    isochReadBufferHandle = INVALID_HANDLE_VALUE;

    printf(_T("\n\nRead transfer.\n"));

    totalTransferSize = DeviceData->IsochOutTransferSize * ISOCH_TRANSFER_COUNT;

    if (totalTransferSize % DeviceData->IsochOutBytesPerFrame != 0)
    {
        printf(_T("Transfer size must end at a frame boundary.\n"));
        goto Error;
    }

    readBuffer = new UCHAR[totalTransferSize];

    if (readBuffer == NULL)
    {
        printf(_T("Unable to allocate memory.\n"));
        goto Error;
    }

    ZeroMemory(readBuffer, totalTransferSize);

    overlapped = new OVERLAPPED[ISOCH_TRANSFER_COUNT];
    ZeroMemory(overlapped, (sizeof(OVERLAPPED) * ISOCH_TRANSFER_COUNT));

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        overlapped[i].hEvent = CreateEvent(NULL, TRUE, FALSE, NULL);

        if (overlapped[i].hEvent == NULL)
        {
            printf("Unable to set event for overlapped operation.\n");
            goto Error;
        }
    }

    isochPackets = new USBD_ISO_PACKET_DESCRIPTOR[DeviceData->IsochInPacketCount * ISOCH_TRANSFER_COUNT];
    ZeroMemory(isochPackets, DeviceData->IsochInPacketCount * ISOCH_TRANSFER_COUNT);

    result = WinUsb_RegisterIsochBuffer(
        DeviceData->WinusbHandle,
        DeviceData->IsochInPipe,
        readBuffer,
        DeviceData->IsochInTransferSize * ISOCH_TRANSFER_COUNT,
        &isochReadBufferHandle);

    if (!result)
    {
        printf(_T("Isoch buffer registration failed.\n"));
        goto Error;
    }

    result = WinUsb_GetCurrentFrameNumber(
                DeviceData->WinusbHandle,
                &frameNumber,
                &timeStamp);

    if (!result)
    {
        printf(_T("WinUsb_GetCurrentFrameNumber failed.\n"));
        goto Error;
    }

    startFrame = frameNumber + 5;

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        if (AsapTransfer)
        {
            result = WinUsb_ReadIsochPipeAsap(
                isochReadBufferHandle,
                DeviceData->IsochInTransferSize * i,
                DeviceData->IsochInTransferSize,
                (i == 0) ? FALSE : TRUE,
                DeviceData->IsochInPacketCount,
                &isochPackets[i * DeviceData->IsochInPacketCount],
                &overlapped[i]);

            printf(_T("Read transfer sent by using ASAP flag.\n"));

        }
        else
        {

            printf("Transfer starting at frame %d.\n", startFrame);

            result = WinUsb_ReadIsochPipe(
                isochReadBufferHandle,
                DeviceData->IsochInTransferSize * i,
                DeviceData->IsochInTransferSize,
                &startFrame,
                DeviceData->IsochInPacketCount,
                &isochPackets[i * DeviceData->IsochInPacketCount],
                &overlapped[i]);

            printf("Next transfer frame %d.\n", startFrame);

        }

        if (!result)
        {
            lastError = GetLastError();

            if (lastError != ERROR_IO_PENDING)
            {
                printf("Failed to start a read operation with error %x\n", lastError);
            }
        }
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        result = WinUsb_GetOverlappedResult(
            DeviceData->WinusbHandle,
            &overlapped[i],
            &numBytes,
            TRUE);

        if (!result)
        {
            lastError = GetLastError();

            printf("Failed to read with error %x\n", lastError);
        }
        else
        {
            numBytes = 0;
            for (j = 0; j < DeviceData->IsochInPacketCount; j++)
            {
                numBytes += isochPackets[j].Length;
            }

            printf("Requested %d bytes in %d packets per transfer.\n", DeviceData->IsochInTransferSize, DeviceData->IsochInPacketCount);
        }

        printf("Transfer %d completed. Read %d bytes. \n\n", i+1, numBytes);
    }



Error:
    if (isochReadBufferHandle != INVALID_HANDLE_VALUE)
    {
        result = WinUsb_UnregisterIsochBuffer(isochReadBufferHandle);
        if (!result)
        {
            printf(_T("Failed to unregister isoch read buffer. \n"));
        }
    }    

    if (readBuffer != NULL)
    {
        delete [] readBuffer;
    }

    if (isochPackets != NULL)
    {
        delete [] isochPackets;
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)

    {
        if (overlapped[i].hEvent != NULL)
        {
            CloseHandle(overlapped[i].hEvent);
        }

    }

    if (overlapped != NULL)
    {
        delete [] overlapped;
    }
    return;
}
```

## <a name="related-topics"></a>相关主题
[如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)  



