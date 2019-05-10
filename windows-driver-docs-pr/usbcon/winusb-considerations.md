---
Description: 选择用于开发的 USB 客户端驱动程序，充当设备的功能驱动程序的最佳驱动程序模型的指导原则。
title: 选择用于开发的 USB 驱动程序的驱动程序模型
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: a548bff389696d1bb369e7d62c7851db6e1b23d3
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405295"
---
# <a name="choosing-a-driver-model-for-developing-a-usb-client-driver"></a>选择用于开发 USB 客户端驱动程序的驱动程序模型


本主题提供有关选择最佳的驱动程序模型开发的 USB 客户端驱动程序，充当设备的功能驱动程序的准则。

USB 设备制造商通常必须提供应用程序访问设备的功能的方法。 若要选择用于访问 USB 设备的最佳机制，开始最简单的方法，并仅当有必要将移到更复杂的解决方案。 以下列表总结了本主题中讨论的选项：

1.  如果你的设备属于 Windows 包括收件箱驱动程序的 USB 设备类，您不必编写驱动程序。
2.  如果你的设备不具有由 Microsoft 提供的类驱动程序，并且由单个应用程序访问该设备，然后加载 WinUSB 作为函数驱动程序。
3.  如果设备需要访问由并发应用程序，而你的设备未同步终结点，编写基于 UMDF 的客户端驱动程序。
4.  如果类驱动程序，WinUSB，或 UMDF 解决方案不起作用，选项编写 KMDF 基于客户端驱动程序。
5.  如果 KMDF 不支持特定功能，编写调用 WDM 例程的混合驱动程序。

最常用的方法是实现设备驱动程序 (称为*USB 客户端驱动程序*本文档中设置)，并提供一个安装包，为更高版本设备堆栈中的函数驱动程序将安装驱动程序提供 Microsoft USB 驱动程序堆栈。 客户端驱动程序公开的应用程序可用于获取设备的文件句柄的设备接口。 然后，应用程序可以使用此文件句柄与驱动程序通过调用 Windows Api 进行通信。

编写自定义驱动程序到设备的要求是最灵活的方式来提供对 USB 设备的访问。 但是，实现一个驱动程序需要大量工作。 该驱动程序必须执行复杂的任务，如驱动程序初始化新的设备时检测到，电源管理、 I/O 操作，在意外删除、 状态管理和清理时删除该设备。 选择要编写驱动程序之前，请提出以下问题：

