---
Description: 用于通信和 CDC 控制设备的 Microsoft 提供的内置驱动程序（Usbser）。
title: USB 串行驱动程序 (Usbser.sys)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: a30e82bfce968f1e3168ed57444b7a79da6ac392
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007574"
---
# <a name="usb-serial-driver-usbsersys"></a>USB 串行驱动程序 (Usbser.sys)


**上次更新时间**

-   2015年4月

\* * OS 版本 * *

-   Windows 10
-   Windows 8.1

**适用于**

-   CDC 控制设备的设备制造商

用于通信和 CDC 控制设备的 Microsoft 提供的内置驱动程序（Usbser）。

在 Windows 10 中，驱动程序已通过使用[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)进行重写，以提高驱动程序的总体稳定性。

-   改善了驱动程序的 PnP 和电源管理（如处理意外删除）。
-   添加了电源管理功能，例如[USB 选择性挂起](usb-selective-suspend.md)。

此外，UWP 应用程序现在可以使用新的[**SerialCommunication**](https://docs.microsoft.com/uwp/api/Windows.Devices.SerialCommunication)命名空间提供的 api，使应用能够与这些设备通信。

## <a name="usbsersys-installation"></a>Usbser 安装


为通信和 CDC 控制设备加载 Microsoft 提供的内置驱动程序（Usbser）。

**请注意**@no__t 1If 你尝试安装 Windows 中包含的 USB 设备类驱动程序，则无需下载驱动程序。 它们将自动安装。 如果未自动安装，请与设备制造商联系。 有关 Windows 中包含的 USB 设备类驱动程序的列表，请参阅[windows 附带的 usb 设备类驱动程序](supported-usb-classes.md)。

 

**Windows 10**

在 Windows 10 中，已将一个新的 INF Usbser 添加到% Systemroot% \\Inf，它将 Usbser 作为函数设备对象（FDO）加载到设备堆栈中。 如果设备属于通信和 CDC 控制设备类，则会自动加载 Usbser。你无需编写自己的 INF 即可引用该驱动程序。 该驱动程序是基于与[Windows 中包含的其他 USB 设备类驱动程序](supported-usb-classes.md)匹配的兼容 ID。

`USB\Class_02`

`USB\Class_02&SubClass_02`

-   如果要自动加载 Usbser，请将类代码设置为02，并在[设备描述符](usb-device-descriptors.md)中将代码设置为02。 有关详细信息，请参阅[USB DWG 网站](https://go.microsoft.com/fwlink/p/?linkid=617741)上的 usb 通信设备类（或 usb CDC）规范。 使用此方法时，不需要为设备分发 INF 文件，因为系统使用的是 Usbser。
-   如果设备指定的是类代码02，而不是02以外的子类代码值，则 Usbser 不会自动加载。 Pnp 管理器尝试查找驱动程序。 如果找不到合适的驱动程序，则设备可能未加载驱动程序。 在这种情况下，你可能需要加载自己的驱动程序或编写引用另一个内置驱动程序的 INF。
-   如果你的设备将类和子类代码指定为02，并且你想要加载另一个驱动程序而不是 Usbser，则必须编写一个 INF 来指定要安装的设备的硬件 ID 和驱动程序。 有关示例，请查看[示例驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=534087)随附的 INF 文件，查找与设备类似的设备。 有关 INF 部分的信息，请参阅[Inf 文件概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)。

**请注意**  Microsoft 建议尽可能使用机箱内驱动程序。 在 Windows 移动版（如 Windows 10 移动版）上，只会加载作为操作系统一部分的驱动程序。 与桌面版不同，不能通过外部驱动程序包加载驱动程序。 使用新的内置 INF，如果在移动设备上检测到 USB 到串行设备，则会自动加载 Usbser。

 

**Windows 8.1 及更早版本**

在 Windows 8.1 和更早版本的操作系统中，当 USB 到串行设备连接到计算机时，不会自动加载 Usbser。 若要加载驱动程序，需要使用**Include**指令来编写引用调制解调器 inf （mdmcpq）的 INF。 需要指令来实例化服务、复制收件箱二进制文件和注册设备接口 GUID，应用程序需要这些 GUID 才能查找设备并与之通信。 该 INF 指定 "Usbser" 作为设备堆栈中的较低筛选器驱动程序。

INF 还需要将设备安装程序类指定为使用 mdmcpq 的**调制解调器**。 在 INF 的 [版本] 部分下，指定**调制解调器**和设备类 GUID。 有关详细信息，请参阅[系统提供的设备安装程序类](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))。

``` syntax
[DDInstall.NT]
include=mdmcpq.inf
CopyFiles=FakeModemCopyFileSection 

[DDInstall.NT.Services]
include=mdmcpq.inf
AddService=usbser, 0x00000000, LowerFilter_Service_Inst 

[DDInstall.NT.HW]
include=mdmcpq.inf
AddReg=LowerFilterAddReg
```

有关详细信息，请参阅[此知识库文章](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser-sys-driver-from-universal-serial/)。

## <a name="configure-selective-suspend-for-usbsersys"></a>配置 Usbser 的选择性挂起


从 Windows 10 开始，Usbser 支持[USB 选择性挂起](usb-selective-suspend.md)。 它允许连接的 USB 到串行设备进入低功耗状态（未使用时），而系统仍处于 S0 状态。 当与设备的通信恢复时，设备可能会退出挂起状态并恢复工作状态。 此功能在默认情况下处于禁用状态，可以通过设置此注册表项下的**IdleUsbSelectiveSuspendPolicy**项来启用和配置：

**HKEY @ no__t-1LOCAL @ no__t-2MACHINE @ no__t-3SYSTEM @ no__t-4CurrentControlSet @ no__t-5Enum @ no__t-6USB @ no__t-7 @ no__t-8hardware id @ no__t-9 @ no__t-10 @ no__t-11instance id @ no__t-12 @ no__t-13Device Parameters**

若要配置 Usbser 的电源管理功能，可以将**IdleUsbSelectiveSuspendPolicy**设置为：

-   0x00000001

    空闲时进入选择性挂起，即，当设备没有活动数据传输时。

-   0x00000000

    仅当设备没有打开的句柄时，才输入选择性挂起。

可以通过以下两种方式之一添加该条目：

-   写入一个 INF，引用安装 INF，并在 HW 中添加注册表项 **。AddReg**部分。
-   描述扩展属性 OS 功能描述符中的注册表项。 添加一个自定义属性部分，该部分将**bPropertyName**字段设置为 Unicode 字符串 "IdleUsbSelectiveSuspendPolicy"，将**wPropertyNameLength**设置为62字节。 将**bPropertyData**字段设置为 "0x00000001" 或 "0x00000000"。 属性值存储为小字节序32位整数。

    有关详细信息，请参阅[MICROSOFT OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=224878)。

## <a name="develop-windows-applications-for-a-usb-cdc-device"></a>为 USB CDC 设备开发 Windows 应用程序


如果为 USB CDC 设备安装 Usbser，以下是应用程序编程模型选项：

-   从 Windows 10 开始，Windows 应用可以使用[**SerialCommunication**](https://docs.microsoft.com/uwp/api/Windows.Devices.SerialCommunication)命名空间将请求发送到 Usbser。 它定义了 Windows 运行时类，这些类可用于通过串行端口或某些串行端口抽象来与 USB CDC 设备通信。 这些类提供了发现此类串行设备、读取和写入数据，以及控制流控制的串行特定属性（例如设置波特率、信号状态）的功能。

-   在 Windows 8.1 及更早版本中，你可以编写一个 Windows 桌面应用程序，用于打开虚拟 COM 端口并与设备通信。 有关详细信息，请参阅：

    Win32 编程模型：

    -   [配置通信资源](https://docs.microsoft.com/windows/desktop/DevIO/configuring-a-communications-resource)
    -   [通信引用](https://docs.microsoft.com/windows/desktop/DevIO/communications-reference)

    .NET framework 编程模型：

    -   [System.web 命名空间](https://docs.microsoft.com/dotnet/api/system.io.ports?redirectedfrom=MSDN)

## <a name="related-topics"></a>相关主题
[Windows 中包含的 USB 设备类驱动程序](supported-usb-classes.md)  
<!-- [How to use or to reference the Usbser.sys driver from universal serial bus (USB) modem .inf files](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser-sys-driver-from-universal-serial) -->



