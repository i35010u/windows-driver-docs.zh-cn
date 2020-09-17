---
description: 从 Windows 8.1 开始，WinUSB 函数集具有 Api，使桌面应用程序能够在 USB 设备的同步终结点之间传输数据。 对于此类应用程序，Microsoft 提供的 Winusb.sys 必须是设备驱动程序。
title: 发送来自 UWP 桌面应用的 USB 常时等量传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8180cea840ab258034aba2abb0152c0d263a629a
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716132"
---
# <a name="send-usb-isochronous-transfers-from-a-winusb-desktop-app"></a>发送来自 UWP 桌面应用的 USB 常时等量传输


**摘要**

-   同步传输的简要概述。
-   基于终结点间隔值传输缓冲区。
-   使用 [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)发送读写同步数据的传输。

**重要的 API**

-   [**WinUsb \_ QueryPipeEx**](/windows/win32/api/winusb/nf-winusb-winusb_querypipeex)
-   [**WinUsb \_ WriteIsochPipeAsap**](/windows/win32/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb \_ ReadIsochPipeAsap**](/windows/win32/api/winusb/nf-winusb-winusb_readisochpipeasap)

从 Windows 8.1 开始， [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md) 集具有 api，使桌面应用程序能够在 USB 设备的同步终结点之间传输数据。 对于此类应用程序，Microsoft 提供的 Winusb.sys 必须是设备驱动程序。

USB 设备可以支持同步终结点以稳定的速率（如使用音频/视频流式处理）传输与时间相关的数据。 不保证送达。 良好的连接不应删除任何数据包，它不是正常的，也不应丢失数据包，但同步协议可容忍这种损失。

主机控制器在总线上的保留时间段内发送或接收数据，称为 *总线间隔*。 总线间隔的单位取决于总线速度。 对于全速，它是1毫秒的帧，为实现高速和 SuperSpeed，它是 250-微秒 microframes。

主机控制器定期轮询设备。 对于读取操作，当终结点准备发送数据时，设备会在总线间隔中发送数据，以进行响应。 若要写入设备，主机控制器会发送数据。

**应用可在一个服务间隔内发送多少数据**

本主题中的 " *同步数据包* " 一词是指在一个服务间隔内传输的数据量。 该值由 USB 驱动程序堆栈计算，应用可以在查询管道属性时获取值。

同步数据包的大小决定了应用分配的传输缓冲区的大小。 缓冲区必须以帧边界结束。 传输的总大小取决于应用要发送或接收的数据量。 在应用程序启动传输后，主机将 packetizes 传输缓冲区，以便每个间隔中的主机可以发送或接收每个间隔允许的最大字节数。

对于数据传输，不使用所有总线间隔。 在本主题中，使用的总线间隔称为 " *服务间隔*"。

**如何计算传输数据的帧**

应用程序可以选择通过以下两种方式之一来指定帧：

-   自动启动。 在此模式下，应用程序会指示 USB 驱动程序堆栈在下一个合适的帧中发送传输。 应用还必须指定缓冲区是否为连续流，以便驱动程序堆栈能够计算开始帧。
-   指定晚于当前帧的开始帧。 应用应考虑应用启动传输的时间与 USB 驱动程序堆栈处理时间之间的延迟。

**代码示例讨论**

本主题中的示例演示如何使用这些 [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)：

-   [**WinUsb \_ QueryPipeEx**](/windows/win32/api/winusb/nf-winusb-winusb_querypipeex)
-   [**WinUsb \_ RegisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_registerisochbuffer)
-   [**WinUsb \_ UnregisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_unregisterisochbuffer)
-   [**WinUsb \_ WriteIsochPipeAsap**](/windows/win32/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb \_ ReadIsochPipeAsap**](/windows/win32/api/winusb/nf-winusb-winusb_readisochpipeasap)
-   [**WinUsb \_ WriteIsochPipe**](/windows/win32/api/winusb/nf-winusb-winusb_writeisochpipe)
-   [**WinUsb \_ ReadIsochPipe**](/windows/win32/api/winusb/nf-winusb-winusb_readisochpipe)
-   [**WinUsb \_ GetCurrentFrameNumber**](/windows/win32/api/winusb/nf-winusb-winusb_getcurrentframenumber)
-   [**WinUsb \_ GetAdjustedFrameNumber**](/windows/win32/api/winusb/nf-winusb-winusb_getadjustedframenumber)

