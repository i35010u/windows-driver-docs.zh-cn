---
description: 用于开发作为设备功能驱动程序的 USB 客户端驱动程序的最佳驱动程序模型的准则。
title: 选择用于开发 USB 驱动程序的驱动程序型号
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1491e059a738fc3d3dd4badaa79f3f8e693b8cb7
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010419"
---
# <a name="choosing-a-driver-model-for-developing-a-usb-client-driver"></a>选择用于开发 USB 客户端驱动程序的驱动程序模型


本主题提供有关为开发作为设备功能驱动程序的 USB 客户端驱动程序选择最佳驱动程序模型的准则。

USB 设备制造商通常必须为应用程序提供访问设备功能的方式。 若要选择访问 USB 设备的最佳机制，请从最简单的方法开始，仅在必要时才转到更复杂的解决方案。 下面的列表总结了本主题中讨论的选项：

1.  如果设备属于 Windows 包含收件箱驱动程序的 USB 设备类，则无需编写驱动程序。
2.  如果你的设备没有 Microsoft 提供的类驱动程序，并且通过单个应用程序访问设备，则将 WinUSB 作为函数驱动程序进行加载。
3.  如果设备需要由并发应用程序访问，而您的设备没有同步终结点，请编写一个基于 UMDF 的客户端驱动程序。
4.  如果类驱动程序、WinUSB 或 UMDF 解决方案并非适用于你的选项，请编写基于 KMDF 的客户端驱动程序。
5.  如果 KMDF 不支持某个特定功能，请编写调用 WDM 例程的混合驱动程序。

最常见的方法是实现设备驱动程序， (称为此文档集中的 *USB 客户端驱动程序* ，) 并提供安装包，该安装包将驱动程序作为功能驱动程序安装在 Microsoft 提供的 USB 驱动程序堆栈上方的设备堆栈中。 客户端驱动程序公开一个设备接口，应用程序可以使用该接口来获取设备的文件句柄。 然后，应用程序可以通过调用 Windows Api，使用此文件句柄与驱动程序通信。

编写自定义为设备要求的驱动程序是提供对 USB 设备的访问权限的最灵活的方法。 但是，实现驱动程序需要很多工作。 驱动程序必须执行复杂的任务，如检测到新设备时的驱动程序初始化、电源管理、i/o 操作、意外删除、状态管理以及删除设备时的清理。 在选择编写驱动程序之前，请询问以下问题：

