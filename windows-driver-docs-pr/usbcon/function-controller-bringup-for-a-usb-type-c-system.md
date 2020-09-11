---
description: 函数控制器的驱动程序将通知操作系统其 USB 类型 C 连接器支持的收费级别，并在电池可能开始充电时通知电池子系统，并通知设备可以消耗的最大电流。
title: 在 USB 类型 C Windows 系统上启动功能控制器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ed6df1777dfa23434d86efa62f44e1311b6203f
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010423"
---
# <a name="bring-up-the-function-controller-on-a-usb-type-c-windows-system"></a>在 USB 类型 C Windows 系统上启动功能控制器


**摘要**

-   OEM 为具有 USB 类型 C 连接器的函数控制器启动任务

**适用于**

-   Windows 10 移动版

**上次更新时间**

-   2015 年 11 月

**重要的 API**

-   [USB 函数控制器客户端驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))
-   [用于支持专用充电器的 USB 筛选器驱动程序](/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))

函数控制器的驱动程序将通知操作系统其 USB 类型 C 连接器支持的收费级别，并在电池可能开始充电时通知电池子系统，并通知设备可以消耗的最大电流。

本主题假定函数控制器在任意给定时间 (UFP) 管理单个连接器。

## <a name="1-load-the-usb-device-side-drivers"></a>1. 加载 USB 设备端驱动程序


有两个驱动程序管理函数控制器的操作。 对是 Microsoft 提供的 USB 函数类扩展及其客户端驱动程序。 类扩展报告客户端驱动程序发送到操作系统的信息。 客户端驱动程序使用硬件接口与硬件通信。 请参阅 [Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)。

![usb 函数控制器驱动程序](images/function-controller.png)

-   如果系统使用的是 ChipIdea 和 Synopsys 控制器。
    1.  为 ChipIdea 和 Synopsys 控制器加载 Microsoft 提供的内置客户端驱动程序。
    2.  写入一个较低的筛选器驱动程序，该驱动程序在连接了充电器后获取附加/分离事件。 驱动程序确定充电器类型和配置属性。 它还可以检测 BC 1.2 规范定义的 USB 充电端口。 向类扩展传递收费信息，使其可以报告该信息以收取 ( # A0) 的仲裁驱动程序。 有关详细信息，请参阅 [支持专用充电器的 USB 筛选器驱动程序](/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))。
-   如果系统使用自定义控制器，请编写客户端驱动程序。 BC 1.2 检测逻辑是在客户端驱动程序中实现的。 有关详细信息，请参阅：

    [USB 函数控制器客户端驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))

    [为 USB 函数控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)

## <a name="2-modify-system-acpi-to-indicate-to-the-function-controller-driver-that-the-connector-is-a-usb-type-c-connector"></a>2. 修改系统 ACPI 以向函数控制器驱动程序指示连接器是 USB 类型 C 连接器。


这是通过 ACPI 6.0 规范中定义的 ACPI 方法完成的

`_UPC (USB Port Capabilities)`

使用 ACPI 6.0 中定义的新值指示正确类型的 USB 类型 C 连接器，如 "Type-C USB2" 和 "Type-C USB2 and SS with switch"。 函数驱动程序将此信息传递到 CAD.sys，以便它使用特定于 C 语言的仲裁逻辑来确定合适的收费来源。

```cpp
Device (UFN0)
{
    ...

    Name (_UPC, Package()
    {
        0x1,    // Connectable
        0x9,    // Type-C USB2 and Type-C USB2 and SS with switch
        0x0,    // Reserved
        0x0     // Reserved
    })

    Name (_CRS, ResourceTemplate()
    {
        ...
    })

    ...
```

## <a name="related-topics"></a>相关主题
[为 USB 类型 C 连接器开发 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)