在本主题中，我们将在三次传输到高速设备时，读取和写入30毫秒的数据。 管道可以在每个服务间隔内传输1024字节。 由于轮询间隔为1，因此将在帧的每个 microframe 中传输数据。 总共30帧将携带 30 \* 8 \* 1024 字节。

用于发送读取和写入传输的函数调用类似。 应用分配一个足够大的传输缓冲区来容纳所有三次传输。 应用通过调用 [**WinUsb \_ RegisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_registerisochbuffer)为特定管道注册缓冲区。 调用返回用于发送传输的注册句柄。 缓冲区将用于后续传输，并调整缓冲区中的偏移量，以发送或接收下一组数据。

示例中的所有传输都是异步发送的。 为此，应用程序分配有三个元素的 [**重叠**](/windows/win32/api/shobjidl/ns-shobjidl-_overlapped) 结构数组，每个元素对应一个传输。 此应用提供事件，以便在传输完成时获得通知，并检索操作的结果。 为此，在数组中的每个 **重叠** 结构中，应用程序分配一个事件并在 **hEvent** 成员中设置句柄。

此图显示了使用 [**WinUsb \_ ReadIsochPipeAsap**](/windows/win32/api/winusb/nf-winusb-winusb_readisochpipeasap) 函数进行三次读传输。 此调用指定每个传输的偏移量和长度。 *ContinueStream*参数值为 FALSE，表示新流。 之后，该应用请求将后续传输立即计划在上一个请求的最后一帧之后，以允许连续流式传输数据。 按帧数计算每帧帧数的同步数据包数 \* ; 8 \* 10。 对于此调用，应用无需担心如何计算开始帧号。

![同步读取传输的 winusb 函数](images/isoch-app-read.png)

此图显示了使用 [**WinUsb \_ WriteIsochPipe**](/windows/win32/api/winusb/nf-winusb-winusb_writeisochpipe) 函数进行三次写入传输。 此调用指定每个传输的偏移量和长度。 在这种情况下，应用必须计算主机控制器开始发送数据的帧号。 在输出时，该函数接收在上一次传输中所使用的最后一个帧之后的帧的帧号。 为获取当前帧，应用将调用 [**WinUsb \_ GetCurrentFrameNumber**](/windows/win32/api/winusb/nf-winusb-winusb_getcurrentframenumber)。 此时，应用必须确保下一次传输的开始帧晚于当前帧，以便 USB 驱动程序堆栈不会丢弃后期数据包。 为此，应用程序将调用 [**WinUsb \_ GetAdjustedFrameNumber**](/windows/win32/api/winusb/nf-winusb-winusb_getadjustedframenumber) 以获取实际的当前帧号， (此帧号晚于接收到的当前帧号) 。 若要在安全端，应用程序添加了五个帧，然后发送传输。

![同步写入传输的 winusb 函数](images/isoch-app-write.png)

每次传输完成后，应用会通过调用 [**WinUsb \_ getoverlappedresult 期间**](/windows/win32/api/winusb/nf-winusb-winusb_getoverlappedresult)获取传输结果。 *BWait*参数设置为 TRUE，以便在操作完成之前不返回调用。 对于读取和写入传输， *lpNumberOfBytesTransferred* 参数始终为0。 对于写入传输，应用程序假定如果操作成功完成，则传输所有字节。 对于读取传输，每个同步数据包 ([**USBD \_ ISO \_ 数据包 \_ 描述符**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_iso_packet_descriptor)) 的**长度**成员都包含在该数据包中每个间隔内传输的字节数。 为获取总长度，应用将添加所有 **长度** 值。

