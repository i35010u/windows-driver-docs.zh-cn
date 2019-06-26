---
Description: 介绍 USB 函数堆栈的体系结构。
title: Windows 中的 USB 设备端驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58fabc40be1d6ca019b64572d71102730b647151
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380583"
---
# <a name="usb-device-side-drivers-in-windows"></a>Windows 中的 USB 设备端驱动程序


介绍 USB 函数堆栈的体系结构。




在 USB 设备，USB 函数堆栈表示的枚举由插管理器中，当 ACPI 创建 USB 设备的物理设备对象 (PDO) 的驱动程序的一组。

在单个配置设备的 USB 设备可以定义一个或多个接口。 例如，媒体传输协议 (MTP) 传输到和从设备的文件。 复合的 USB 设备可以支持多个接口中的单个配置。 USB 函数堆栈的每个接口创建 PDOs 和 PnP 管理器将创建该接口的函数设备对象 (FDO) 的类驱动程序加载。

在此图中，USB 函数堆栈进行概念化：

![usb 函数堆栈](images/usb-fn.png)

**应用程序和服务**

- 用户模式下的所有请求都发送到由 Microsoft 提供的内核模式类驱动程序 GenericUSBFn.sys。 您可以通过发送 I/O 控制代码 (Ioctl) 中定义与 GenericUSBFn.sys 创建进行通信的用户模式服务[genericusbfnioctl.h](https://docs.microsoft.com/windows/desktop/api/genericusbfnioctl/)。 有关这些 Ioctl 的详细信息请参阅[GenericUSBFn.sys 与从用户模式服务通信](https://docs.microsoft.com/windows-hardware/drivers/usbcon/user-mode-services-ufx)

**USB 函数类驱动程序**

USB 函数类驱动程序实现 USB 设备上的特定接口 （或的接口的组） 的功能。 MTP 和 IpOverUsb 是系统提供的类驱动程序的示例。 在类驱动程序可能实现完全作为内核模式驱动程序，也可能是用户模式服务与系统提供的类驱动程序 GenericUSBFn.sys 配对。

函数类驱动程序将请求发送到控制器，使用[USB 到 UFX 编程接口的函数类驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))。

**USB 函数类扩展 (UFX)**

USB 函数类扩展 (UFX) 是对系统提供的扩展[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)(KMDF)。 USB 是标准的总线和具有一些必需的功能和功能。 UFX 负责实现普遍适用于所有 USB 函数控制器的 USB 函数逻辑和处理和/或调度请求从 USB 函数类驱动程序。 具体而言，UFX 处理枚举设备和处理标准控制传输的过程。 若要执行这些操作，UFX 需要了解的有关总线的功能。 建立的类扩展接口时，这些功能被报告给 UFX。

UFX 公开标准 Ioctl 上层 （USB 函数类驱动程序和用户模式服务） 可用于将请求发送到控制器。 此外，UFX 通知有关标准请求收到来自主机的上层。

**USB 函数客户端驱动程序**

UFX 提供跨不同的控制器中一致地工作的抽象的接口。 但是，控制器有不同的功能，例如终结点的数目、 类型的终结点、 低功耗、 远程唤醒的限制。 例如，某些控制器都支持 DMA，而其他人则不能。 一些控制器的硬件中实现流，而其他控制器预期驱动程序来处理流。 出于这些原因，只有常用功能在 UFX 中处理。 传输、 电源管理、 流支持和其他功能会不同控制器控制器由客户端驱动程序处理。

USB 函数客户端驱动程序负责实施特定于控制器的操作。 其中包括实现终结点数据传输，USB 设备状态发生更改 （重置、 挂起、 恢复），附加/分离检测，端口/充电器检测。 客户端驱动程序还负责处理电源管理和即插即用事件。

功能的客户端驱动程序编写为[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)(KMDF) 驱动程序通过使用[USB 到 UFX 编程接口的函数类驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))。

Microsoft 为 ChipIdea 和 Synopsys 控制器提供内置函数 （UfxChipidea.sys，Ufxsynopsys.sys） 的客户端驱动程序。

**USB 较低的筛选器驱动程序**

USB 低筛选器驱动程序支持检测的充电器，如果函数控制器使用的现成 Synopsys 和 ChipIdea 驱动程序。 筛选器驱动程序管理 USB 充电从 USB 端口检测开始。 t 必须发布它支持每个充电器类型和该充电器属性的列表的 GUID。 如果可配置特定的充电器，较低的 USB 筛选器驱动程序定义受支持的属性 Id 可以发送给它，若要配置充电器及其相应值类型的列表。 它可以开始收费和当前的最长可以绘制设备时，驱动程序还会通知电池堆栈。 有关 Synopsys 以外的客户端驱动程序和 ChipIdea 驱动程序，收费逻辑可以实现在客户端驱动程序。

函数类驱动程序通过将请求发送到 UFX[编程接口支持专有充电器](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



