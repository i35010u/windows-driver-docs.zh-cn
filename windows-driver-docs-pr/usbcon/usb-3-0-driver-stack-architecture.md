---
description: 本主题概述了通用串行总线 (USB) 驱动程序堆栈体系结构。
title: Windows 中的 USB 宿主端驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e318ba7e57bae782f7964bce7ab9f12f8745fd3
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010443"
---
# <a name="usb-host-side-drivers-in-windows"></a>Windows 中的 USB 宿主端驱动程序


本主题概述了通用串行总线 (USB) 驱动程序堆栈体系结构。

下图显示了适用于 Windows 8 的 USB 驱动程序堆栈的体系结构块关系图。 此图显示了适用于 USB 2.0 和 USB 3.0 的单独 USB 驱动程序堆栈。 当设备连接到 xHCI 控制器时，Windows 将加载 USB 3.0 驱动程序堆栈。 USB 3.0 堆栈是 Windows 8 中的新堆栈。

Windows 将为连接到 eHCI、oHCI 或 uHCI 控制器的设备加载 USB 2.0 驱动程序堆栈。 在 Windows XP Service Pack 1 (SP1) 和更高版本的 Windows 操作系统中附带了 USB 2.0 驱动程序堆栈。

![usb 2.0 和3.0 驱动程序堆栈的体系结构块示意图](images/usb-driver-stack-3.png)

