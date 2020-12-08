---
title: 基于 USB 的 HID 设备的选择性挂起
description: 通用串行总线规范的修订版2.0 指定 USB 选择性挂起功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 917d29b0f8970f2301b9d02ad47e56db007be6d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820325"
---
# <a name="selective-suspend-for-hid-over-usb-devices"></a>基于 USB 的 HID 设备的选择性挂起


*通用串行总线规范* 的修订版2.0 指定 USB 选择性挂起功能。 通过使用此功能，Windows 操作系统可以有选择地挂起空闲 USB 设备。 这允许 Windows 有效地管理整个系统的电源要求。 有关 Windows 如何支持 USB 选择性挂起功能的详细信息，请参阅 [usb 选择性挂起](../usbcon/usb-selective-suspend.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

默认情况下，Windows 将禁用 USB 选择性挂起，以便提供一致的用户体验，并避免从选择性挂起恢复延迟。

支持选择性挂起的 HID 设备必须旨在：

-   从选择性挂起状态恢复时，保留第一个输入、触摸、移动或按键。
-   从选择性挂起移动时唤醒。
-   如果适用) ，请维持无线链接 (。
-   维持任何活动状态 Led （如 NUM lock 或 CAPS lock）的供电。
-   从选择性挂起恢复，用户不会有任何明显的延迟。

Windows 8 支持两种方法，用于启用 HID USB 设备的选择性挂起。 这些限制如下：

1.  **MICROSOFT OS 描述符 \[首选 \]**： Microsoft OS 描述符的扩展属性描述符可用于写入所需的注册表项 () ，以支持 USB HID 选择性挂起。
2.  **供应商提供的 inf**：硬件制造商可以提供一个 inf 文件 (与 HID devnode) 的 USB 硬件 ID 相匹配，以安装相应的注册表项。

Microsoft 建议硬件供应商和 PC 制造商使用第一个选项启用 USB HID 选择性挂起。 此选项的优点是：

-   硬件供应商和 PC 制造商不必安装另一个 INF 文件。
-   所需的注册表设置会在新的 Windows 8 安装上自动填充。
-   升级到 Windows 8 时，所需的注册表设置会保留。
-   用户无法通过卸载 INF 来丢失 (或禁用) 选择性挂起功能。

但是，如果硬件供应商和 PC 制造商仍要使用 INF 方法，则可以使用以下示例。 下面是一个示例 INF 文件，演示如何在 Windows 中为 HID 设备启用此 USB 功能：

```ManagedCPlusPlus
; Vendor INF File for USB HID devices
;
; A sample INF for a stand-alone USB HID device that supports 
; selective suspend

[Version]
Signature   ="$WINDOWS NT$"
Class       =HIDClass
ClassGuid   ={745a17a0-74d3-11d0-b6fe-00a0c90f57da}
Provider    =%VendorName%
DriverVer   =09/19/2008,6.0.0.0
CatalogFile =VendorXYZ.cat

; ================= Class section =====================
[ControlFlags]
ExcludeFromSelect=*

[SourceDisksNames]
1 = %DiskName%,,,""

;*****************************************
; Install Section
;*****************************************

[Manufacturer]
%VendorName% = VendorXYZDevice,NTx86,NTamd64,NTarm

[VendorXYZDevice.NTx86]
%VendorXYZ.DeviceDesc% = VendorXYZDevice_Install, USB\VID_045E&PID_00B4

[VendorXYZDevice.NTamd64]
%VendorXYZ.DeviceDesc% = VendorXYZDevice_Install, USB\VID_045E&PID_00B4

[VendorXYZDevice.NTarm]
%VendorXYZ.DeviceDesc% = VendorXYZDevice_Install, USB\VID_045E&PID_00B4


[VendorXYZDevice_Install.NT] 
include     = input.inf
needs       = HID_SelSus_Inst.NT

[VendorXYZDevice_Install.NT.HW]
include     = input.inf
needs       = HID_SelSus_Inst.NT.HW

[VendorXYZDevice_Install.NT.Services]
include     = input.inf
needs       = HID_SelSus_Inst.NT.Services

[Strings]
VendorName = "Vendor XYZ"
DiskName   = "Vendor XYZ Installation Disk"
VendorXYZ.DeviceDesc = "VendorXYZ Device"
```

其中：

1.  [**INF 版本部分**](../install/inf-version-section.md)应将 **CLASSGUID** 和 **DriverVer** 指令设置如下：

    -   **CLASSGUID** 指令必须为 HID 设备指定 MICROSOFT 类 GUID。 此 GUID 的值为 {745a17a0-74d3-11d0-b6fe-00a0c90f57da}。

    -   **DriverVer** 指令的值必须具有比 Input 中的 **DriverVer** 指令指定的值更新的日期和版本号更高的值。

2.  2. VendorXYZDevice \* 部分指定供应商 HID 设备 (ID) 的硬件标识符。 硬件 ID 由供应商标识符 (VID) 和产品标识符 (PID) 组成。 设备的每个硬件 ID 必须具有对供应商和设备唯一的 VID/PID 值。 这可确保相同的硬件 ID 不与多个名称和设置相对应

3.  3. VendorXYZDevice \_ 和 VendorXYZDevice \_ 部分都是 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)。 在此示例中，这些部分包含 INF **Include** 和 **需求** 指令。

    **Include** 指令引用系统提供的输入 .inf 文件，其中包含为供应商的 HID 设备启用 USB 选择性挂起功能所需的 inf 部分。

    **需求** 指令指示应在设备安装过程中处理来自输入的哪些部分。 在这种情况下， \_ 将 \_ 选择 HID SelSus 指令部分，而不是默认的 hid \_ 指令节，这不支持选择性挂起。

4.  4. VendorXYZDevice \_ 部分是一个 [**INF DDInstall 部分**](../install/inf-ddinstall-hw-section.md)，。 在此示例中，部分还包含与 INF **Include** 和 **需求** 指令相同的值。

 

