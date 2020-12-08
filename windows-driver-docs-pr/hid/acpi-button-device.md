---
title: ACPI 按钮设备
description: 通用按钮设备是一个标准设备，用于通过硬件中断报告按钮事件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55ff2d4ea0349ed5010e724034ef861ac0327e61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791551"
---
# <a name="acpi-button-device"></a>ACPI 按钮设备

通用按钮设备是一种标准设备，用于通过硬件中断报告按钮事件，并将这些中断映射到在人体学接口设备 (HID) 规范中定义的特定使用情况。

若要将按钮的功能表达给操作系统，需要两条信息：

- HID 控件的用法
- 控件所属的 HID 集合的使用情况

用法是使用页面和使用 ID 的组合。 例如，"音量向上" 按钮被标识为 " (使用量" 页上的 "使用情况 Id 0xE9)  (使用情况页0x0C，用法 Id 0x01) 中的" 使用情况 Id "页。

通用按钮设备的 ACPI 设备 Id 为 ACPI0011。 Windows 将加载 Microsoft 提供的内置驱动程序，Hidinterrupt.sys 设备。

有关通用按钮设备的详细信息，请访问 [统一可扩展固件接口](https://uefi.org/specifications) 规范网站，并下载 *ACPI 规范6.0 版* PDF 文档。 然后，使用左侧窗格导航到 **9.19 节**。

## <a name="sample-buttons-acpi-for-phonetablet"></a>手机/平板电脑的示例按钮 ACPI

用于描述运行 Windows 10 移动版的手机/平板电脑中的按钮的示例。

```cpp
// Sample Buttons ACPI for Phone/Tablet device running Windows 10 Mobile.

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

//
// This HID Report Descriptor describes a 1-byte input report for the 8
// buttons supported on Windows 10 Mobile. Following are the buttons and
// their bit positions in the input report:
//     Bit 0: Power Button
//     Bit 1: Volume Up Button
//     Bit 2: Volume Down Button
//     Bit 3: Camera Auto-focus Button
//     Bit 4: Camera Shutter Button
//     Bit 5: Back Button
//     Bit 6: Windows/Home Button
//     Bit 7: Search Button
//
// The Report Descriptor also defines a 1-byte Control Enable/Disable
// feature report of the same size and bit positions as the Input Report.
// For a Get Feature Report, each bit in the report conveys whether the
// corresponding Control (i.e. button) is currently Enabled (1) or
// Disabled (0). For a Set Feature Report, each bit in the report conveys
// whether the corresponding Control (i.e. button) should be Enabled (1)
// or Disabled (0).
//

UCHAR ReportDescriptor[] = {

    15, 00,         // LOGICAL_MINIMUM (0)
    25, 01,         // LOGICAL_MAXIMUM (1)
    75, 01,         // REPORT_SIZE (1)

    06, 01,         // USAGE_PAGE (Generic Desktop)
    0A, 0D,         // USAGE (Portable Device Control)
    A1, 01,         // COLLECTION (Application)
    85, 01,         //   REPORT_ID (1) (For Input Report & Feature Report)

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 01,         //     USAGE_PAGE (Generic Desktop)
    0A, 81,         //     USAGE (System Power Down)            // Power Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 0C,         //     USAGE_PAGE (Consumer Devices)
    0A, E9,         //     USAGE (Volume Increment)             // Volume Up Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 0C,         //     USAGE_PAGE (Consumer Devices)
    0A, EA,         //     USAGE (Volume Decrement)             // Volume Down Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 90,         //     USAGE_PAGE (Camera Control)
    0A, 20,         //     USAGE (Camera Auto-focus)            // Camera Auto-focus Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 90,         //     USAGE_PAGE (Camera Control)
    0A, 21,         //     USAGE (Camera Shutter)               // Camera Shutter Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 0C,         //     USAGE_PAGE (Consumer Page)
    0A, 224,        //     USAGE (AC Back)                      // Back Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 07,         //     USAGE_PAGE (Keyboard)
    0A, E3,         //     USAGE (Keyboard Left GUI)            // Windows/Home Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 0C,         //     USAGE_PAGE (Consumer)
    0A, 221,        //     USAGE (AC Search)                    // Search Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    C0              //  END_COLLECTION
};


//
// This HID Report Descriptor describes a 1-byte Input Report for the 3
// Headset buttons supported on Windows 10 Mobile. Following are the
// buttons and their bit positions in the Input Report:
//     Bit 0: HeadSet : Middle Button
//     Bit 1: HeadSet : Volume Up Button
//     Bit 2: HeadSet : Volume Down Button
//     Bit 3: Unused
//     Bit 4: Unused
//     Bit 5: Unused
//     Bit 6: Unused
//     Bit 7: Unused
//

UCHAR ReportDescriptor[] = {
    0x05, 0x01,         // USAGE_PAGE (Generic Desktop Controls)
    0x09, 0x0D,         // USAGE (Portable Device Buttons)
    0xA1, 0x01,         // COLLECTION (Application)
    0x85, 0x01,         //   REPORT_ID (1)
    0x05, 0x09,         //   USAGE_PAGE (Button Page)
    0x09, 0x01,         //   USAGE (Button 1 - HeadSet : Middle Button)
    0x09, 0x02,         //   USAGE (Button 2 - HeadSet : Volume Up Button)
    0x09, 0x03,         //   USAGE (Button 3 - HeadSet : Volume Down Button)
    0x15, 0x00,         //   LOGICAL_MINIMUM (0)
    0x25, 0x01,         //   LOGICAL_MAXIMUM (1)
    0x75, 0x01,         //   REPORT_SIZE (1)
    0x95, 0x09,         //   REPORT_COUNT (3)
    0x81, 0x02,         //   INPUT (Data,Var,Abs)
    0x95, 0x07,         //   REPORT_COUNT (5)     // 5 unused bits in 8-bit Input Report.
    0x81, 0x03,         //   INPUT (Cnst,Var,Abs)
    0xC0,               // END_COLLECTION
};
```

## <a name="sample-buttons-acpi-for-desktop"></a>示例按钮桌面版 ACPI

介绍如何在运行 Windows 10 for desktop edition (Home、Pro、Enterprise 和教育) 中介绍适用于运行 Windows 10 的设备的手机/平板电脑设备的按钮的示例。

```cpp
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

//
// This HID Report Descriptor describes a 1-byte input report for the 5
// buttons supported on Windows 10 for desktop editions (Home, Pro, and Enterprise). Following are the buttons and
// their bit positions in the input report:
//     Bit 0 - Windows/Home Button
//     Bit 1 - Power Button
//     Bit 2 - Volume Up Button
//     Bit 3 - Volume Down Button
//     Bit 4 - Rotation Lock Slider switch
//     Bit 5 - Unused
//     Bit 6 - Unused
//     Bit 7 - Unused
//
// The Report Descriptor also defines a 1-byte Control Enable/Disable
// feature report of the same size and bit positions as the Input Report.
// For a Get Feature Report, each bit in the report conveys whether the
// corresponding Control (i.e. button) is currently Enabled (1) or
// Disabled (0). For a Set Feature Report, each bit in the report conveys
// whether the corresponding Control (i.e. button) should be Enabled (1)
// or Disabled (0).
//

UCHAR ReportDescriptor[] = {

    15, 00,         // LOGICAL_MINIMUM (0)
    25, 01,         // LOGICAL_MAXIMUM (1)
    75, 01,         // REPORT_SIZE (1)

    06, 01,         // USAGE_PAGE (Generic Desktop)
    0A, 0D,         // USAGE (Portable Device Control)
    A1, 01,         // COLLECTION (Application)
    85, 01,         //   REPORT_ID (1) (For Input Report & Feature Report)

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 07,         //     USAGE_PAGE (Keyboard)
    0A, E3,         //     USAGE (Keyboard LGUI)                // Windows/Home Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 01,         //     USAGE_PAGE (Generic Desktop)
    0A, 81,         //     USAGE (System Power Down)            // Power Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 0C,         //     USAGE_PAGE (Consumer Devices)
    0A, E9,         //     USAGE (Volume Increment)             // Volume Up Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 0C,         //     USAGE_PAGE (Consumer Devices)
    0A, EA,         //     USAGE (Volume Decrement)             // Volume Down Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    C0,             //     END_COLLECTION

    06, 01,         //   USAGE_PAGE (Generic Desktop)
    0A, 0D,         //   USAGE (Portable Device Control)
    A1, 02,         //   COLLECTION (Logical)
    06, 01,         //     USAGE_PAGE (Generic Desktop)
    0A, CA,         //     USAGE (System Display Rotation Lock Slider Switch) // Rotation Lock Button
    95, 01,         //     REPORT_COUNT (1)
    81, 02,         //     INPUT (Data,Var,Abs)
    95, 06,         //     REPORT_COUNT (3)                     // 3 unused bits in 8-bit Input Report
    81, 03,         //     INPUT (Cnst,Var,Abs)
    05, 01,         //     USAGE_PAGE (Generic Desktop)
    09, CB,         //     USAGE (Control Enable)
    95, 01,         //     REPORT_COUNT (1)
    B1, 02,         //     FEATURE (Data,Var,Abs)
    95, 06,         //     REPORT_COUNT (3)                     // 3 unused bits in 8-bit Feature Report
    B1, 03,         //     FEATURE (Cnst,Var,Abs)
    C0,             //     END_COLLECTION

    C0              //  END_COLLECTION
};
```
