---
title: 基于 USB 的 HID 设备的选择性挂起
description: 版本 2.0 的通用串行总线规范指定 USB 选择性挂起功能。
ms.assetid: A4560D7C-8A32-4A91-95B6-4377E0F0D0C1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffdbb2132bdcf6e9982d3761faa750059d24b8f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385810"
---
# <a name="selective-suspend-for-hid-over-usb-devices"></a>基于 USB 的 HID 设备的选择性挂起


版本 2.0*通用串行总线规范*指定 USB 选择性挂起功能。 通过使用此功能，Windows 操作系统可以有选择地挂起空闲的 USB 设备。 这使 Windows 能够高效地管理整个系统的电源需求。 详细了解 Windows 如何支持 USB 选择性挂起功能，请参阅[USB 选择性挂起](../usbcon/usb-selective-suspend.md)。 （此资源可能不会在某些语言和国家/地区中可用。）

默认情况下，USB 选择性挂起禁用的 Windows，以便提供一致的用户体验并避免恢复延迟从选择性挂起。

支持选择性挂起的 HID 设备必须设计为：

-   从选择性恢复挂起时，请保留第一个输入、 触控、 移动或键按。
-   从选择性唤醒挂起的移动。
-   维护无线链接 （如果适用）。
-   维护任何活动的状态 Led，如 NUM lock 或 CAPS lock 的电源。
-   从选择性恢复挂起而无需用户感知到的任何延迟。

Windows 8 支持两种方法启用的选择性挂起的 HID USB 设备。 它们是：

1.  **Microsoft 操作系统描述符\[PREFERRED\]** :Microsoft 操作系统描述符的扩展属性描述符可以用于编写在必要的注册表项以支持 USB HID 的选择性挂起。
2.  **供应商提供 INF**:硬件制造商可以提供的 INF 文件 （与 HID devnode USB 硬件 id 相匹配） 来安装相应的注册表项。

Microsoft 建议，硬件供应商和 PC 制造商使用第一个选项来启用 USB HID 的选择性挂起。 此选项的优点是：

-   硬件供应商和 PC 制造商不需要安装一个额外的 INF 文件。
-   必需的注册表设置将自动填充新的 Windows 8 安装。
-   升级到 Windows 8 时将保留必要的注册表设置。
-   该用户不能丢失 （或禁用） 通过卸载 INF 选择性挂起功能。

但是，硬件供应商和 PC 制造商希望为仍使用 INF 方法中，可以使用下面的示例。 下面是一个示例 INF 文件，演示如何启用 Windows 中的 HID 设备的此 USB 功能：

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

1.  [ **INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)应有**CLASSGUID**并**DriverVer**指令设置，如下所示：

    -   **CLASSGUID**指令必须指定 HID 设备的 Microsoft 类 GUID。 此 GUID 具有 {745a17a0-74d3-11d0-b6fe-00a0c90f57da} 的值。

    -   **DriverVer**指令必须具有一个值具有更高版本的日期和更高版本的版本号高于指定的值，该值**DriverVer** Input.inf 指令。

2.  2. VendorXYZDevice\*部分指定供应商的 HID 设备的硬件标识符 (ID)。 硬件 ID 包含供应商标识符 (VID) 和产品标识符 (PID)。 设备每个硬件 ID 必须是唯一的供应商和设备的 VID/PID 值。 这可以保证在相同的硬件 ID 与多个名称和设置不对应

3.  3. VendorXYZDevice\_Install.NT 和 VendorXYZDevice\_Install.NT.HW 部分都[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。 在此示例中，以下各节包含 INF **Include**并**需要**指令。

    **Include**指令引用系统提供 Input.inf 文件，其中包含 INF 部分需要启用 USB 选择性挂起供应商的 HID 设备的功能。

    **需要**指令指示应在设备安装过程中处理从 Input.inf 哪些部分。 在此情况下，HID\_SelSus\_Inst 部分选择而不是默认 HID\_Inst 部分中，不支持选择性挂起。

4.  4. VendorXYZDevice\_Install.NT.Services 部分[ **INF DDInstall.HW 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)。 在此示例中，本节还包含相同的值为 INF **Include**并**需要**指令。

 

 




