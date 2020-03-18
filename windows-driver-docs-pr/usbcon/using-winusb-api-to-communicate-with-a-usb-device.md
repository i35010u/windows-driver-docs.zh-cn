---
Description: 本主题包括一个详细演练，用于说明如何使用 WinUSB 函数来与使用 Winusb.sys 作为其函数驱动程序的 USB 设备进行通信。
title: 如何通过 WinUSB 函数访问 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 214dfc6d36eef05f533aa4eed749ef1a998d1bc8
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79437066"
---
# <a name="how-to-access-a-usb-device-by-using-winusb-functions"></a>如何通过 WinUSB 函数访问 USB 设备


**摘要**

-   打开设备并获取 WinUSB 句柄。
-   获取有关设备、配置和所有接口的接口设置及其终结点的信息。
-   从批量终结点和中断终结点读取数据并将数据写入其中。

**重要的 API**

-   [SetupAPI 函数](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)
-   [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)

本主题包括一个详细演练，用于说明如何使用 [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)来与使用 Winusb.sys 作为其函数驱动程序的 USB 设备进行通信。

如果使用 Microsoft Visual Studio 2013，请使用 WinUSB 模板创建主干应用。 在这种情况下，请跳过步骤 1 到 3，并继续执行本主题中的步骤 4。 该模板将打开设备的文件句柄，并获取后续操作所需的 WinUSB 句柄。 该句柄存储在 device.h 的应用定义 DEVICE\_DATA 结构中。

有关模板的详细信息，请参阅“基于 WinUSB 模板编写 Windows 桌面应用”。

**注意**  WinUSB 函数需要 Windows XP 或更高版本。 可以在 C/C++应用程序中使用这些函数与 USB 设备通信。 Microsoft 不为 WinUSB 提供托管 API。

## <a href="" id="pre"></a>先决条件


以下各项适用于本演练：

