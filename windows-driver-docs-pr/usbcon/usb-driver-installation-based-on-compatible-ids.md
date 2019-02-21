---
Description: Microsoft-provided in-box driver (Usbser.sys) for your Communications and CDC Control device.
title: USB 串行驱动程序 (Usbser.sys)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff60502b51bf4e670f5d3e92c6044a6e338611d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540973"
---
# <a name="usb-serial-driver-usbsersys"></a>USB 串行驱动程序 (Usbser.sys)


**上次更新时间**

-   2015 年 4 月，

* * OS 版本 * *

-   Windows 10
-   Windows 8.1

**适用于**

-   CDC 控制设备的设备制造商

Microsoft 提供内置设备驱动程序 (Usbser.sys) 通信和 CDC 控制。

在 Windows 10 中，该驱动程序已重新编写通过使用[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)驱动程序的整体稳定性。

-   改进 （例如，处理意外删除） 的驱动程序 PnP 和电源管理。
-   如添加电源管理功能[USB 选择性挂起](usb-selective-suspend.md)。

此外，UWP 应用程序现在可以使用新提供的 Api [ **Windows.Devices.SerialCommunication** ](https://msdn.microsoft.com/library/windows/apps/dn921817)允许与这些设备的应用程序的命名空间。

## <a name="usbsersys-installation"></a>Usbser.sys 安装


加载由 Microsoft 提供现成的驱动程序 (Usbser.sys) 通信和 CDC 控制设备。

**请注意**  如果您尝试安装 USB 设备类驱动程序包含在 Windows 中，您不需要下载驱动程序。 它们将自动安装。 如果它们不会自动安装，请联系设备制造商。 USB 设备类驱动程序包含在 Windows 中的列表，请参阅[USB 设备类驱动程序包含在 Windows 中](supported-usb-classes.md)。

 

**Windows 10**

在 Windows 10 中，新 INF，Usbser.inf，已添加到 %systemroot%\\设备堆栈中的函数设备对象 (FDO) 加载 Usbser.sys Inf。 如果你的设备属于通信和 CDC 控制设备类，Usbser.sys 自动加载。不需要编写您自己来引用该驱动程序的 INF。 加载驱动程序根据兼容 ID 匹配项类似于[包含在 Windows 中其他 USB 设备类驱动程序](supported-usb-classes.md)。

`USB\Class_02`

`USB\Class_02&SubClass_02`

-   如果你想要自动加载 Usbser.sys，则将类代码到 02 和子类代码设置为在 02[设备描述符](usb-device-descriptors.md)。 有关详细信息，请参阅 USB 通信设备类 （或 USB CDC） 上找到规范[USB DWG 网站](https://go.microsoft.com/fwlink/p/?linkid=617741)。 使用此方法时，不需要分发你的设备的 INF 文件，因为系统将使用 Usbser.inf。
-   如果你的设备指定但 02 以外的子类代码值的类代码 02，Usbser.sys 不自动加载。 Pnp 管理器尝试查找驱动程序。 如果找不到适当的驱动程序，则设备可能没有加载的驱动程序。 在这种情况下，您可能需要加载您自己的驱动程序或编写引用另一个现成驱动程序 INF。
-   如果你的设备指定为 02、 类和子类代码并且你想要加载而不是 Usbser.sys 的另一个驱动程序，您必须编写指定的设备和驱动程序的硬件 ID 安装 INF。 有关示例，仔细查看附带的 INF 文件[示例驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=534087)和查找设备类似于你的设备。 INF 部分有关的信息，请参阅[概述的 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff549520)。

**请注意**  Microsoft 建议你将使用现成驱动程序，只要有可能。 移动版本的 Windows，如 Windows 10 移动版上加载只是操作系统的一部分的驱动程序。 与桌面版本中，不能加载驱动程序通过外部驱动程序包。 使用新的现成 INF 中，如果在移动设备上检测到 USB 到串行转换设备，则会自动加载 Usbser.sys。

 

**Windows 8.1 及更早版本**

在 Windows 8.1 和早期版本的操作系统，Usbser.sys 自动时不会加载 USB 到串行转换设备连接到计算机。 若要加载的驱动程序，需要编写使用引用调制解调器 INF (mdmcpq.inf) INF **Include**指令。 指令是实例化此服务，将收件箱二进制文件复制和注册设备接口的应用程序需要用来查找设备，与它交互的 GUID 所必需的。 该 INF 作为设备堆栈中较低的筛选器驱动程序指定"Usbser"。

此外需要指定设备安装程序类作为 INF**调制解调器**使用 mdmcpq.inf。 在 INF [Version] 部分中，指定**调制解调器**和设备类 GUID。 有关详细信息，请参阅[System-Supplied 设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)。

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

有关详细信息，请参阅[此知识库文章](https://support.microsoft.com/kb/837637/)。

## <a name="configure-selective-suspend-for-usbsersys"></a>配置选择性挂起针对 Usbser.sys


从 Windows 10 开始，支持 Usbser.sys [USB 选择性挂起](usb-selective-suspend.md)。 它允许连接的 USB 串行设备，进入低功耗状态在不使用，而系统仍然处于 S0 状态。 当与设备通信继续时，设备可以保持挂起状态，并恢复工作状态。 该功能默认处于禁用状态并可以启用和配置的设置**IdleUsbSelectiveSuspendPolicy**此注册表项下的条目：

**HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\枚举\\USB\\&lt;硬件 id&gt; \\ &lt;实例 id&gt;\\设备参数**

若要配置的 Usbser.sys 电源管理功能，可以设置**IdleUsbSelectiveSuspendPolicy**到：

-   "0x00000001"

    进入选择性挂起时空闲，也就是说，如果不有任何活动的数据传输到或从设备。

-   "0x00000000"

    进入选择性挂起仅当没有任何打开的句柄到设备时。

可以在两种方式之一中添加该条目：

-   编写引用安装 INF INF 和添加注册表项中的**硬件。AddReg**部分。
-   介绍了扩展的属性操作系统功能描述符中的注册表项。 添加自定义属性部分用于设置**bPropertyName**字段为 Unicode 字符串，"IdleUsbSelectiveSuspendPolicy"和**wPropertyNameLength**为 62 个字节。 设置**bPropertyData** "0x00000001"或"0x00000000"字段。 属性值存储为小字节序 32 位整数。

    有关详细信息，请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=224878)。

## <a name="develop-windows-applications-for-a-usb-cdc-device"></a>开发 USB CDC 设备的 Windows 应用程序


如果您安装 Usbser.sys for CDC USB 设备时，以下是应用程序的编程模型选项：

-   从 Windows 10 开始，Windows 应用程序可以使用发送请求到 Usbser.sys [ **Windows.Devices.SerialCommunication** ](https://msdn.microsoft.com/library/windows/apps/dn921817)命名空间。 它定义可用于与通过串行端口或串行端口的一些抽象 USB CDC 设备进行通信的 Windows 运行时类。 类提供功能来发现此类串行设备、 读取和写入数据，以及控制特定于序列的属性用于流控制，如设置波特率信号状态。

-   在 Windows 8.1 和早期版本中，可以编写的 Windows 桌面应用程序会打开一个虚拟 COM 端口和与设备通信。 有关详细信息，请参阅：

    Win32 编程模型：

    -   [配置通信资源](https://msdn.microsoft.com/library/windows/desktop/aa363201)
    -   [通信引用](https://msdn.microsoft.com/library/windows/desktop/aa363195)

    .NET framework 编程模型：

    -   [System.IO.Ports Namespace](https://msdn.microsoft.com/library/System.IO.Ports.aspx)

## <a name="related-topics"></a>相关主题
[包含在 Windows 中的 USB 设备类驱动程序](supported-usb-classes.md)  
<!-- [How to use or to reference the Usbser.sys driver from universal serial bus (USB) modem .inf files](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser.sys-driver-from-universal-serial-bus-usb-modem-.inf-files) -->



