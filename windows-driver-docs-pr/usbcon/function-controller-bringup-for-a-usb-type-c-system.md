---
Description: 函数控制器的驱动程序通知有关充电级别操作系统，其 USB C 型连接器支持，并在它可以开始收费和设备可以绘制当前的最长时通知电池子系统。
title: 在 USB 类型 C Windows 系统上启动功能控制器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 488ea8a90b8d46564e7351c001267271f719f854
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391558"
---
# <a name="bring-up-the-function-controller-on-a-usb-type-c-windows-system"></a>在 USB 类型 C Windows 系统上启动功能控制器


**摘要**

-   OEM 显示有 USB 类型 C 接口函数控制器的任务

**适用于**

-   Windows 10 移动版

**上次更新时间**

-   2015 年 11 月

**重要的 Api**

-   [USB 函数控制器客户端驱动程序编程参考](https://msdn.microsoft.com/library/windows/hardware/mt188010)
-   [支持专有充电器 USB 筛选器驱动程序](https://msdn.microsoft.com/library/windows/hardware/mt188012)

函数控制器的驱动程序通知有关充电级别操作系统，其 USB C 型连接器支持，并在它可以开始收费和设备可以绘制当前的最长时通知电池子系统。

本主题在任何给定时间假定函数控制器管理单个连接器 (UFP)。

## <a name="1-load-the-usb-device-side-drivers"></a>1.加载 USB 设备端驱动程序


有两个驱动程序管理函数控制器的操作。 对是由 Microsoft 提供的 USB 函数类扩展和其客户端驱动程序。 类扩展报告发送到操作系统的客户端驱动程序的信息。 客户端驱动程序与硬件通信，使用硬件接口。 查看，请[USB 设备端驱动程序在 Windows 中的](usb-device-side-drivers-in-windows.md)。

![usb 函数控制器驱动程序](images/function-controller.png)

-   如果您的系统使用 ChipIdea 和 Synopsys 控制器。
    1.  加载 Microsoft ChipIdea 和 Synopsys 控制器提供的框中客户端驱动程序。
    2.  编写较低的筛选器驱动程序，获取附加/分离充电器连接时的事件。 该驱动程序确定的充电器和配置属性的类型。 它还可以检测 USB 充电 BC1.2 规范定义的端口。 收费信息传递给此类扩展，以便它可以将其报告给充电仲裁驱动程序 (CAD.sys)。 有关详细信息，请参阅[USB 筛选器驱动程序支持专有充电器](https://msdn.microsoft.com/library/windows/hardware/mt188012)。
-   如果您的系统使用自定义控制器，编写客户端驱动程序。 BC1.2 检测逻辑在客户端驱动程序中实现。 有关详细信息，请参阅：

    [USB 函数控制器客户端驱动程序编程参考](https://msdn.microsoft.com/library/windows/hardware/mt188010)

    [开发，USB 函数控制器的 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)

## <a name="2-modify-system-acpi-to-indicate-to-the-function-controller-driver-that-the-connector-is-a-usb-type-c-connector"></a>2.修改系统 ACPI 函数控制器驱动程序向指示连接器是 USB 类型 C 连接器。


这是通过 ACPI 6.0 规范中定义的 ACPI 方法

`_UPC (USB Port Capabilities)`

ACPI 6.0 中定义的新值用于指示 USB C 型连接器，如"类型 C USB2"和"类型 C USB2 和与交换机 SS"的正确类型。 功能驱动程序，以便它使用特定于类型的 C-USB 仲裁逻辑来确定适当的充电源通信到 CAD.sys，此信息。

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



