---
description: 用于通信和 CDC 控制设备的 Microsoft 提供的内置驱动程序 (Usbser.sys)。
title: USB 串行驱动程序 (Usbser.sys)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: cd4dfa2415eb29ee190867d718cb957b5f14add6
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648172"
---
# <a name="usb-serial-driver-usbsersys"></a>USB 串行驱动程序 (Usbser.sys)

## <a name="versions-supported"></a>支持的版本

- Windows 10
- Windows 8.1

## <a name="applies-to"></a>适用于

- CDC 控制设备的设备制造商

用于通信和 CDC 控制设备的 Microsoft 提供的内置驱动程序 (Usbser.sys)。

在 Windows 10 中，通过使用[内核模式驱动程序框架](../wdf/index.md)重写了驱动程序，从而提高了驱动程序的整体稳定性。

- 通过驱动程序改进了 PnP 和电源管理（例如处理意外删除）。
- 添加了电源管理功能，如 [USB 选择性挂起](usb-selective-suspend.md)。

此外，UWP 应用程序现在可以使用新的 [Windows.Devices.SerialCommunication](/uwp/api/Windows.Devices.SerialCommunication) 命名空间提供的 API，该命名空间允许应用与这些设备对话。

## <a name="usbsersys-installation"></a>Usbser.sys 安装

加载用于通信和 CDC 控制设备的 Microsoft 提供的内置驱动程序 (Usbser.sys)。

> [!NOTE]
> 如果你尝试安装 Windows 中包含的 USB 设备类驱动程序，则不需要下载该驱动程序。 它们将自动进行安装。 如果未自动安装，请与设备制造商联系。 有关包含在 Windows 中的 USB 设备类驱动程序的列表，请参见[包含在 Windows 中的 USB 设备类驱动程序](supported-usb-classes.md)。

### <a name="windows-10"></a>Windows 10

在 Windows 10 中，已将一个新的 INF (Usbser) 添加到 %Systemroot%\\Inf 中，该 Inf 将 Usbser.sys 作为设备堆栈中的函数设备对象 (FDO) 进行加载。 如果设备属于通信和 CDC 控制设备类，则会自动加载 Usbser.sys。无需编写自己的 INF 即可引用该驱动程序。 驱动程序是基于与[包含在 Windows 中的其他 USB 设备类驱动程序](supported-usb-classes.md)相似的兼容 ID 匹配来加载的。

`USB\Class_02`

`USB\Class_02&SubClass_02`