-   [您可以使用 Microsoft 提供的驱动程序吗？](#can-you-use-a-microsoft-provided-driver)
-   [如果你编写了一个 USB 客户端驱动程序，最好哪个驱动程序型号？](#if-you-write-a-usb-client-driver-which-driver-model-is-best)

## <a name="can-you-use-a-microsoft-provided-driver"></a>您可以使用 Microsoft 提供的驱动程序吗？


如果需要，你可能 *不* 需要编写驱动程序：

-   你的设备属于 Microsoft 支持的 USB 设备类别。

    在这种情况下，相应的类驱动程序将加载为设备驱动程序。 有关 Windows 包含其收件箱驱动程序的设备类的列表，请参阅 [windows 附带的 USB 设备类驱动程序](supported-usb-classes.md)。

-   你的设备不属于设备类别。

    对于此类设备，请评估设备功能，以确定是否可以加载 Microsoft 提供的 [WinUSB](winusb.md) ( # A0) 作为设备的函数驱动程序。 在以下情况中，使用 WinUSB 是最佳解决方案：

    -   你的设备由单个应用程序访问。
    -   设备支持大容量、中断或同步终结点。
    -   设备旨在与运行 Windows XP Service Pack 2 (SP2) 和更高版本的 Windows 的目标计算机一起使用。

    将 WinUSB 作为函数驱动程序加载提供了一种更简单的方法来实现自定义 USB 驱动程序。 例如，WinUSB 是电子天气工作站的首选方法，只由与设备一起打包的应用程序访问。 它还可用于诊断与设备和闪存固件的通信。

    为了使应用程序能够轻松地将请求发送到 Winusb.sys，我们提供了一个公开 [WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)的用户模式 DLL Winusb.dll。 应用程序可调用这些函数来访问设备、对其进行配置，以及将数据传输到设备的终结点。

    如果出现以下情况，则不能选择 WinUSB：

    -   你的设备由多个应用程序访问。
    -   你的设备具有 Windows 操作系统中已经有内核模式支持的功能。 例如，对于调制解调器功能 (哪个 TAPI 支持) 或 LAN 功能 (NDIS 支持) ，则必须使用 Usbser.sys 驱动程序支持的接口来管理具有用户模式软件的调制解调器设备。

    在 Windows 8 中，我们已将一个新的兼容 ID 添加到 WinUSB 安装的 INF。 如果设备固件包含该兼容 ID，则默认情况下会加载 WinUSB 作为设备的函数驱动程序。 这意味着，硬件制造商不需要为其 WinUSB 设备分发 INF 文件。 有关详细信息，请参阅 [WinUSB 设备](automatic-installation-of-winusb.md)。

## <a name="if-you-write-a-usb-client-driver-which-driver-model-is-best"></a>如果你编写了一个 USB 客户端驱动程序，最好哪个驱动程序型号？


答案取决于设备的设计。 首先，确定特定的驱动程序型号是否满足您的要求。 某些设计注意事项取决于你是否希望多个并发应用程序访问 USB 设备，并支持通过同步终结点流式传输数据。

如果选择编写驱动程序，可选择以下选项：

-   [用户模式驱动程序框架](../wdf/index.md) (UMDF) 

    UMDF 提供 (DDIs) 的设备驱动程序接口，客户端驱动程序可以使用该接口与即插即用 Manager 和电源管理器等 Windows 组件进行集成。 UMDF 还为 USB 设备提供专用目标对象，这些对象在用户模式下抽象硬件，并简化驱动程序的 i/o 操作。 除了 UMDF 接口，WDF 还为用户模式驱动程序提供增强的调试器扩展和跟踪工具。 UMDF 基于组件对象模型 (COM) ，开发用户模式驱动程序对于 c + + 开发人员来说更为简单。

    在以下情况下，为 USB 设备实现基于 UMDF 的客户端驱动程序：

    -   该设备由多个应用程序同时访问。
    -   设备支持批量或中断传输。

    在用户模式下运行的驱动程序只能访问 (虚拟) 用户地址空间，并对系统造成很大的风险。 内核模式驱动程序可以访问系统地址空间和内部系统结构。 错误编码的内核模式驱动程序可能会导致影响其他驱动程序或系统的问题，并最终导致计算机崩溃。 因此，用户模式驱动程序在安全性和稳定性方面比内核模式驱动程序更安全。

    用户模式驱动程序的另一个优点是它们利用了所有的 Win32 Api。 例如，驱动程序可以调用 Winsock、压缩、加密 Api 等 Api。 这些 Api 不可用于内核模式驱动程序。

    如果 USB 设备支持同步终结点，则不能选择基于 UMDF 的客户端驱动程序。

    **注意**   Windows 8.1 引入了版本2.0 的 UMDF。 使用 UMDF 版本2.0，你可以使用 C 编程语言编写一个 UMDF 驱动程序，该驱动程序调用可用于 KMDF 驱动程序的多种方法。 不能使用 UMDF 版本2.0 来写入适用于 USB 的较低筛选器驱动程序。

     

-   [内核模式驱动程序框架](../wdf/index.md) (KMDF) 

    KMDF 旨在使驱动程序模型易于扩展，以支持新类型的硬件。 KMDF 提供 DDIs 和数据结构，使内核模式 USB 驱动程序比早期 Windows 驱动模型 (WDM) 驱动程序更容易实现。 此外，KMDF 还提供专用的输入/输出 (i/o) 目标，可用于编写使用 Microsoft USB 驱动程序堆栈的功能完备的客户端驱动程序。

    在某些情况下，如果某个特定功能未通过 KMDF 公开，则驱动程序必须调用 WDM 例程。 驱动程序无需实现整个 WDM 基础结构，而是使用 KMDF 方法访问一组选择的 WDM 例程。 例如，若要执行同步传输，基于 KMDF 的客户端驱动程序可以将描述请求的 WDM 样式 URBs 发送到 USB 驱动程序堆栈。 此类驱动程序在此文档集中称为 *混合驱动程序* 。

    KMDF 还支持端口-微型端口驱动程序模型。 例如，内核流式处理微型端口驱动程序 (例如，在上边缘使用内核流式处理的 USB 网络摄像机) 可以使用 KMDF USB i/o 目标对象将请求发送到 USB 驱动程序堆栈。 此外，还可以使用 KMDF 为基于协议的总线（如 USB）编写 NDIS 驱动程序。

    纯粹的 WDM 驱动程序难以编写、复杂且不可靠。 随着 KMDF 的发展，不再需要编写这种类型的驱动程序。

Microsoft Visual Studio 2012 包括 **Usb 用户模式驱动程序** 和 **Usb 内核模式驱动程序** 模板，分别为 UMDF 和 KMDF USB 客户端驱动程序生成起始代码。 模板代码初始化 USB 目标设备对象，以启用与硬件的通信。 有关详情，请参阅以下主题：
-   [将第一个 USB 客户端驱动程序写入 (UMDF) ](implement-driver-entry-for-a-usb-driver--umdf-.md)
-   [ (KMDF 中写入第一个 USB 客户端驱动程序) ](tutorial--write-your-first-usb-client-driver--kmdf-.md)

有关如何实现 UMDF 和 KMDF 驱动程序的信息，请参阅 Microsoft 新闻簿 *通过 Windows Driver Foundation 开发驱动程序*。

## <a name="winusb-umdf-kmdf-feature-comparison"></a>WinUSB、UMDF、KMDF 功能比较


下表总结了基于 WinUSB 的 USB 驱动程序和基于 KMDF 的 USB 驱动程序的功能。

| 特性                                                                                                          | WinUSB | UMDF | KMDF |
|------------------------------------------------------------------------------------------------------------------|--------|------|------|
| 支持多个并发应用程序                                                                        | 否     | 是  | 是  |
| 隔离应用程序地址空间中的驱动程序地址空间                                                     | 否     | 是  | 否   |
| 支持大容量、中断和控制传输                                                                  | 是    | 是  | 是  |
| 支持同步传输                                                                                   | 是⁴  | 否   | 是  |
| 支持将内核模式驱动程序（例如筛选器驱动程序）安装为 USB 堆栈上的覆盖层 | 否     | 否   | 是  |
| 支持选择性挂起和等待/唤醒状态                                                               | 是    | 是  | 是  |

 

下表汇总了不同版本的 Windows 支持的 WDF 选项。

| Windows 版本        | WinUSB | UMDF | KMDF |
|------------------------|--------|------|------|
| Windows 8              | 是    | 是  | 是  |
| Windows 7              | 是    | 是  | 是  |
| Windows Vista          | 是¹   | 是¹ | 是  |
| Windows Server 2003    | 否     | 否   | 是  |
| Windows XP             | 是²   | 是² | 是  |
| Microsoft Windows 2000 | 否     | 否   | 是³ |

 

**注意**   是¹：仅在基于 x86 和 x64 的 Windows 版本上支持 WinUSB 和 UMDF。

是²： Windows XP Service Pack 2 (SP2) 或更高版本的 Windows 支持 WINUSB 和 UMDF。

是³：在 Windows 2000 中支持 SP4 或更高版本的 Windows。

是⁴： Windows 8.1 或更高版本的 Windows 中支持同步传输。

 

32位版本的 Windows XP with SP2support WinUSB 的所有客户端 Sku。 WinUSB 不是 Windows XP 的本机的;它必须与 WinUSB 共同安装程序一起安装。 所有 Windows Vista Sku 以及 Windows 的更高版本都支持 WinUSB。

## <a name="related-topics"></a>相关主题
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  
[WinUSB](winusb.md)  
[将第一个 USB 客户端驱动程序写入 (UMDF) ](implement-driver-entry-for-a-usb-driver--umdf-.md)  
[ (KMDF 中写入第一个 USB 客户端驱动程序) ](tutorial--write-your-first-usb-client-driver--kmdf-.md)