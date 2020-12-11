---
title: ACPI 按钮设备
description: 通用按钮设备是一个标准设备，用于通过硬件中断报告按钮事件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 501aaa2e36797b2b2ba9710234cacaca7eefe947
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091116"
---
# <a name="acpi-button-device"></a>ACPI 按钮设备

通用按钮设备是一种标准设备，用于通过硬件中断报告按钮事件，并将这些中断映射到在人体学接口设备 (HID) 规范中定义的特定使用情况。

若要将按钮的功能表达给操作系统，需要两条信息：

- HID 控件的用法
- 控件所属的 HID 集合的使用情况

用法是使用页面和使用 ID 的组合。 例如，"音量向上" 按钮被标识为 " (使用量" 页上的 "使用情况 Id 0xE9)  (使用情况页0x0C，用法 Id 0x01) 中的" 使用情况 Id "页。

通用按钮设备的 ACPI 设备 Id 为 ACPI0011。 Windows 将加载 Microsoft 提供的内置驱动程序，Hidinterrupt.sys 设备。

有关通用按钮设备的详细信息，请访问 [统一可扩展固件接口](https://uefi.org/specifications) 规范网站，并下载 *ACPI 规范6.0 版* PDF 文档。 然后，使用左侧窗格导航到 **9.19 节**。

## <a name="sample-acpi-button-device-for-windows-10-core-os-editions"></a>适用于 Windows 10 核心操作系统版本的 ACPI 按钮设备示例 

描述用于运行 Windows 10 Core 操作系统的设备的 ACPI 中的按钮的示例。

```console
// Sample Buttons in ACPI for Windows 10.

Device(BTNS)
{
    Name(_HID, "ACPI0011")
    Name(_CRS, ResourceTemplate() {
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 0: Power Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 1: Volume Up Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 2: Volume Down Button
        GpioInt(Edge, ActiveHigh,...) {pin} // Index 3: Camera Auto-focus Button
        GpioInt(Edge, ActiveLow,...)  {pin} // Index 4: Camera Shutter Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 5: Back Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 6: Windows/Home Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 7: Search Button
    })
    Name(_DSD, Package(2) {
        //UUID for HID Button Descriptors:
        ToUUID("FA6BD625-9CE8-470D-A2C7-B3CA36C4282E"),
        //Data structure for this UUID:
        Package(9) {
            Package(5) {
                0,    // This is a Collection
                1,    // Unique ID for this Collection
                0,    // This is a Top-Level Collection
                0x01, // Usage Page ("Generic Desktop Page")
                0x0D  // Usage ("Portable Device Control")
            },
            Package(5) {
                1,    // This is a Control
                0,    // Interrupt index in _CRS for Power Button
                1,    // Unique ID of Parent Collection
                0x01, // Usage Page ("Generic Desktop Page")
                0x81  // Usage ("System Power Down")
            },
            Package(5) {
                1,    // This is a Control
                1,    // Interrupt index in _CRS for Volume Up Button
                1,    // Unique ID of Parent Collection
                0x0C, // Usage Page ("Consumer Page")
                0xE9  // Usage ("Volume Increment")
            },
            Package(5) {
                1,    // This is a Control
                2,    // Interrupt index in _CRS for Volume Down Button
                1,    // Unique ID of Parent Collection
                0x0C, // Usage Page ("Consumer Page")
                0xEA  // Usage ("Volume Decrement")
            },
            Package(5) {
                1,    // This is a Control
                3,    // Interrupt index in _CRS for Camera Auto-focus Button
                1,    // Unique ID of Parent Collection
                0x90, // Usage Page ("Camera Control Page")
                0x20  // Usage ("Camera Auto-focus")
            },
            Package(5) {
                1,    // This is a Control
                4,    // Interrupt index in _CRS for Camera Shutter Button
                1,    // Unique ID of Parent Collection
                0x90, // Usage Page ("Camera Control Page")
                0x21  // Usage ("Camera Shutter")
            },
            Package(5) {
                1,    // This is a Control
                5,    // Interrupt index in _CRS for Back Button
                1,    // Unique ID of Parent Collection
                0x0C, // Usage Page ("Consumer Page")
                0x224 // Usage ("AC Back")
            },
            Package(5) {
                1,    // This is a Control
                6,    // Interrupt index in _CRS for Windows/Home Button
                1,    // Unique ID of Parent Collection
                0x07, // Usage Page ("Keyboard Page")
                0xE3  // Usage ("Keyboard Left GUI")
            },
            Package(5) {
                1,    // This is a Control
                7,    // Interrupt index in _CRS for Search Button
                1,    // Unique ID of Parent Collection
                0x0C, // Usage Page ("Consumer Page")
                0x221 // Usage ("AC Search")
            }
        }
    })
}
```

## <a name="sample-buttons-in-acpi-for-device-running-windows-10-desktop-editions"></a>运行 Windows 10 桌面版的设备的 ACPI 中的示例按钮。

用于描述运行 Windows 10 桌面版的设备的 ACPI 中的按钮的示例 (Home、Pro、Enterprise 和教育) 。

```console
Device(BTNS)
{
    Name(_HID, "ACPI0011")
    Name(_CRS, ResourceTemplate() {
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 0: Power Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 1: Volume Up Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 2: Volume Down Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 3: Windows/Home Button
        GpioInt(Edge, ActiveBoth,...) {pin} // Index 4: Rotation Lock Button
    })
    Name(_DSD, Package(2) {
        //UUID for HID Button Descriptors:
        ToUUID("FA6BD625-9CE8-470D-A2C7-B3CA36C4282E"),
        //Data structure for this UUID:
        Package(6) {
            Package(5) {
                0,    // This is a Collection
                1,    // Unique ID for this Collection
                0,    // This is a Top-Level Collection
                0x01, // Usage Page ("Generic Desktop Page")
                0x0D  // Usage ("Portable Device Control")
            },
            Package(5) {
                1,    // This is a Control
                0,    // Interrupt index in _CRS for Power Button
                1,    // Unique ID of Parent Collection
                0x01, // Usage Page ("Generic Desktop Page")
                0x81  // Usage ("System Power Down")
            },
            Package(5) {
                1,    // This is a Control
                1,    // Interrupt index in _CRS for Volume Up Button
                1,    // Unique ID of Parent Collection
                0x0C, // Usage Page ("Consumer Page")
                0xE9  // Usage ("Volume Increment")
            },
            Package(5) {
                1,    // This is a Control
                2,    // Interrupt index in _CRS for Volume Down Button
                1,    // Unique ID of Parent Collection
                0x0C, // Usage Page ("Consumer Page")
                0xEA  // Usage ("Volume Decrement")
            },
            Package(5) {
                1,    // This is a Control
                3,    // Interrupt index in _CRS for Windows/Home Button
                1,    // Unique ID of Parent Collection
                0x07, // Usage Page ("Keyboard Page")
                0xE3  // Usage ("Keyboard Left GUI")
            },
            Package(5) {
                1,    // This is a Control
                4,    // Interrupt index in _CRS for Rotation Lock Button
                1,    // Unique ID of Parent Collection
                0x01, // Usage Page ("Generic Desktop Page")
                0xCA  // Usage ("System Display Rotation Lock Slider Switch")
            }
        }
    })
}

```