- 如果要自动加载 Usbser.sys，请在[设备描述符](usb-device-descriptors.md)中将类代码设置为 02，将子类代码设置为 02。 有关详细信息，请参阅 [USB 通信设备类](https://www.usb.org/document-library/class-definitions-communication-devices-12)。 使用此方法时，无需为设备分发 INF 文件，因为系统使用的是 Usbser.inf。
- 如果设备指定类代码 02，但子类代码值不是 02，则 Usbser.sys 不会自动加载。 Pnp 管理器尝试查找驱动程序。 如果找不到合适的驱动程序，则设备可能未加载驱动程序。 在这种情况下，你可能需要加载自己的驱动程序或编写引用另一个内置驱动程序的 INF。
- 如果你的设备将类和子类代码指定为 02，并且你想要加载另一个驱动程序而不是 Usbser.sys，则必须编写一个 INF，指定要安装的设备和驱动程序的硬件 ID。 例如，查看[示例驱动程序](../samples/universal-serial-bus--usb--driver-samples.md)中包含的 INF 文件，并查找与你的设备类似的设备。 有关 INF 部分的信息，请参阅 [INF 文件概述](../install/overview-of-inf-files.md)。

> [!NOTE]
> Microsoft 鼓励你尽可能使用内置驱动程序。 在 Windows 的移动版（如 Windows 10 Mobile）上，只会加载属于操作系统的驱动程序。 与桌面版不同，不能通过外部驱动程序包加载驱动程序。 使用新的内置 INF，如果在移动设备上检测到 USB 到串行设备，则会自动加载 Usbser.sys。

### <a name="windows-81-and-earlier-versions"></a>Windows 8.1 及更低版本

在 Windows 8.1 及更低版本的操作系统中，当 USB 到串行设备连接到计算机时，不会自动加载 Usbser.sys。 若要加载驱动程序，需要使用“包含”指令编写引用调制解调器 INF (mdmcpq.inf) 的 INF。 需要该指令，才能实例化服务、复制内置二进制文件和注册设备接口 GUID，应用程序需要此 GUID 来查找设备并与之通信。 该 INF 将“Usbser”指定为设备堆栈中较低的筛选器驱动程序。

INF 还需要将设备安装程序类指定为调制解调器才能使用 mdmcpq.INF。 在 INF 的 [Version] 部分下，指定“调制解调器”和设备类 GUID。 有关详细信息，请参阅[系统提供的设备安装程序类](../install/system-defined-device-setup-classes-reserved-for-system-use.md)。

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

有关详细信息，请参阅[如何从通用串行总线 (USB) 调制解调器 .inf 文件中使用或引用 Usbser.sys 驱动程序](/troubleshoot/windows-client/deployment/how-to-use-reference-usbser-driver-universal-serial-bus)。

## <a name="configure-selective-suspend-for-usbsersys"></a>为 Usbser.sys 配置选择性挂起

从 Windows 10 开始，Usbser.sys 支持 [USB 选择性挂起](usb-selective-suspend.md)。 它允许连接到串行设备的 USB 在不使用时进入低功耗状态，同时系统保持在 S0 状态。 当与设备的通信恢复时，设备可以由“挂起”状态恢复到“工作”状态。 此功能在默认情况下处于禁用状态，可以通过设置此注册表项下的“IdleUsbSelectiveSuspendPolicy”项来启用和配置：

```dotnetcli
HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB\\&lt;hardware id&gt;\\&lt;instance id&gt;\\Device Parameters
```

若要配置 Usbser.sys 的电源管理功能，可以将“IdleUsbSelectiveSuspendPolicy”设置为：

- “0x00000001”：空闲时（即，当没有活动数据传输到或从设备传输时）进入选择性挂起。

- “0x00000000”：仅当设备没有打开的句柄时才进入选择性挂起。

可以通过以下两种方式之一添加该条目：

- 编写一个引用安装 INF 的 INF，并在“HW.AddReg”部分添加注册表项。
- 在扩展属性 OS 功能描述符中描述该注册表项。 添加自定义属性，将“bPropertyName”字段设置为 Unicode 字符串“IdleUsbSelectiveSuspendPolicy”，将“wPropertyNameLength”设置为 62  。 将“bPropertyData”字段设置为“0x00000001”或“0x00000000”。 属性值存储为小字节序 32 位整数。

    有关详细信息，请参阅 [Microsoft OS 描述符](./microsoft-defined-usb-descriptors.md)。

## <a name="develop-windows-applications-for-a-usb-cdc-device"></a>为 USB CDC 设备开发 Windows 应用程序

如果为 USB CDC 设备安装 Usbser.sys，以下是应用程序编程模型选项：

- 从 Windows 10 开始，Windows 应用可以使用 [Windows.Devices.SerialCommunication](/uwp/api/Windows.Devices.SerialCommunication) 命名空间向 Usbser.sys 发送请求。 它定义了 Windows 运行时类，这些类可用于通过串行端口或某个串行端口抽象与 USB CDC 设备通信。 这些类提供了发现此类串行设备、读写数据和控制流控制的串行特定属性（如设置波特率、信号状态）的功能。

- 在 Windows 8.1 及更低版本中，你可以编写 Windows 桌面应用程序，使其打开虚拟 COM 端口并与设备通信。 有关详细信息，请参阅：

    Win32 编程模型：

  - [配置通信资源](/windows/desktop/DevIO/configuring-a-communications-resource)
  - [通信引用](/windows/desktop/DevIO/communications-reference)

    .NET framework 编程模型：

  - [System.IO.Ports Namespace](/dotnet/api/system.io.ports?redirectedfrom=MSDN)

## <a name="related-topics"></a>相关主题

[包含在 Windows 中的 USB 设备类驱动程序](supported-usb-classes.md)