-   此信息适用于以下 Windows 版本：Windows 8.1、Windows 8、Windows 7、Windows Server 2008 和 Windows Vista。
-   已将 Winusb.sys 作为设备的函数驱动程序进行了安装。 有关此过程的详细信息，请参阅 [WinUSB (Winusb.sys) 安装](winusb-installation.md)。
-   本主题中的示例基于 [OSR USB FX2 学习工具包设备](https://www.osronline.com/)。 可以使用这些示例将过程扩展到其他 USB 设备。

## <a href="" id="setup"></a>步骤 1：基于 WinUSB 模板创建主干应用


若要访问 USB 设备，请首先基于Windows 驱动程序工具包 (WDK)（带有 Windows 调试工具）和 Microsoft Visual Studio 的集成环境中所包含的 WinUSB 模板创建一个主干应用。可以使用该模板作为起点。

有关模板代码与如何创建、生成、部署和调试主干应用的信息，请参阅[基于 WinUSB 模板编写 Windows 桌面应用](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)。

该模板通过使用 [SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi) 例程来枚举设备，打开设备的文件句柄，并创建后续任务所需的 WinUSB 接口句柄。 有关获取设备句柄并打开设备的示例代码，请参阅[模板代码讨论](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)。

## <a href="" id="query"></a>步骤 2：向设备查询 USB 描述符


接下来，向设备查询特定于 USB 的信息，例如设备速度、接口描述符、相关终结点及其管道。 此过程类似于 USB 设备驱动程序使用的过程。 但是，应用程序通过调用 [**WinUsb\_GetDescriptor**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor) 来完成设备查询。

以下列表显示了 WinUSB 函数，你可以调用这些函数来获取特定于 USB 的信息：

-   其他设备信息。

    调用 [**WinUsb\_QueryDeviceInformation**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querydeviceinformation) 来请求设备的设备描述符中的信息。 若要获取设备的速度，请在 *InformationType* 参数中设置 DEVICE\_SPEED (0x01)。 该函数返回 LowSpeed (0x01) 或 HighSpeed (0x03)。

-   接口描述符

    调用 [**WinUsb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings) 并传递设备的接口句柄以获取相应的接口描述符。 WinUSB 接口句柄对应于第一个接口。 某些 USB 设备（例如 OSR Fx2 设备）仅支持一个接口，没有任何备用设置。 因此，对于这些设备，*AlternateSettingNumber* 参数设置为零，并且该函数仅被调用一次。 **WinUsb\_QueryInterfaceSettings** 使用有关接口的信息填充调用方分配的 [**USB\_INTERFACE\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor) 结构（在 *UsbAltInterfaceDescriptor* 参数中传递）。 例如，接口中的终结点数目在 **USB\_INTERFACE\_DESCRIPTOR** 的 **bNumEndpoints** 成员中设置。

    对于支持多个接口的设备，请通过在 *AssociatedInterfaceIndex* 参数中指定备用设置来调用 [**WinUsb\_GetAssociatedInterface**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getassociatedinterface) 获取关联接口的接口句柄。

-   终结点

    调用 [**WinUsb\_QueryPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe) 获取有关每个接口上每个终结点的信息。 **WinUsb\_QueryPipe** 使用有关指定终结点的管道的信息填充调用方分配的 [**WINUSB\_PIPE\_INFORMATION**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information) 结构。 终结点的管道由从零开始的索引标识，并且必须小于在上一次调用 [**WinUsb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings) 时检索到的接口描述符的 **bNumEndpoints** 成员中的值。 OSR Fx2 设备有一个具有三个终结点的接口。 对于此设备，函数的 *AlternateInterfaceNumber* 参数设置为 0，*PipeIndex* 参数的值的值在 0 到 2 之间变动。

    若要确定管道类型，请检查 [**WINUSB\_PIPE\_INFORMATION**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information) 结构的 **PipeInfo** 成员。 此成员设置为 [**USBD\_PIPE\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ne-usb-_usbd_pipe_type) 枚举值之一：UsbdPipeTypeControl、UsbdPipeTypeIsochronous、UsbdPipeTypeBulk 或 UsbdPipeTypeInterrupt。 OSR USB FX2 设备支持一个中断管道、一个批量传入管道和一个批量传出管道，因此 **PipeInfo** 设置为 UsbdPipeTypeInterrupt 或 UsbdPipeTypeBulk。 UsbdPipeTypeBulk 值标识批量管道，但不提供管道的方向。 方向信息会编码到管道地址的高位中，该地址存储在 **WINUSB\_PIPE\_INFORMATION** 结构的 **PipeId** 成员中。 确定管道方向的最简单方法是将 **PipeId** 值传递到 Usb100.h 中的以下宏之一：

    -   如果方向为 in，则 `USB_ENDPOINT_DIRECTION_IN (PipeId)` 宏将返回 **TRUE**。
    -   如果方向为 out，则 `USB_ENDPOINT_DIRECTION_OUT(PipeId)` 宏将返回 **TRUE**。

    应用程序使用 **PipeId** 值来标识在调用诸如 [**WinUsb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)（在本主题的“发出 I/O 请求”部分中介绍）之类的 WinUSB 函数时要使用哪个管道进行数据传输，因此该示例存储了所有三个 **PipeId** 值，供以后使用。

下面的示例代码获取 WinUSB 接口句柄指定的设备的速度。

```ManagedCPlusPlus
BOOL GetUSBDeviceSpeed(WINUSB_INTERFACE_HANDLE hDeviceHandle, UCHAR* pDeviceSpeed)
{
    if (!pDeviceSpeed || hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    ULONG length = sizeof(UCHAR);

    bResult = WinUsb_QueryDeviceInformation(hDeviceHandle, DEVICE_SPEED, &length, pDeviceSpeed);
    if(!bResult)
    {
        printf("Error getting device speed: %d.\n", GetLastError());
        goto done;
    }

    if(*pDeviceSpeed == LowSpeed)
    {
        printf("Device speed: %d (Low speed).\n", *pDeviceSpeed);
        goto done;
    }
    if(*pDeviceSpeed == FullSpeed)
    {
        printf("Device speed: %d (Full speed).\n", *pDeviceSpeed);
        goto done;
    }
    if(*pDeviceSpeed == HighSpeed)
    {
        printf("Device speed: %d (High speed).\n", *pDeviceSpeed);
        goto done;
    }

done:
    return bResult;
}
```

下面的示例代码查询 WinUSB 接口句柄指定的 USB 设备的各种描述符。 该示例函数检索受支持终结点的类型及其管道标识符。 该示例存储所有三个 PipeId 值供以后使用。

```ManagedCPlusPlus
struct PIPE_ID
{
    UCHAR  PipeInId;
    UCHAR  PipeOutId;
};

BOOL QueryDeviceEndpoints (WINUSB_INTERFACE_HANDLE hDeviceHandle, PIPE_ID* pipeid)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    USB_INTERFACE_DESCRIPTOR InterfaceDescriptor;
    ZeroMemory(&InterfaceDescriptor, sizeof(USB_INTERFACE_DESCRIPTOR));

    WINUSB_PIPE_INFORMATION  Pipe;
    ZeroMemory(&Pipe, sizeof(WINUSB_PIPE_INFORMATION));

    
    bResult = WinUsb_QueryInterfaceSettings(hDeviceHandle, 0, &InterfaceDescriptor);

    if (bResult)
    {
        for (int index = 0; index < InterfaceDescriptor.bNumEndpoints; index++)
        {
            bResult = WinUsb_QueryPipe(hDeviceHandle, 0, index, &Pipe);

            if (bResult)
            {
                if (Pipe.PipeType == UsbdPipeTypeControl)
                {
                    printf("Endpoint index: %d Pipe type: Control Pipe ID: %d.\n", index, Pipe.PipeType, Pipe.PipeId);
                }
                if (Pipe.PipeType == UsbdPipeTypeIsochronous)
                {
                    printf("Endpoint index: %d Pipe type: Isochronous Pipe ID: %d.\n", index, Pipe.PipeType, Pipe.PipeId);
                }
                if (Pipe.PipeType == UsbdPipeTypeBulk)
                {
                    if (USB_ENDPOINT_DIRECTION_IN(Pipe.PipeId))
                    {
                        printf("Endpoint index: %d Pipe type: Bulk Pipe ID: %c.\n", index, Pipe.PipeType, Pipe.PipeId);
                        pipeid->PipeInId = Pipe.PipeId;
                    }
                    if (USB_ENDPOINT_DIRECTION_OUT(Pipe.PipeId))
                    {
                        printf("Endpoint index: %d Pipe type: Bulk Pipe ID: %c.\n", index, Pipe.PipeType, Pipe.PipeId);
                        pipeid->PipeOutId = Pipe.PipeId;
                    }

                }
                if (Pipe.PipeType == UsbdPipeTypeInterrupt)
                {
                    printf("Endpoint index: %d Pipe type: Interrupt Pipe ID: %d.\n", index, Pipe.PipeType, Pipe.PipeId);
                }
            }
            else
            {
                continue;
            }
        }
    }

done:
    return bResult;
}
```

## <a href="" id="control"></a>步骤 3：将控制传输发送到默认终结点


接下来，通过向默认终结点发出控制请求来与设备通信。

除了与接口关联的终结点外，所有 USB 设备还有一个默认终结点。 默认终结点的主要用途是为主机提供可用来配置设备的信息。 不过，设备还可以将默认终结点用于设备特定的用途。 例如，OSR USB FX2 设备使用默认终结点来控制灯条和 7 段数字显示器。

控制命令包含一个 8 字节设置数据包，其中包括指定特定请求的请求代码和可选的数据缓冲区。 请求代码和缓冲区格式是供应商定义的。 在此示例中，应用程序将数据发送到设备来控制灯条。 用于设置灯条的代码为 0xD8，为方便起见，它被定义为 SET\_BARGRAPH\_DISPLAY。 对于此请求，设备需要一个 1 字节数据缓冲区，该缓冲区通过设置相应的位来指定应点亮哪些元素。

应用程序可以通过用户界面 (UI) 对此进行设置，例如，通过提供总数为 8 个的一组复选框控件来指定应点亮灯条的哪些元素。 指定的元素对应于缓冲区中的相应位。 为避免编写 UI 代码，此部分中的示例代码将设置位以使备用灯亮起。

**使用以下步骤发出控制请求。**

1.  分配一个 1 字节数据缓冲区，并将数据加载到通过设置相应位来指定应点亮的元素的缓冲区中。
2.  在调用方分配的 [**WINUSB\_SETUP\_PACKET**](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet) 结构中构造一个设置数据包。 将成员初始化，以便表示请求类型和数据，如下所示：
    -   **RequestType** 成员指定请求方向。 它设置为 0，表示主机到设备的数据传输。 对于设备到主机的传输，请将 RequestType 设置为 1。
    -   **Request** 成员已针对此请求设置为供应商定义的代码 0xD8。 为方便起见，它被定义为 SET\_BARGRAPH\_DISPLAY。
    -   **Length** 成员设置为数据缓冲区的大小。
    -   **Index** 和 **Value** 成员对于此请求而言并非必需，因此它们设置为零。

3.  调用 [**WinUsb\_ControlTransfer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)，以便通过传递设备的 WinUSB 接口句柄、设置数据包和数据缓冲区来将请求传输到默认终结点。 该函数在 *LengthTransferred* 参数中接收已传输到的设备的字节数。

下面的代码示例将控制请求发送到指定的 USB 设备，以便控制灯条上的灯。

```ManagedCPlusPlus
BOOL SendDatatoDefaultEndpoint(WINUSB_INTERFACE_HANDLE hDeviceHandle)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    
    UCHAR bars = 0;

    WINUSB_SETUP_PACKET SetupPacket;
    ZeroMemory(&SetupPacket, sizeof(WINUSB_SETUP_PACKET));
    ULONG cbSent = 0;

    //Set bits to light alternate bars
    for (short i = 0; i < 7; i+= 2)
    {
        bars += 1 << i;
    }

    //Create the setup packet
    SetupPacket.RequestType = 0;
    SetupPacket.Request = 0xD8;
    SetupPacket.Value = 0;
    SetupPacket.Index = 0; 
    SetupPacket.Length = sizeof(UCHAR);

    bResult = WinUsb_ControlTransfer(hDeviceHandle, SetupPacket, &bars, sizeof(UCHAR), &cbSent, 0);
    if(!bResult)
    {
        goto done;
    }

    printf("Data sent: %d \nActual data transferred: %d.\n", sizeof(bars), cbSent);


done:
    return bResult;

}
```

## <a href="" id="io"></a>步骤 4：发出 I/O 请求


接下来，将数据发送到设备的批量传入终结点和批量传出终结点，这两种终结点可分别用于读取请求和写入请求。 在 OSR USB FX2 设备上，已为环回功能配置了这两个终结点，因此设备会将数据从批量传入终结点移动到批量传出终结点。 它不会更改数据的值或添加任何新数据。 对于环回配置，读取请求将读取由最新写入请求发送的数据。 WinUSB 提供了以下用于发送写入请求和读取请求的函数：

-   [**WinUsb\_WritePipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)
-   [**WinUsb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)

**发送写入请求**

1.  分配一个缓冲区并使用要写入到设备的数据进行填充。 如果应用程序未将 RAW\_IO 设置为管道的策略类型，则缓冲区大小没有限制。 如有必要，WinUSB 会将缓冲区划分为适当大小的区块。 如果设置了 RAW\_IO，则缓冲区的大小将受 WinUSB 支持的最大传输大小限制。
2.  调用 [**WinUsb\_WritePipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe) 将缓冲区写入到设备。 传递设备的 WinUSB 接口句柄、用于批量传出管道的管道标识符（如本主题的[向设备查询 USB 描述符](#query)部分所述）和缓冲区。 函数在 *bytesWritten* 参数中返回实际写入到设备的字节数。 *Overlapped* 参数设置为 **NULL** 以请求同步操作。 若要执行异步写入请求，请将 *Overlapped* 设置为指向 **OVERLAPPED** 结构的指针。

包含长度为零的数据的写入请求将沿 USB 堆栈向下转发。 如果传输长度大于最大传输长度，则 WinUSB 会将该请求划分成长度为最大传输长度的较小请求，并按顺序提交它们。
下面的代码示例分配一个字符串，并将其发送到设备的批量传出终结点。

```ManagedCPlusPlus
BOOL WriteToBulkEndpoint(WINUSB_INTERFACE_HANDLE hDeviceHandle, UCHAR* pID, ULONG* pcbWritten)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE || !pID || !pcbWritten)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    UCHAR szBuffer[] = "Hello World";
    ULONG cbSize = strlen(szBuffer);
    ULONG cbSent = 0;

    bResult = WinUsb_WritePipe(hDeviceHandle, *pID, szBuffer, cbSize, &cbSent, 0);
    if(!bResult)
    {
        goto done;
    }

    printf("Wrote to pipe %d: %s \nActual data transferred: %d.\n", *pID, szBuffer, cbSent);
    *pcbWritten = cbSent;


done:
    return bResult;

}
```

**发送读取请求**

-   调用 [**WinUsb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe) 从设备的批量传入终结点读取数据。 传递设备的 WinUSB 接口句柄、用于批量传入终结点的管道标识符，以及适当大小的空缓冲区。 当函数返回时，缓冲区会包含已从设备读取的数据。 已读取的字节数在函数的 *bytesRead* 参数中返回。 对于读取请求，缓冲区大小必须是最大数据包大小的倍数。

长度为零的读取请求会立即完成（结果为成功），并且不会沿堆栈向下发送。 如果传输长度大于最大传输长度，则 WinUSB 会将该请求划分成长度为最大传输长度的较小请求，并按顺序提交它们。 如果传输长度不是终结点的 **MaxPacketSize** 的倍数，则 WinUSB 会将传输的大小增加到 MaxPacketSize 的下一倍数。 如果设备返回的数据多于已请求的数据，WinUSB 将保存多余的数据。 如果来自上一个读取请求的数据仍然存在，则 WinUSB 会将其复制到下一个读取请求的开头，并完成请求（如有必要）。
下面的代码示例从设备的批量传入终结点读取数据。

```ManagedCPlusPlus
BOOL ReadFromBulkEndpoint(WINUSB_INTERFACE_HANDLE hDeviceHandle, UCHAR* pID, ULONG cbSize)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    UCHAR* szBuffer = (UCHAR*)LocalAlloc(LPTR, sizeof(UCHAR)*cbSize);
    
    ULONG cbRead = 0;

    bResult = WinUsb_ReadPipe(hDeviceHandle, *pID, szBuffer, cbSize, &cbRead, 0);
    if(!bResult)
    {
        goto done;
    }

    printf("Read from pipe %d: %s \nActual data read: %d.\n", *pID, szBuffer, cbRead);


done:
    LocalFree(szBuffer);
    return bResult;

}
```

## <a name="step-5-release-the-device-handles"></a>步骤 5：释放设备句柄


完成对设备的全部所需调用后，请释放设备的文件句柄和 WinUSB 接口句柄。 为此，请调用以下函数：

-   **CloseHandle** 释放由 **CreateFile** 创建的句柄，如步骤 1 中所述。
-   [**WinUsb\_Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free) 释放设备的 WinUSB 接口句柄，该句柄由 [**WinUsb\_Initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize) 返回。

## <a name="step-6-implement-main"></a>步骤 6：实现 Main


下面的代码示例显示了控制台应用程序的 main 函数。

```ManagedCPlusPlus
int _tmain(int argc, _TCHAR* argv[])
{

    GUID guidDeviceInterface = OSR_DEVICE_INTERFACE; //in the INF file

    BOOL bResult = TRUE;

    PIPE_ID PipeID;

    HANDLE hDeviceHandle = INVALID_HANDLE_VALUE;
    WINUSB_INTERFACE_HANDLE hWinUSBHandle = INVALID_HANDLE_VALUE;
    
    UCHAR DeviceSpeed;
    ULONG cbSize = 0;

    bResult = GetDeviceHandle(guidDeviceInterface, &hDeviceHandle);
    if(!bResult)
    {
        goto done;
    }

    bResult = GetWinUSBHandle(hDeviceHandle, &hWinUSBHandle);
    if(!bResult)
    {
        goto done;
    }

    bResult = GetUSBDeviceSpeed(hWinUSBHandle, &DeviceSpeed);
    if(!bResult)
    {
        goto done;
    }

    bResult = QueryDeviceEndpoints(hWinUSBHandle, &PipeID);
    if(!bResult)
    {
        goto done;
    }

    bResult = SendDatatoDefaultEndpoint(hWinUSBHandle);
    if(!bResult)
    {
        goto done;
    }

    bResult = WriteToBulkEndpoint(hWinUSBHandle, &PipeID.PipeOutId, &cbSize);
    if(!bResult)
    {
        goto done;
    }

    bResult = ReadFromBulkEndpoint(hWinUSBHandle, &PipeID.PipeInId, cbSize);
    if(!bResult)
    {
        goto done;
    }


    system("PAUSE");

done:
    CloseHandle(hDeviceHandle);
    WinUsb_Free(hWinUSBHandle);

    return 0;
}
```

## <a name="next-steps"></a>后续步骤


如果设备支持常时等量终结点，则可以使用 [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)发送传输。 仅 Windows 8.1 支持此功能。

有关详细信息，请参阅[从 WinUSB 桌面应用发送 USB 常时等量传输](getting-set-up-to-use-windows-devices-usb.md)。

## <a name="related-topics"></a>相关主题
[WinUSB](winusb.md)  
[WinUSB 体系结构和模块](winusb-architecture.md)  
[WinUSB (Winusb.sys) 安装](winusb-installation.md)  
[用于修改管道策略的 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 电源管理](winusb-power-management.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[基于 WinUSB 模板编写 Windows 桌面应用](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)  