完成后，应用会通过调用 [**WinUsb \_ UnregisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_unregisterisochbuffer)释放同步缓冲区句柄。

## <a name="before-you-start"></a>开始之前...


请确保，

-   设备驱动程序是 Microsoft 提供的驱动程序： WinUSB ( # A0) 。 该驱动程序包含在 \\ Windows \\ System32 文件夹中 \\ 。 有关详细信息，请参阅 [WinUSB ( # A0) 安装](winusb-installation.md)。

-   你先前已通过调用 [**WinUSB \_ Initialize**](/windows/win32/api/winusb/nf-winusb-winusb_initialize)获取了设备的 WinUSB 接口句柄。 所有操作都是通过使用该句柄来执行的。 阅读 [如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

-   活动接口设置具有同步端点。 否则，将无法访问目标终结点的管道。

## <a name="step-1-find-the-isochronous-pipe-in-the-active-setting"></a>步骤1：在活动设置中查找同步管道


1.  通过调用 [**WinUsb \_ QueryInterfaceSettings**](/windows/win32/api/winusb/nf-winusb-winusb_queryinterfacesettings)获取具有同步终结点的 USB 接口。
2.  枚举定义终结点的接口设置的管道。
3.  对于每个终结点，通过调用[**WINUSB \_ QueryPipeEx**](/windows/win32/api/winusb/nf-winusb-winusb_querypipeex)获取[**WINUSB \_ 管道 \_ 信息 \_ EX**](/windows/win32/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)结构中的关联管道属性。 检索到的 **WINUSB \_ 管道 \_ 信息 \_ EX** 结构，其中包含有关同步管道的信息。 结构包含有关管道、类型、id 等的信息。
4.  检查结构成员，以确定它是否是必须用于传输的管道。 如果为，则存储 **PipeId** 值。 在模板代码中，将成员添加到设备 \_ 数据结构，该结构是在设备中定义的。

此示例演示如何确定活动设置是否具有同步终结点并获取有关它们的信息。 在此示例中，该设备是 SuperMUTT 设备。 设备在默认接口中有两个同步终结点，即备用设置1。

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

SuperMUTT 设备在默认接口中定义其同步终结点，其设置为1。 前面的代码获取 **PipeId** 值，并将它们存储在设备 \_ 数据结构中。

## <a name="step-2-get-interval-information-about-the-isochronous-pipe"></a>步骤2：获取有关同步管道的间隔信息


接下来，获取有关在调用 [**WinUsb \_ QueryPipeEx**](/windows/win32/api/winusb/nf-winusb-winusb_querypipeex)时获得的管道的详细信息。

-   **传输大小**

    1.  从检索到的 [**WINUSB \_ 管道 \_ 信息 \_ EX**](/windows/win32/api/winusbio/ns-winusbio-_winusb_pipe_information_ex) 结构，获取 **MaximumBytesPerInterval** 和 **Interval** 值。
    2.  根据要发送或接收的同步数据量，计算传输大小。 例如，请考虑以下计算：

        ` TransferSize = ISOCH_DATA_SIZE_MS * pipeInfoEx.MaximumBytesPerInterval * (8 / pipeInfoEx.Interval);             `

        在此示例中，传输大小计算为10毫秒的同步数据。

-   **同步数据包数**例如，请考虑以下计算：

    用于计算保存整个传输所需的同步数据包的总数。 此信息是读取传输所必需的，并且计算为 `>IsochInTransferSize / pipe.MaximumBytesPerInterval;             ` 。

此示例演示如何将代码添加到步骤1示例，并获取同步管道的间隔值。

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

在前面的代码中，应用程序从[**WINUSB \_ 管道 \_ 信息 \_ **](/windows/win32/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)获取**间隔**和**MaximumBytesPerInterval** ，以计算读取传输所需的传输大小和同步数据包的数量。 对于同步终结点， **Interval** 为1。 该值指示帧的所有 microframes 都带有数据。 基于这一点，若要发送10毫秒的数据，需要10帧，总传输大小为 10 \* 1024 \* 8 字节，80同步数据包，每个1024字节长。

## <a name="step-3-send-a-write-transfer-to-send-data-to-an-isochronous-out-endpoint"></a>步骤3：发送写入传输以将数据发送到同步输出终结点


此过程总结了将数据写入同步终结点的步骤。

1.  分配包含要发送的数据的缓冲区。
2.  如果要以异步方式发送数据，请分配并初始化包含调用方分配的事件对象的句柄的 [**重叠**](/windows/win32/api/shobjidl/ns-shobjidl-_overlapped) 结构。 结构必须初始化为零，否则调用将失败。
3.  通过调用 [**WinUsb \_ RegisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_registerisochbuffer)注册缓冲区。
4.  通过调用 [**WinUsb \_ WriteIsochPipeAsap**](/windows/win32/api/winusb/nf-winusb-winusb_writeisochpipeasap)开始传输。 如果要手动指定传输数据的帧，请改为调用 [**WinUsb \_ WriteIsochPipe**](/windows/win32/api/winusb/nf-winusb-winusb_writeisochpipe) 。
5.  通过调用 [**WinUsb \_ getoverlappedresult 期间**](/windows/win32/api/winusb/nf-winusb-winusb_getoverlappedresult)获取传输结果。
6.  完成后，通过调用 [**WinUsb \_ UnregisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_unregisterisochbuffer)、重叠事件句柄和传输缓冲区来释放缓冲区句柄。

下面是演示如何发送写入传输的示例。

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

## <a name="step-4-send-a-read-transfer-to-receive-data-from-an-isochronous-in-endpoint"></a>步骤4：发送读取传输以从按同步的终结点接收数据


此过程汇总了从同步终结点读取数据的步骤。

1.  分配将在传输结束时接收数据的传输缓冲区。 缓冲区的大小必须基于步骤2中的传输大小计算。 传输缓冲区必须以帧边界结束。
2.  如果要以异步方式发送数据，请将包含句柄的 [**重叠**](/windows/win32/api/shobjidl/ns-shobjidl-_overlapped) 结构分配给调用方分配的事件对象。 结构必须初始化为零，否则调用将失败。
3.  通过调用 [**WinUsb \_ RegisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_registerisochbuffer)注册缓冲区。
4.  根据步骤2中计算的同步数据包数， ([**USBD \_ ISO \_ 数据包 \_ 描述符**](/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_iso_packet_descriptor)) 分配一个同步数据包数组。
5.  通过调用 [**WinUsb \_ ReadIsochPipeAsap**](/windows/win32/api/winusb/nf-winusb-winusb_readisochpipeasap)开始传输。 如果要手动指定将传输数据的开始帧，请改为调用 [**WinUsb \_ ReadIsochPipe**](/windows/win32/api/winusb/nf-winusb-winusb_readisochpipe) 。
6.  通过调用 [**WinUsb \_ getoverlappedresult 期间**](/windows/win32/api/winusb/nf-winusb-winusb_getoverlappedresult)获取传输结果。
7.  完成后，请通过调用 [**WinUsb \_ UnregisterIsochBuffer**](/windows/win32/api/winusb/nf-winusb-winusb_unregisterisochbuffer)、重叠的事件句柄、同步数据包的数组和传输缓冲区来释放缓冲区句柄。

下面是一个示例，演示如何通过调用 WinUsb \_ ReadIsochPipeAsap 和 WinUsb ReadIsochPipe 发送读取传输 \_ 。

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
[如何通过 WinUSB Functions 访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)