---
Description: This topic provides an overview of the Universal Serial Bus (USB) driver stack architecture.
title: 在 Windows 中的 USB 宿主端驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31e021cffe443cab922140fab6d5c5c32af6460d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543767"
---
# <a name="usb-host-side-drivers-in-windows"></a>在 Windows 中的 USB 宿主端驱动程序


本主题提供了通用串行总线 (USB) 驱动程序堆栈体系结构的概述。

下图显示 Windows 8 的 USB 驱动程序堆栈体系结构的框图。 在关系图显示了 USB 2.0 和 USB 3.0 的单独的 USB 驱动程序堆栈。 设备附加到 xHCI 控制器时，Windows 将加载 USB 3.0 驱动程序堆栈。 USB 3.0 堆栈是 Windows 8 中的新增功能。

Windows 将加载到 eHCI、 oHCI 或 uHCI 控制器附加设备的 USB 2.0 驱动程序堆栈。 在 Windows XP Service Pack 1 (SP1) 和更高版本的 Windows 操作系统中随附的 USB 2.0 驱动程序堆栈。

![usb 2.0 和 3.0 驱动程序堆栈的体系结构的框图](images/usb-driver-stack-3.png)

-   [USB 3.0 驱动程序堆栈](#usb-3-0-driver-stack)
    -   [USB 3.0 主机控制器驱动程序 (Usbxhci.sys)](#usb-3-0-host-controller-driver--usbxhci-sys)
    -   [USB 主机控制器扩展 (Ucx01000.sys)](#usb-host-controller-extension--ucx01000-sys)
    -   [USB 集线器驱动程序 (Usbhub3.sys)](#usb-hub-driver-usbhub3-sys)
-   [USB 2.0 驱动程序堆栈](#usb-2-0-driver-stack)
-   [USB 常见类泛型父驱动程序 (Usbccgp.sys)](#usb-common-class-generic-parent-driver--usbccgp-sys--)
-   [WinUSB (Winusb.sys)](#winusb-winusb-sys)
-   [USB 客户端驱动程序](#usb-client-driver)
-   [客户端驱动程序的帮助程序库](#helper-libraries-for-client-drivers)
-   [相关的主题](#related-topics)

## <a name="usb-30-driver-stack"></a>USB 3.0 驱动程序堆栈


USB 3.0 堆栈是 Windows 8 中的新增功能。 Microsoft 使用内核模式驱动程序框架 (KMDF) 接口来创建新的驱动程序。 KMDF 驱动程序模型可以降低复杂性并提高了稳定性。

### <a href="" id="usb-3-0-host-controller-driver--usbxhci-sys"></a>USB 3.0 主机控制器驱动程序 (Usbxhci.sys)

XHCI 驱动程序是 USB 3.0 主机控制器驱动程序。 XHCI 驱动程序的责任包括初始化 MMIO 寄存器和 xHCI 控制器硬件的主机基于内存的数据结构映射传输到传输请求的块，从较高层驱动程序请求和提交将请求发送到硬件。 完成后传输，驱动程序处理从硬件传输完成事件并将事件驱动程序堆栈中向上传播。 它还可以控制 xHCI 控制器设备槽和终结点上下文。

XHCI 驱动程序是 Windows 8 中的新增功能并不是扩展了早期版本的操作系统中提供的 eHCI 微型端口驱动程序。 新的驱动程序通过使用内核模式驱动程序框架 (KMDF) 接口编写，并为所有控制器电源管理和即插即用事件使用 KMDF。 Windows 加载 xHCI 驱动程序作为函数设备对象 (FDO) 在主控制器设备堆栈中。

### <a href="" id="-usb-host-controller-extension--ucx01000-sys--"></a> USB 主机控制器扩展 (Ucx01000.sys)

USB 主控制器扩展驱动程序 （KMDF 的扩展） 为基础的类特定于主机控制器驱动程序，如 xHCI 驱动程序的新扩展。 新的驱动程序是可扩展的旨在支持其他类型的预期在将来开发的主控制器驱动程序。 中心驱动程序的常见抽象的接口提供对主机控制器驱动程序，队列请求的通用机制和重写某些所选的函数用作 USB 主机控制器扩展。 所有 I/O 请求由上部的驱动程序覆盖范围都启动主机控制器扩展驱动程序之前 xHCI 驱动程序。 收到的 I/O 请求时，主机控制器扩展验证请求，然后将请求转发到与目标终结点关联的正确 KMDF 队列。 XHCI 驱动程序，当准备好进行处理，请求从队列中检索。 USB 主控制器扩展驱动程序的任务是：

-   提供到 xHCI 驱动程序的特定于 USB 的对象。
-   提供到 xHCI 驱动程序 KMDF 事件回调例程。
-   管理和控制与主机控制器相关联的根中心的操作。
-   客户端驱动程序，可配置的实现功能，如链接 MDLs、 流和等等。

### <a href="" id="usb-hub-driver-usbhub3-sys"></a>USB 集线器驱动程序 (Usbhub3.sys)

新的中心驱动程序，在 3.0 版的设备的 USB 驱动程序堆栈使用 KMDF 驱动程序模型。 中心驱动程序主要执行以下任务：

-   管理 USB 集线器和它们的端口。
-   枚举设备和其他连接到其下游端口的集线器。
-   创建枚举的设备和中心的物理设备对象 (PDOs)。

Windows 为中心的设备堆栈中 FDO 加载中心驱动程序。 通过一系列状态机实现了设备枚举和新的驱动程序中的中心管理。 中心驱动程序依赖 KMDF 电源管理和即插即用的函数。 除了中心管理的中心驱动程序还执行初步检查和发送 USB 客户端驱动程序层的某些请求的处理。 例如，中心驱动程序分析选择配置请求，以确定该请求将配置的终结点。 分析信息之后, 中心驱动程序提交到 USB 主机控制器扩展或进一步处理请求。

## <a name="usb-20-driver-stack"></a>USB 2.0 驱动程序堆栈


Windows 将加载到 eHCI、 oHCI 或 uHCI 控制器附加设备的 USB 2.0 驱动程序堆栈。 在 Windows XP SP1 和更高版本的 Windows 操作系统中提供的 USB 2.0 驱动程序堆栈中的驱动程序。 USB 2.0 驱动程序堆栈旨在提供高速 USB 设备方便 USB 2.0 规范中定义。

底部的 USB 驱动程序堆栈是主机控制器驱动程序。 它包括端口驱动程序、 Usbport.sys，和一个或多个同时运行的三个微型端口驱动程序。 当系统检测到主机控制器硬件时，它会加载一个微型端口驱动程序。 微型端口驱动程序，它加载后，将加载端口驱动程序，Usbport.sys。 端口驱动程序处理这些方面都独立于特定协议的主机控制器驱动程序的职责。

Usbuhci.sys （通用主机控制器接口） 微型端口驱动程序将替换为 Windows 2000 附带的 Uhcd.sys miniclass 驱动程序。 Usbohci.sys （打开主机控制器接口） 微型端口驱动程序将替换 Openhci.sys。 Usbehci.sys 微型端口驱动程序支持高速 USB 设备和 Windows XP SP1 和更高版本和 Windows Server 2003 和更高版本操作系统中引入了。

在所有版本的 Windows 支持 USB 2.0，操作系统是能够同时管理 USB 1.1 和 USB 2.0 主机控制器。 只要操作系统检测到控制器的两种类型都存在，它将创建两个单独的设备节点，一个用于每个主机控制器。 Windows 随后加载的 USB 2.0 兼容的主机控制器硬件和是 Usbohci.sys Usbehci.sys 微型端口驱动程序或 Openhci.sys USB 1.1 兼容硬件，具体取决于系统配置。

端口上方驱动程序是 USB 总线驱动程序 Usbhub.sys，也称为中心驱动程序。 这是在系统上每个中心的设备驱动程序。

## <a name="usb-common-class-generic-parent-driver-usbccgpsys"></a>USB 常见类泛型父驱动程序 (Usbccgp.sys)


USB 的常见类泛型父驱动程序是复合设备由 Microsoft 提供的父驱动程序。 中心驱动程序枚举和加载父复合驱动程序，如果**deviceClass**为 0 或 0xef 和**numInterfaces**大于 1 的设备描述符中。 中心驱动程序将生成为父复合驱动程序的兼容 ID"USB\\复合"。 Usbccgp.sys 使用 Windows 驱动程序模型 (WDM) 例程。

父复合驱动程序枚举复合设备中的所有函数，并创建每个 PDO。 这将导致相应的类或客户端驱动程序加载的设备中的每个函数。 每个函数驱动程序 （子 PDO） 将请求发送到父驱动程序，可以将其提交给 USB 集线器驱动程序。

Usbccgp.sys 随 Windows XP SP1 和更高版本的 Windows 操作系统。 在 Windows 8 中，已更新，该驱动程序以实现函数挂起和远程唤醒功能在 USB 3.0 规范中定义。

有关详细信息，请参阅[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)。

## <a name="winusb-winusbsys"></a>WinUSB (Winusb.sys)


Windows USB (WinUSB) 是适用于 USB 设备由 Microsoft 提供通用驱动程序。 WinUSB 体系结构由内核模式驱动程序 (Winusb.sys) 和用户模式动态链接库 (Winusb.dll) 组成。 对于不需要自定义功能驱动程序的设备，Winusb.sys 可以安装在设备的内核模式堆栈为功能驱动程序。 用户模式进程然后可以通过使用一系列设备 I/O 控制请求或调用与 Winusb.sys 通信**WinUsb\_Xxx**函数。 有关详细信息，请参阅[WinUSB](winusb.md)。

在 Windows 8 中，WinUSB，Winusb.inf，由 Microsoft 提供的信息 (INF) 文件包含 USB\\MS\_COMP\_WINUSB 作为设备标识符字符串。 这允许 Winusb.sys 作为具有匹配的 WinUSB 兼容 ID MS OS 描述符中的这些设备的函数驱动程序自动加载。 此类设备称为 WinUSB 设备。 硬件制造商不需要分发其 WinUSB 设备 INF 文件为最终用户简化驱动程序安装过程。 有关详细信息，请参阅[WinUSB 设备](automatic-installation-of-winusb.md)。

## <a name="usb-client-driver"></a>USB 客户端驱动程序


每个 USB 设备，复合或非组合键，由客户端驱动程序管理。 USB 客户端驱动程序是一个类或设备的驱动程序的客户端的 USB 驱动程序堆栈。 此类驱动程序包括类和特定于设备的驱动程序从 Microsoft 或第三方供应商。 若要查看由 Microsoft 提供的类驱动程序的列表，请参阅[支持 USB 设备类的驱动程序](supported-usb-classes.md)。 客户端驱动程序创建请求，以与设备通信通过调用公共接口公开的 USB 驱动程序堆栈。

复合设备的客户端驱动程序是与用于非复合设备，除了在驱动程序堆栈中的位置的客户端驱动程序没有什么不同。

非复合设备的客户端驱动程序直接上中心驱动程序进行分层。

对于复合的 USB 设备，用于公开多个函数并不具有父类驱动程序，Windows 将加载[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)中心驱动程序和客户端驱动程序层之间。 父驱动程序创建一个单独的 PDO 复合设备的每个函数。 在泛型父驱动程序加载客户端驱动程序 (FDOs 函数)。 供应商可以选择为每个函数提供单独的客户端驱动程序。

USB 客户端驱动程序可以运行在用户模式或内核模式，具体取决于驱动程序的要求。 可以通过使用 KMDF、 UMDF 或 WDM 例程编写 USB 客户端驱动程序。

## <a name="helper-libraries-for-client-drivers"></a>客户端驱动程序的帮助程序库


Microsoft 提供了以下的帮助程序库，以帮助内核模式驱动程序和应用程序与 USB 驱动程序堆栈进行通信：

-   Usbd.sys

    Microsoft 提供了导出的客户端的 USB 驱动程序例程的 Usbd.sys 库。 帮助器例程简化客户端驱动程序的操作任务。 例如，通过使用的帮助器例程，USB 客户端驱动程序可以建立[USB 请求块 (URBs)](communicating-with-a-usb-device.md)对于某些特定操作，如选择一个配置，并将提交这些 URBs 到 USB 驱动程序堆栈。

-   Usbdex.lib

    此帮助程序库是 Windows 8 的新增功能。 库导出主要用于分配和构建 URBs 例程。 这些例程替换一些旧例程由 Usbd.sys 导出。 新的例程需要客户端驱动程序注册到 USB 驱动程序堆栈，这会保存注册的句柄。 该句柄用于对其他 Usbdex.lib 例程的调用。 由新例程分配某些 URBs 具有更好地跟踪和处理的 USB 驱动程序使用 URB 上下文。 有关详细信息，请参阅[Allocating 和构建 URBs](how-to-add-xrb-support-for-client-drivers.md)。

-   Winusb.dll

    Winusb.dll 是公开的用户模式 DLL [WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)用于与 Winusb.sys 进行通信，这作为设备的功能在内核模式下的驱动程序中加载。 应用程序使用这些函数来配置设备，检索有关设备的信息和执行 I/O 操作。 有关使用这些函数的信息，请参阅[如何访问由使用 WinUSB 函数 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB) 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



