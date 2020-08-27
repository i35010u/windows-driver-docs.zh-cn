---
description: 介绍 USB 函数堆栈的体系结构。
title: Windows 中的 USB 设备端驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92282939d13e0be925a1c622b7e535bb5fdd38ab
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969220"
---
# <a name="usb-device-side-drivers-in-windows"></a>Windows 中的 USB 设备端驱动程序


介绍 USB 函数堆栈的体系结构。




在 USB 设备上，当 ACPI (PDO) 创建 USB 设备物理设备对象时，USB 函数堆栈将引用由即插即用管理器枚举的一组驱动程序。

在单个配置设备中，USB 设备可定义一个或多个接口。 例如，媒体传输协议 (MTP) 将文件传输到设备和从设备传输文件。 复合 USB 设备在单个配置中可以支持多个接口。 USB 函数堆栈为每个接口创建 PDOs，而 PnP 管理器加载类驱动程序，该驱动程序将创建函数设备对象 (该接口的 FDO) 。

此图中对 USB 函数堆栈进行了概念：

![usb 函数堆栈](images/usb-fn.png)

**应用程序和服务**

- 所有用户模式请求都将发送到 Microsoft 提供的内核模式类驱动程序 GenericUSBFn.sys。 你可以创建与 GenericUSBFn.sys 通信的用户模式服务， (IOCTLs) 发送 i/o 控制代码，如 [genericusbfnioctl](https://docs.microsoft.com/windows/desktop/api/genericusbfnioctl/)中所定义。 有关这些 IOCTLs 的详细信息，请参阅 [与用户模式服务中的 GenericUSBFn.sys 通信](https://docs.microsoft.com/windows-hardware/drivers/usbcon/user-mode-services-ufx)

**USB 函数类驱动程序**

USB 函数类驱动程序实现 (或 USB 设备上) 组接口的功能。 MTP 和 IpOverUsb 是系统提供的类驱动程序的示例。 类驱动程序可以纯粹作为内核模式驱动程序来实现，也可以是与系统提供的类驱动程序 GenericUSBFn.sys 配对的用户模式服务。

函数类驱动程序通过使用 [USB 函数类驱动程序向 UFX 编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))发送请求。

**USB 函数类扩展 (UFX) **

USB 函数类扩展 (UFX) 是系统提供的针对 [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging) 的扩展 (KMDF) 。 USB 是标准总线，具有一些必需的功能和功能。 UFX 负责实现所有 USB 函数控制器通用的 USB 函数逻辑，并处理和/或分派来自 USB 函数类驱动程序的请求。 特别是，UFX 处理枚举设备和处理标准控制传输的过程。 若要执行这些操作，UFX 需要了解有关总线功能的信息。 在建立类扩展接口时，这些功能将报告给 UFX。

UFX 公开了标准 IOCTLs， (USB 函数类驱动程序和用户模式服务的上层) 可用于向控制器发送请求。 此外，UFX 还通知上层从主机收到的标准请求。

**USB 函数客户端驱动程序**

UFX 提供了一个统一的接口，该接口在不同的控制器之间保持一致。 但是，控制器具有不同的功能，但有一些限制，如终结点数、终结点类型、低功率、远程唤醒。 例如，某些控制器支持 DMA，而其他控制器则不支持。 一些控制器在硬件中实现流，而其他控制器则需要驱动程序处理流。 出于这些原因，仅在 UFX 中处理通用功能。 不同于控制器的传输、电源管理、流支持和其他功能均由客户端驱动程序处理。

USB 函数客户端驱动程序负责实现控制器特定的操作。 其中包括实现终结点数据传输、USB 设备状态更改 (重置、挂起、恢复) 、附加/分离检测、端口/充电器检测。 客户端驱动程序还负责处理电源管理和 PnP 事件。

函数客户端驱动程序通过使用[USB 函数类驱动程序 UFX 编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))，以[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging) (KMDF) 驱动程序的形式写入。

Microsoft 为 ChipIdea 和 Synopsys 控制器 ( # A0、Ufxsynopsys.sys) 提供内置的函数客户端驱动程序。

**USB 低筛选器驱动程序**

如果函数控制器使用机箱中的 Synopsys 和 ChipIdea 驱动程序，则 USB lower 筛选器驱动程序支持检测充电器。 筛选器驱动程序管理从 USB 端口检测开始的 USB 充电。 t 必须为其支持的每个充电器类型发布一个 GUID，以及该充电器属性的列表。 如果特定的充电器是可配置的，则较低的 USB 筛选器驱动程序会定义一个列表，其中列出了支持的 PropertyIDs 及其相应的值类型，可以将其发送到该列表来配置充电器。 驱动程序还会在电池堆栈开始充电时通知电池堆栈，并通知设备最大电流。 对于 Synopsys 和 ChipIdea 驱动程序以外的客户端驱动程序，可以在客户端驱动程序中实现充电逻辑。

函数类驱动程序使用 [用于支持专用充电器的编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))向 UFX 发送请求。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