-   [您可以使用由 Microsoft 提供的驱动程序？](#can-you-use-a-microsoft-provided-driver)
-   [如果您编写 USB 客户端驱动程序，哪些驱动程序模型是最佳的？](#if-you-write-a-usb-client-driver-which-driver-model-is-best)

## <a name="can-you-use-a-microsoft-provided-driver"></a>您可以使用由 Microsoft 提供的驱动程序？


您可能*不*需要编写驱动程序，如果：

-   你的设备属于受 Microsoft 的 USB 设备类。

    在这种情况下，作为设备驱动程序加载相应的类驱动程序。 Windows 包括收件箱驱动程序的设备类的列表，请参阅[USB 设备类驱动程序包含在 Windows 中](supported-usb-classes.md)。

-   你的设备不属于设备类。

    对于此类设备，计算结果确定是否可以加载 Microsoft 提供的设备功能[WinUSB](winusb.md) (Winusb.sys) 作为设备的功能驱动程序。 如果使用 WinUSB 是最佳的解决方案：

    -   通过单个应用程序可以访问你的设备。
    -   你的设备支持大容量、 中断或同步终结点。
    -   你的设备旨在使用运行 Windows XP Service Pack 2 (SP2) 和更高版本的 Windows 的目标计算机。

    正在加载 WinUSB 作为函数驱动程序提供了更简单的方法来实现自定义的 USB 驱动程序。 例如，WinUSB 是只能由与设备一起打包的应用程序访问电子气象站的首选的方法。 还有用于诊断与设备通信和闪烁的固件。

    若要使应用程序轻松地将请求发送到 Winusb.sys，我们提供的用户模式 DLL，Winusb.dll，公开[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)。 应用程序可以调用这些函数来访问设备、 其进行配置，并将数据传输到设备的终结点。

    如果 WinUSB 不是选项：

    -   通过多个应用程序可以访问你的设备。
    -   你的设备具有已有支持 Windows 操作系统中的内核模式下的功能。 例如，对于调制解调器函数 （它们 TAPI 支持） 或 LAN 函数 （它们支持 NDIS），必须使用 Usbser.sys 驱动程序来管理用户模式软件调制解调器设备所支持的接口。

    在 Windows 8 中，我们添加了新的兼容 ID 到 WinUSB 安装 INF。 如果设备固件中包含该兼容 ID，WinUSB 加载默认情况下为设备功能驱动程序。 这意味着硬件制造商不需要分发其 WinUSB 设备的 INF 文件。 有关详细信息，请参阅[WinUSB 设备](automatic-installation-of-winusb.md)。

## <a name="if-you-write-a-usb-client-driver-which-driver-model-is-best"></a>如果您编写 USB 客户端驱动程序，哪些驱动程序模型是最佳的？


答案取决于你的设备的设计。 首先，确定特定驱动程序模型是否满足需求。 是否希望 USB 设备由多个并发应用程序和流式处理通过同步终结点支持数据访问的基于一些设计注意事项。

如果您选择编写驱动程序，以下是你的选项：

-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)(UMDF)

    UMDF 提供客户端驱动程序可以使用与 Windows 组件，如插管理器和电源管理器集成的设备驱动程序接口 (DDIs)。 UMDF 还提供对 USB 设备，即在用户模式下的硬件的抽象并简化驱动程序的 I/O 操作的专用化的目标对象。 除了 UMDF 接口，WDF 提供增强的调试器扩展和跟踪工具对用户模式驱动程序。 UMDF 基于组件对象模型 (COM) 和开发的用户模式驱动程序是更轻松C++开发人员。

    在以下情况下实现 USB 设备的 UMDF 基于客户端驱动程序：

    -   设备是通过同时访问多个应用程序。
    -   设备支持大容量或中断传输。

    在用户模式下运行的驱动程序可以访问仅 （虚拟） 的用户地址空间，并会带来较低风险系统。 内核模式驱动程序可以访问的系统地址空间和内部系统结构。 错误编码的内核模式驱动程序可能会导致问题会影响其他驱动程序或系统，并最终导致计算机崩溃。 因此，用户模式驱动程序可以比在安全性和稳定性方面的内核模式驱动程序更安全。

    用户模式驱动程序的另一个优点是，他们会利用所有 Win32 Api。 例如，驱动程序可以调用 Api，如 Winsock、 压缩、 加密 Api 等。 这些 Api 不可用于内核模式驱动程序。

    UMDF 基于客户端驱动程序不支持同步终结点的 USB 设备的选项。

    **请注意**  Windows 8.1 引入了 UMDF 的 2.0 版本。 使用 UMDF 版本 2.0，您可以调用的许多方法可用于 KMDF 驱动程序的 C 编程语言中编写 UMDF 驱动程序。 不能使用 UMDF 版本 2.0 编写的 USB 的较低的筛选器驱动程序。

     

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)(KMDF)

    KMDF 旨在使驱动程序模型轻松地将扩展以支持新的硬件类型。 KMDF 提供 DDIs 和数据结构，使内核模式的 USB 驱动程序比早期版本的 Windows 驱动程序模型 (WDM) 驱动程序更容易实现。 此外，KMDF 还提供了可用于编写使用 Microsoft USB 驱动程序堆栈的完全正常运行的客户端驱动程序的专用的输入/输出 (I/O) 目标。

    在某些情况下，通过 KMDF 不公开特定的功能，该驱动程序必须调用 WDM 例程。 驱动程序不需要实现整个 WDM 基础结构，但使用 KMDF 方法来访问一组精选的 WDM 例程。 例如，若要执行同步传输，KMDF 基于客户端驱动程序可以发送 WDM 样式 URBs 描述对 USB 驱动程序堆栈的请求。 此类驱动程序被称为*混合驱动程序*本文档中设置。

    KMDF 还支持端口微型端口驱动程序模型。 例如，流式处理 （如 USB 网络摄像机） 的微型端口驱动程序在上边缘上使用流式处理的内核的内核可用于 KMDF USB I/O 目标对象将请求发送到 USB 驱动程序堆栈。 此外可以通过用于基于协议的总线如 USB KMDF 编写 NDIS 驱动程序。

    纯 WDM 驱动程序是难以编写、 复杂，且不可靠。 随着 KMDF 的发展，编写这种类型的驱动程序不再需要。

