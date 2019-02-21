---
Description: This topic includes a detailed walkthrough of how to use WinUSB Functions to communicate with a USB device that is using Winusb.sys as its function driver.
title: 如何通过使用 WinUSB 函数访问 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bcd3146360736d2402c5fb03ccd28d7ff4661f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523520"
---
# <a name="how-to-access-a-usb-device-by-using-winusb-functions"></a>如何通过使用 WinUSB 函数访问 USB 设备


**摘要**

-   打开设备并获取 WinUSB 处理。
-   获取有关设备、 配置和接口的所有接口、、 和其终结点设置的信息。
-   读取和写入到大容量和中断终结点的数据。

**重要的 Api**

-   [安装程序 Api 函数](https://msdn.microsoft.com/library/windows/hardware/ff550855)
-   [WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)

本主题包括如何使用的详细的演练[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)与正在使用 Winusb.sys 作为其功能驱动程序的 USB 设备进行通信。

如果使用 Microsoft Visual Studio 2013，请使用 WinUSB 模板创建主干应用程序。 在这种情况下，跳过步骤 1 到 3，本主题中的步骤 4 中执行。 该模板打开的文件句柄设备并获取所需的后续操作 WinUSB 句柄。 该句柄存储在应用程序定义设备\_device.h 中的数据结构。

有关模板的详细信息，请参阅写 WinUSB 模板所基于的 Windows 桌面应用。

**请注意**  WinUSB 函数需要 Windows XP 或更高版本。 可以在 C/c + + 应用程序中使用这些函数与 USB 设备进行通信。 Microsoft 不提供有关 WinUSB 托管的 API。

## <a href="" id="pre"></a>系统必备组件


以下各项适用于本演练：

-   此信息适用于 Windows 8.1、 Windows 8、 Windows 7、 Windows Server 2008、 Windows Vista 版本的 Windows。
-   你已安装 Winusb.sys 作为设备的功能驱动程序。 有关此过程的详细信息，请参阅[WinUSB (Winusb.sys) 安装](winusb-installation.md)。
-   本主题中的示例基于[OSR USB FX2 学习工具包设备](http://www.osronline.com/)。 这些示例可用于扩展到其他 USB 设备的过程。

## <a href="" id="setup"></a>步骤 1:创建主干应用基于 WinUSB 模板


若要访问的 USB 设备，首先创建基于的 Windows Driver Kit (WDK) （包含有关 Windows 调试工具) 的集成环境中包含的 WinUSB 模板的主干应用和 Microsoft Visual Studio.You 可以使用模板作为起点。

有关模板的信息进行编码时，如何创建、 生成、 部署和调试该骨架应用，请参阅[编写基于 WinUSB 模板的 Windows 桌面应用](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)。

该模板通过使用枚举设备[SetupAPI](https://msdn.microsoft.com/library/windows/hardware/ff550855)例程，会打开一个文件处理设备，并创建 WinUSB 接口句柄所需的后续任务。 有关示例代码，以便获取设备句柄打开设备，请参阅[模板代码讨论](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)。

## <a href="" id="query"></a>步骤 2:查询设备的 USB 描述符


接下来，查询有关特定于 USB 的信息，例如设备的速度、 接口描述符、 相关终结点和其管道设备。 该过程是类似于 USB 设备驱动程序使用。 但是，应用程序将通过调用完成设备查询[ **WinUsb\_GetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff540257)。

以下列表显示 WinUSB 函数可调用以获取特定于 USB 的信息：

-   其他设备信息。

    调用[ **WinUsb\_QueryDeviceInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff540290)请求从该设备的设备描述符的信息。 若要获取设备的速度，请设置设备\_中的速度 (0x01) *InformationType*参数。 该函数返回降低速度 (0x01) 或高速 (0x03)。

-   接口描述符

    调用[ **WinUsb\_QueryInterfaceSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff540292)并传递设备的接口的句柄来获取相应的接口描述符。 WinUSB 接口句柄对应于第一个接口。 某些 USB 设备，如 OSR Fx2 设备，支持只有一个接口，而无需任何其他设置。 因此，对于这些设备*AlternateSettingNumber*参数设置为零，只进行一次调用该函数。 **WinUsb\_QueryInterfaceSettings**填充调用方分配[ **USB\_接口\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff540065) （在传递结构*UsbAltInterfaceDescriptor*参数) 与有关接口的信息。 例如，设置界面中的终结点数量**bNumEndpoints**的成员**USB\_接口\_描述符**。

    对于支持多个接口的设备，调用[ **WinUsb\_GetAssociatedInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff540245)通过指定替代设置中的获取接口的关联的接口的句柄*AssociatedInterfaceIndex*参数。

-   终结点

    调用[ **WinUsb\_QueryPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff540293)以获取有关每个接口上每个终结点的信息。 **WinUsb\_QueryPipe**填充调用方分配[ **WINUSB\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540285)结构有关的信息指定终结点的管道。 终结点的管道由一个从零开始的索引，并且必须是中的值小于**bNumEndpoints**成员的上一个调用中检索到的接口描述符[ **WinUsb\_QueryInterfaceSettings**](https://msdn.microsoft.com/library/windows/hardware/ff540292)。 OSR Fx2 设备都有一个具有三个终结点的接口。 为此设备，该函数的*AlternateInterfaceNumber*参数设置为 0 和的值*PipeIndex*参数值从 0 到变化 2。

    若要确定管道类型，请检查[ **WINUSB\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540285)结构的**PipeInfo**成员。 此成员设置为之一[ **USBD\_管道\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff539119)枚举值：UsbdPipeTypeControl、 UsbdPipeTypeIsochronous、 UsbdPipeTypeBulk 或 UsbdPipeTypeInterrupt。 OSR USB FX2 设备支持中断管道、 大容量中管道和大容量扩展管道，因此**PipeInfo**设置为 UsbdPipeTypeInterrupt 或 UsbdPipeTypeBulk。 UsbdPipeTypeBulk 值标识批量传输管道，但不提供管道的方向。 方向信息编码中的管道地址，它存储在了高位**WINUSB\_管道\_信息**结构的**PipeId**成员。 确定管道方向的最简单方法是将传递**PipeId** Usb100.h 从以下宏之一的值：

    -   `USB_ENDPOINT_DIRECTION_IN (PipeId)`宏将返回**TRUE**如果方向为向内。
    -   `USB_ENDPOINT_DIRECTION_OUT(PipeId)`宏将返回**TRUE**如果方向为向外。

    应用程序使用**PipeId**值以标识要使用的数据传输中对 WinUSB 函数的调用如下所示的管道[ **WinUsb\_ReadPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff540297) (介绍本主题的"问题 I/O 请求"部分中），因此该示例将存储所有这三个**PipeId**值供以后使用。

下面的代码示例获取 WinUSB 接口句柄指定的设备的速度。

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

下面的代码示例将查询 WinUSB 接口句柄指定的 USB 设备的各种描述符。 示例函数检索受支持的终结点和其管道标识符的类型。 该示例将存储所有三个 PipeId 值以供将来使用。

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

## <a href="" id="control"></a>步骤 3:将控件传输发送到默认终结点


接下来，与设备通信通过向默认终结点发出控制请求。

所有 USB 设备都具有除了与接口关联的终结点的默认终结点。 默认终结点的主要用途是向主机提供可用于配置设备的信息。 但是，设备还可以使用默认终结点，用于特定于设备的目的。 例如，OSR USB FX2 设备使用的默认终结点来控制光线栏和七个段的数字显示。

控制命令包含的 8 字节安装数据包，其中包括指定特定请求和可选的数据缓冲区的请求代码。 请求代码和缓冲区格式是供应商定义。 在此示例中，应用程序将数据发送到设备来控制光线栏。 设置浅色栏的代码是 0xD8，为方便起见，为组定义\_BARGRAPH\_显示。 对于此请求中，设备需要指定哪些元素应亮起通过设置适当的位的 1 个字节的数据缓冲区。

应用程序可以设置这通过用户界面 (UI)，如浅色栏中的元素应亮起通过提供一组八个复选框控件以指定的。 指定的元素对应于在缓冲区中的相应位。 若要避免的 UI 代码，此部分中的示例代码设置位，以便备用灯获取亮起。

**使用以下步骤来发出控制请求。**

1.  分配 1 个字节的数据缓冲区并将数据加载到的缓冲区的指定应亮起通过设置适当的位的元素。
2.  构造在调用方分配的安装程序数据包[ **WINUSB\_安装程序\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff540313)结构。 初始化要表示的请求类型和数据，如下所示的成员：
    -   **RequestType**成员指定请求方向。 它设置为 0，表示主机设备数据传输。 对于设备主机传输，设置为 1 的 RequestType。
    -   **请求**成员设置为此请求，0xD8 供应商定义的代码。 为方便起见，为组定义\_BARGRAPH\_显示。
    -   **长度**成员设置为数据缓冲区的大小。
    -   **索引**并**值**成员不是此请求，因此它们被设置为零。

3.  调用[ **WinUsb\_ControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff540219)来通过传递设备的 WinUSB 接口句柄、 设置数据包和数据缓冲区传输到默认终结点的请求。 在函数收到的已传输到设备中的字节数*LengthTransferred*参数。

下面的代码示例将控制请求发送到指定的 USB 设备，以控制光浅栏上。

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

## <a href="" id="io"></a>步骤 4:发出 I/O 请求


接下来，将数据发送到设备的大容量中和大容量扩展终结点，可用于读取和写入请求，分别。 OSR USB FX2 设备上这些两个终结点配置为环回，因此该设备将数据从大容量终结点移到向外大容量终结点。 它不会更改数据的值或添加任何新数据。 对于环回配置的读取的请求将读取已发送的最新的写入请求数据。 WinUSB 提供以下函数用于发送写入和读取请求：

-   [**WinUsb\_WritePipe**](https://msdn.microsoft.com/library/windows/hardware/ff540322)
-   [**WinUsb\_ReadPipe**](https://msdn.microsoft.com/library/windows/hardware/ff540297)

**若要发送的写入请求**

1.  分配的缓冲区，并用你想要写入设备的数据填充它。 缓冲区大小没有限制，如果则应用程序不会设置 RAW\_IO 作为管道的策略类型。 WinUSB 将缓冲区划分为适当大小的区块，如有必要。 如果原始\_设置 IO，缓冲区的大小受到 WinUSB 支持的最大传输大小。
2.  调用[ **WinUsb\_WritePipe** ](https://msdn.microsoft.com/library/windows/hardware/ff540322)缓冲区写入设备。 传递设备，大容量扩展管道的管道标识符的 WinUSB 接口句柄 (如中所述[USB 描述符查询设备](#query)本主题的部分)，和缓冲区。 该函数返回实际写入中的设备的字节数*bytesWritten*参数。 *Overlapped*参数设置为**NULL**请求了同步操作。 若要执行的异步写入请求，设置*Overlapped*指向的**OVERLAPPED**结构。

编写包含长度为零的数据的请求转发下 USB 堆栈。 如果传输长度大于最大传输长度，WinUSB 请求划分为较小的最大传输长度的请求，并将其按顺序提交。
下面的代码示例分配一个字符串，并将其发送到设备的大容量扩展终结点。

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

**若要发送的读取的请求**

-   调用[ **WinUsb\_ReadPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff540297)从设备的大容量中终结点读取数据。 传递设备、 大容量中终结点，并相应大小的空缓冲区的管道标识符 WinUSB 接口句的柄。 当函数返回时，该缓冲区包含已从设备读取的数据。 在函数中返回的所读取的字节数*bytesread 时非常谨慎*参数。 读取请求，缓冲区必须最大数据包大小的倍数。

长度为零的读取请求立即完成成功和不会在堆栈的下层发送。 如果传输长度大于最大传输长度，WinUSB 请求划分为较小的最大传输长度的请求，并将其按顺序提交。 如果传输长度不是终结点的倍数**MaxPacketSize**，WinUSB 增加到 MaxPacketSize 下一步多个传输的大小。 如果设备返回更多的数据少于请求，WinUSB 保存过多数据。 如果数据来自前面的读取请求保持，WinUSB 将其复制到下一个读取请求的开始和完成请求，如有必要。
下面的代码示例从设备的大容量中终结点读取数据。

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

## <a name="step-5-release-the-device-handles"></a>步骤 5：发布设备句柄


已完成对设备的所有所需的调用后，释放文件句柄和设备的 WinUSB 接口句柄。 为此，调用以下函数：

-   **CloseHandle**释放已通过的句柄**CreateFile**，如步骤 1 中所述。
-   [**WinUsb\_免费**](https://msdn.microsoft.com/library/windows/hardware/ff540233)释放 WinUSB 接口为设备返回的句柄[ **WinUsb\_初始化**](https://msdn.microsoft.com/library/windows/hardware/ff540277)。

## <a name="step-6-implement-main"></a>步骤 6：实现 Main


下面的代码示例演示控制台应用程序的主要功能。

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


如果设备支持同步终结点，则可以使用[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)发送传输。 在 Windows 8.1 中仅支持此功能。

有关详细信息，请参阅[从 WinUSB 桌面应用发送 USB 同步传输](getting-set-up-to-use-windows-devices-usb.md)。

## <a name="related-topics"></a>相关主题
[WinUSB](winusb.md)  
[WinUSB 体系结构和模块](winusb-architecture.md)  
[WinUSB (Winusb.sys) 安装](winusb-installation.md)  
[针对管道策略修改 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 电源管理](winusb-power-management.md)  
[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)  
[编写基于 WinUSB 模板的 Windows 桌面应用](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)  



