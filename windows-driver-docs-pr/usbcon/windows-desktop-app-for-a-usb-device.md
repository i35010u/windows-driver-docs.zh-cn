---
description: 了解应用程序如何调用 WinUSB 函数以与 USB 设备进行通信。
title: USB 设备的 Windows 桌面应用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed8c93d71ed546106542e318d29ad539a7d8f0f5
ms.sourcegitcommit: b75e9940d49410e2b952e96f325df67a039cd571
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92337021"
---
# <a name="windows-desktop-app-for-a-usb-device"></a>USB 设备的 Windows 桌面应用

在本主题中，你将了解应用程序如何调用 [WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb) 来与 USB 设备通信。 对于此类应用程序，必须将 [WinUSB](winusb.md) ( # A0) 安装为设备的功能驱动程序。 设备内核模式堆栈中的 WinUSB。 此驱动程序包含在 windows 的 \\ windows \\ System32 \\ 驱动程序文件夹中。

如果使用 Winusb.sys 作为 USB 设备的功能驱动程序，则可以从应用程序中调用 [WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb) 以与设备进行通信。 这些函数由用户模式 DLL Winusb.dll 公开，用于简化通信过程。 应用程序调用等效的 WinUSB 函数，而不是构建设备 i/o 控制请求来执行标准 USB 操作 (例如配置设备、发送控制请求以及将数据传输到设备) 。

Winusb.dll 使用应用程序提供的数据来构造相应的设备 i/o 控制请求，然后将请求发送到 Winusb.sys 进行处理。 若要与 USB stack 通信，WinUSB 函数会调用 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数，其中包含与应用程序的请求相关联的相应 IOCTL。 请求完成后，WinUSB 函数会将 Winusb.sys (返回的任何信息（例如读取) 请求中的数据）传递回调用进程。 如果对 **DeviceIoControl** 的调用成功，它将返回一个非零值。 如果调用失败或挂起 (未立即处理) ，则 **DeviceIoControl** 将返回一个零值。 如果发生错误，应用程序可以调用 [**GetLastError**](/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror) 以获取更详细的错误消息。

使用 WinUSB 函数与设备进行通信比实现驱动程序更简单。 不过，请注意以下限制：

- WinUSB 函数允许一次应用程序与设备进行通信。 如果需要多个应用程序同时与设备进行通信，则必须实现函数驱动程序。

- 在 Windows 8.1 之前，WinUSB 函数不支持向或从同步终结点流式传输数据。

- WinUSB 函数不支持已具有内核模式支持的设备。 此类设备的示例包括调制解调器和网络适配器，这些适配器分别受电话 API (TAPI) 和 NDIS 支持。

- 对于多功能设备，你可以使用设备的 INF 文件单独指定每个 USB 函数的内置内核模式驱动程序或 Winusb.sys。 但是，只能为特定函数指定其中一个选项，而不能同时指定这两者。

> [!NOTE]
> WinUSB 函数需要 Windows XP 或更高版本。 可以在 C/C++应用程序中使用这些函数与 USB 设备通信。 若要编写使用 WinUSB Api 的 UWP 应用，请参阅 [USB 设备的 uwp 应用](writing-usb-device-companion-apps-for-microsoft-store.md)。

## <a name="getting-started"></a>入门

1. 获取编写适用于设备的 Windows 桌面应用程序所需的工具

    - 按照 [下载 Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)中的说明进行操作。

2. 获取测试 USB 设备及其硬件规范。

    使用规范来确定应用程序的功能和相关的设计决策。 出于学习目的，常用的选项包括：

    - [ (OSR) 商店中的开放系统资源](https://www.osr.com/online-seminars/)提供的 OSR USB FX2 学习套件。 此工具包最适合学习本文档集中包括的 USB 示例。

    - Microsoft USB 测试工具 (可通过 [JJG 技术](http://www.jjgtechnologies.com/Mutt20.htm)使用的 MUTT) 设备。 此设备需要 Microsoft 提供的固件，请参阅 [下载 MUTT](/windows-hardware/drivers/usbcon/mutt-software-package#download-mutt-software-package)软件包。

3. 编写一个框架应用，用于获取设备的句柄。

    编写第一个应用程序的方法有两种：

    - 基于包含在 Visual Studio 中的 WinUSB 模板编写。 有关详细信息，请参阅 [基于 WinUSB 模板编写 Windows 桌面应用](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)。

    - 调用 [setupapi.log](/windows-hardware/drivers/install/setupapi) 例程以获取设备的句柄，并通过调用 [WinUsb_Initialize](/windows/desktop/api/winusb/nf-winusb-winusb_initialize)将其打开。 有关详细信息，请参阅 [如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

4. 安装设备 Winusb.sys。

    如果使用的是 Visual Studio，请使用 Visual Studio 部署在目标计算机上安装驱动程序包。 有关说明，请参阅 [基于 WinUSB 模板编写 Windows 桌面应用](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)。 否则，通过编写自定义 INF，在设备管理器中手动安装驱动程序。 有关详细信息，请参阅 [WinUSB ( # A0) 安装](winusb-installation.md)。

5. 获取有关设备的信息并查看其描述符。

    有关概念性信息，请参阅 [所有 USB 开发人员的概念](usb-concepts-for-all-developers.md)。 通过阅读配置描述符、每个受支持的备用设置的接口描述符及其终结点描述符，获取有关设备功能的信息。 有关详细信息，请参阅 [查询设备的 USB 描述符](using-winusb-api-to-communicate-with-a-usb-device.md#query)。

6. 发送 USB 控件传输。

    将标准控制请求和供应商命令发送到设备。 有关详细信息，请参阅 [将控制传输发送到默认终结点](using-winusb-api-to-communicate-with-a-usb-device.md#control)。

7. 发送批量或中断传输。

    对设备支持的大容量、中断和同步终结点执行读写操作。 有关详细信息，请参阅 [发出 I/o 请求](using-winusb-api-to-communicate-with-a-usb-device.md#io)。

8. 发送同步传输。

    发送同步读取和写入请求，主要用于流式传输数据。 此功能仅在 Windows 8.1 和更高版本上可用。 有关详细信息，请参阅 [从 WinUSB 桌面应用发送 USB 同步传输](getting-set-up-to-use-windows-devices-usb.md)。

## <a name="related-topics"></a>相关主题

[为 USB 设备开发 Windows 应用程序](developing-windows-applications-that-communicate-with-a-usb-device.md)  

[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