Microsoft Visual Studio 2012 包含**USB 用户模式驱动程序**并**USB 内核模式驱动程序**分别生成 UMDF 和 KMDF USB 客户端驱动程序，起始代码的模板。 模板代码初始化 USB 目标设备对象，以允许与硬件进行通信。 有关详细信息，请参阅下列主题：
-   [编写第一个 USB 客户端驱动程序 (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)
-   [编写第一个 USB 客户端驱动程序 (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)

有关如何实现 UMDF 和 KMDF 驱动程序的信息，请参阅 Microsoft Press 书籍*使用 Windows Driver Foundation 开发驱动程序*。

## <a name="winusb-umdf-kmdf-feature-comparison"></a>WinUSB，UMDF，KMDF 功能比较


下表总结了 WinUSB、 基于 UMDF 的 USB 驱动程序和基于 KMDF 的 USB 驱动程序的功能。

| 功能                                                                                                          | WinUSB | UMDF | KMDF |
|------------------------------------------------------------------------------------------------------------------|--------|------|------|
| 支持多个并发应用程序                                                                        | 否     | 是  | 是  |
| 隔离应用程序地址空间中的驱动程序地址空间                                                     | 否     | 是  | 否   |
| 支持大容量、 中断，并控制传输                                                                  | 是    | 是  | 是  |
| 支持同步传输                                                                                   | 是 ⁴  | 否   | 是  |
| 支持作为基础层 USB 堆栈上的内核模式驱动程序，例如筛选器驱动程序安装 | 否     | 否   | 是  |
| 支持选择性暂停并等待/唤醒状态                                                               | 是    | 是  | 是  |

 

下表总结了由不同版本的 Windows 支持的 WDF 选项。

| Windows 版本        | WinUSB | UMDF | KMDF |
|------------------------|--------|------|------|
| Windows 8              | 是    | 是  | 是  |
| Windows 7              | 是    | 是  | 是  |
| Windows Vista          | Yes¹   | Yes¹ | 是  |
| Windows Server 2003    | 否     | 否   | 是  |
| Windows XP             | Yes²   | Yes² | 是  |
| Microsoft Windows 2000 | 否     | 否   | Yes³ |

 

**请注意**   Yes¹:只能在基于 x86 和基于 x64 的版本的 Windows 上支持 WinUSB 和 UMDF。

Yes²:在 Windows XP Service Pack 2 (SP2) 或更高版本的 Windows 中支持 WINUSB 和 UMDF。

Yes³:在 Windows 2000 SP4 或更高版本的 Windows 中支持 KMDF。

Yes⁴:Windows 8.1 或更高版本的 Windows 中支持同步传输。

 

32 位版本的 Windows XP SP2support WinUSB 的所有客户端 Sku。 WinUSB 不是本机转到 Windows XP;它必须与 WinUSB 共同安装程序安装。 所有 Windows Vista Sku 和更高版本的 Windows 都支持 WinUSB。

## <a name="related-topics"></a>相关主题
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  
[WinUSB](winusb.md)  
[编写第一个 USB 客户端驱动程序 (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)  
[编写第一个 USB 客户端驱动程序 (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)  