-   [USB 3.0 驱动程序堆栈](#usb-30-driver-stack)
    -   [USB 3.0 主机控制器驱动程序 ( # A0) ](#usb-30-host-controller-driver-usbxhcisys)
    -   [USB 主机控制器扩展 ( # A0) ](#-usb-host-controller-extension-ucx01000sys)
    -   [USB 集线器驱动程序 ( # A0) ](#usb-hub-driver-usbhub3sys)
-   [USB 2.0 驱动程序堆栈](#usb-20-driver-stack)
-   [USB 公共类泛型父驱动程序 ( # A0) ](#usb-common-class-generic-parent-driver-usbccgpsys)
-   [WinUSB (Winusb.sys)](#winusb-winusbsys)
-   [USB 客户端驱动程序](#usb-client-driver)
-   [适用于客户端驱动程序的帮助程序库](#helper-libraries-for-client-drivers)
-   [相关主题](#related-topics)

## <a name="usb-30-driver-stack"></a>USB 3.0 驱动程序堆栈


USB 3.0 堆栈是 Windows 8 中的新堆栈。 Microsoft 使用内核模式驱动程序框架 (KMDF) 接口创建了新驱动程序。 KMDF 驱动程序模型降低了复杂性，并提高了稳定性。

### <a name="usb-30-host-controller-driver-usbxhcisys"></a><a href="" id="usb-30-host-controller-driver-usbxhcisys"></a>USB 3.0 主机控制器驱动程序 ( # A0) 

XHCI 驱动程序是 USB 3.0 主机控制器驱动程序。 XHCI 驱动程序的责任包括为 xHCI 控制器硬件初始化 MMIO 寄存器和基于主机内存的数据结构、将上层驱动程序的传输请求映射到传输请求块，以及向硬件提交请求。 完成传输后，驱动程序将处理来自硬件的传输完成事件，并在驱动程序堆栈上传播事件。 它还控制 xHCI 控制器设备槽和终结点上下文。

XHCI 驱动程序是 Windows 8 中的新增功能，并且不是早期版本的操作系统中可用的 eHCI 微型端口驱动程序的扩展。 新驱动程序通过使用内核模式驱动程序框架 (KMDF) 接口写入，并为所有控制器电源管理和 PnP 事件使用 KMDF。 Windows 将 xHCI 驱动程序加载为主机控制器的设备堆栈中 (FDO) 的函数设备对象。

### <a name="usb-host-controller-extension-ucx01000sys"></a><a href="" id="-usb-host-controller-extension-ucx01000sys"></a> USB 主机控制器扩展 ( # A0) 

USB 主机控制器扩展驱动程序 (扩展 KMDF) 是特定于基础类的主机控制器驱动程序（如 xHCI 驱动程序）的新扩展。 新的驱动程序是可扩展的，旨在支持将来开发的其他类型的主机控制器驱动程序。 USB 主机控制器扩展充当集线器驱动程序的通用抽象接口，提供一种通用机制，用于将请求排队到主机控制器驱动程序，并替代某些选定的函数。 由上层驱动程序启动的所有 i/o 请求都将在 xHCI 驱动程序之前到达主机控制器扩展驱动程序。 接收到 i/o 请求后，主机控制器扩展将验证请求，然后将请求转发到与目标终结点关联的正确的 KMDF 队列。 XHCI 驱动程序在准备好进行处理时，将从队列中检索请求。 USB 主机控制器扩展驱动程序的责任是：

-   向 xHCI 驱动程序提供 USB 特定的对象。
-   向 xHCI 驱动程序提供 KMDF 事件回调例程。
-   管理和控制与主机控制器关联的根集线器的操作。
-   实现可由客户端驱动程序（如链式 MDLs、流等）配置的功能。

### <a name="usb-hub-driver-usbhub3sys"></a><a href="" id="usb-hub-driver-usbhub3sys"></a>USB 集线器驱动程序 ( # A0) 

新的集线器驱动程序在3.0 设备的 USB 驱动程序堆栈中使用 KMDF 驱动程序模型。 集线器驱动程序主要执行以下任务：

-   管理 USB 集线器及其端口。
-   枚举附加到下游端口的设备和其他中心。
-   为枚举的设备和中心创建 (PDOs) 的物理设备对象。

Windows 将集线器驱动程序加载为中心设备堆栈中的 FDO。 新驱动程序中的设备枚举和中心管理通过一组状态机实现。 集线器驱动程序依赖于 KMDF 进行电源管理和 PnP 功能。 除集线器管理外，集线器驱动程序还会执行初步检查并处理 USB 客户端驱动程序层发送的某些请求。 例如，集线器驱动程序将分析一个选择配置请求，以确定请求将配置哪些终结点。 分析信息后，集线器驱动程序会将请求提交到 USB 主机控制器扩展或进一步处理。

## <a name="usb-20-driver-stack"></a>USB 2.0 驱动程序堆栈


Windows 将为连接到 eHCI、oHCI 或 uHCI 控制器的设备加载 USB 2.0 驱动程序堆栈。 USB 2.0 驱动程序堆栈中的驱动程序随附于 Windows XP SP1 和更高版本的 Windows 操作系统中。 USB 2.0 驱动程序堆栈旨在加速 USB 2.0 规范中定义的高速 USB 设备。

USB 驱动程序堆栈的底部是主机控制器驱动程序。 它包含端口驱动程序、Usbport.sys 以及同时运行的三个或多个小型端口驱动程序中的一个或多个。 当系统检测到主机控制器硬件时，它会加载其中一个微型端口驱动程序。 加载微型端口驱动程序后，会加载端口驱动程序，Usbport.sys。 端口驱动程序处理主机控制器驱动程序的与特定协议无关的职责。

Usbuhci.sys (通用主机控制器接口) 微型端口驱动程序替换了随 Windows 2000 提供的 Uhcd.sys miniclass 驱动程序。 Usbohci.sys (打开主机控制器接口) 微型端口驱动程序替换 Openhci.sys。 Usbehci.sys 微型端口驱动程序支持高速 USB 设备，并在 Windows XP SP1 和更高版本以及 Windows Server 2003 及更高版本的操作系统中引入。

在支持 USB 2.0 的所有 Windows 版本中，操作系统能够同时管理 USB 1.1 和 USB 2.0 主机控制器。 每当操作系统检测到两种类型的控制器都存在时，它将创建两个单独的设备节点，每个节点对应一个主机控制器。 Windows 随后会加载适用于 USB 2.0 兼容主机控制器硬件的 Usbehci.sys 微型端口驱动程序，并为与 USB 1.1 兼容的硬件 Usbohci.sys 或 Openhci.sys，具体取决于系统配置。

上述端口驱动程序为 USB 总线驱动程序，Usbhub.sys （也称为集线器驱动程序）。 这是系统中每个集线器的设备驱动程序。

## <a name="usb-common-class-generic-parent-driver-usbccgpsys"></a>USB 公共类泛型父驱动程序 ( # A0) 


USB 公共类通用父驱动程序是 Microsoft 提供的用于复合设备的父驱动程序。 如果 **deviceClass** 为0或0xef，且设备描述符中的 **numInterfaces** 大于1，则集线器驱动程序会枚举并加载父复合驱动程序。 集线器驱动程序生成父复合驱动程序的兼容 ID 作为 "USB \\ 复合"。 Usbccgp.sys 使用 Windows 驱动模型 (WDM) 例程。

父复合驱动程序枚举复合设备中的所有函数，并为每个函数创建一个 PDO。 这将导致为设备中的每个函数加载适当的类或客户端驱动程序。 每个功能驱动程序 (子 PDO) 将请求发送到父驱动程序，后者会将请求提交到 USB 集线器驱动程序。

Windows XP SP1 和更高版本的 Windows 操作系统中包含 Usbccgp.sys。 在 Windows 8 中，驱动程序已更新为可实现 "功能挂起" 和 "远程唤醒" 功能（如 USB 3.0 规范中所定义）。

有关详细信息，请参阅 [USB 通用父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md)。

## <a name="winusb-winusbsys"></a>WinUSB (Winusb.sys)


Windows USB (WinUSB) 是 Microsoft 提供的用于 USB 设备的通用驱动程序。 WinUSB 体系结构包含内核模式驱动程序 ( # A0) 和用户模式的动态链接库 ( # A1) 。 对于不需要自定义函数驱动程序的设备，Winusb.sys 可以作为函数驱动程序安装在设备的内核模式堆栈中。 然后，用户模式进程可以通过使用一组设备 i/o 控制请求或通过调用 **WinUsb \_ Xxx** 函数与 Winusb.sys 进行通信。 有关详细信息，请参阅 [WinUSB](winusb.md)。

在 Windows 8 中，Microsoft 提供的信息 (INF) file for WinUSB，Winusb，包含 USB \\ MS \_ COMP \_ WinUSB 作为设备标识符字符串。 这允许 Winusb.sys 自动加载为在 MS OS 描述符中具有匹配 WinUSB 兼容 ID 的设备的函数驱动程序。 此类设备称为 WinUSB 设备。 硬件制造商不需要为其 WinUSB 设备分发 INF 文件，因此，为最终用户简化驱动程序的安装过程。 有关详细信息，请参阅 [WinUSB 设备](automatic-installation-of-winusb.md)。

## <a name="usb-client-driver"></a>USB 客户端驱动程序


每个 USB 设备（复合或非复合）都由客户端驱动程序管理。 USB 客户端驱动程序是一种作为 USB 驱动程序堆栈的客户端的类或设备驱动程序。 此类驱动程序包括 Microsoft 或第三方供应商提供的类和设备特定驱动程序。 若要查看 Microsoft 提供的类驱动程序的列表，请参阅 [支持的 USB 设备类的驱动程序](supported-usb-classes.md)。 客户端驱动程序通过调用 USB 驱动程序堆栈公开的公共接口来创建与设备通信的请求。

复合设备的客户端驱动程序与非复合设备的客户端驱动程序没有区别，但其在驱动程序堆栈中的位置除外。

非复合设备的客户端驱动程序直接在集线器驱动程序的上方分层。

对于公开多个功能并且没有父类驱动程序的复合 USB 设备，Windows 将在集线器驱动程序和客户端驱动程序层之间加载 [USB 通用父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md) 。 父驱动程序为复合设备的每个函数创建一个单独的 PDO。 ) 的客户端驱动程序 (加载到泛型父驱动程序之上。 供应商可能会选择为每个功能提供单独的客户端驱动程序。

USB 客户端驱动程序可以在用户模式或内核模式下运行，具体取决于驱动程序的要求。 USB 客户端驱动程序可以通过使用 KMDF、UMDF 或 WDM 例程来编写。

## <a name="helper-libraries-for-client-drivers"></a>适用于客户端驱动程序的帮助程序库


Microsoft 提供了以下帮助程序库，用于帮助内核模式驱动程序和应用程序与 USB 驱动程序堆栈进行通信：

-   Usbd.sys

    Microsoft 提供了导出 USB 客户端驱动程序例程的 Usbd.sys 库。 帮助器例程简化了客户端驱动程序的操作任务。 例如，通过使用 helper 例程，USB 客户端驱动程序可以为某些特定操作（如选择配置） [ (URBs) 生成 Usb 请求块 ](communicating-with-a-usb-device.md) ，并将这些 URBs 提交到 USB 驱动程序堆栈。

-   Usbdex

    此帮助程序库是适用于 Windows 8 的新的。 库导出主要用于分配和生成 URBs。 这些例程将替换 Usbd.sys 导出的某些旧例程。 新例程要求客户端驱动程序注册到 USB 驱动程序堆栈，后者维护注册的句柄。 该句柄用于对其他 Usbdex 例程的调用。 新例程分配的某些 URBs 具有一个 URB 上下文，USB 驱动程序使用该上下文来更好地进行跟踪和处理。 有关详细信息，请参阅 [分配和生成 URBs](how-to-add-xrb-support-for-client-drivers.md)。

-   Winusb.dll

    Winusb.dll 是一种用户模式 DLL，该 DLL 公开用于与 Winusb.sys 通信的 [WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb) ，该函数作为内核模式下的设备功能驱动程序加载。 应用程序使用这些功能来配置设备、检索有关设备的信息以及执行 i/o 操作。 有关使用这些功能的信息，请参阅 [如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

## <a name="related-topics"></a>相关主题
[ (USB) 驱动程序的通用串行总线](../index.yml)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)