---
title: 组件固件更新 (CFU) INF 配置
description: 提供有关配置组件固件更新 INF 文件 (CFU) 的信息。
ms.date: 10/01/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 8da017d88774cbc64eafcfbef6b6bac237c0bcd1
ms.sourcegitcommit: b14becba4beb4e7c843908710352ad60999f0c38
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97611761"
---
# <a name="component-firmware-update-cfu-inf-file-configuration"></a>组件固件更新 (CFU) INF 文件配置

若要为 CFU 配置自定义 INF 文件，请按照本主题中的指导为固件映像文件和硬件设备提供正确的值和设置。

> [!NOTE]
> CFU 在 Windows 10 中提供，版本 2004 (Windows 10 2020 更新) 及更高版本。

下面附带的 [示例 CFU INF 文件](#sample-cfu-inf-file) 为设备的自定义 INF 文件提供了一个起点。 示例 INF 将 CFU 收件箱驱动程序配置 ( # A0) 为虚拟 CFU Hid 设备启用固件更新方案。 有关模拟在虚拟 HID 设备上更新固件的示例虚拟设备代码和演练的详细信息，请参阅 [CFU VIRTUAL HID 设备固件更新模拟](cfu-firmware-update-simulation.md) 主题。 以下部分引用了包含的示例 INF 文件，以说明本主题中讨论的配置概念。

必须为你的设备固件和硬件专门自定义和配置你的实际 INF 文件。

## <a name="before-you-begin"></a>开始之前

以下资源将帮助你了解组件固件更新 (CFU) 协议。

- [组件固件更新简介](https://blogs.windows.com/buildingapps/?p=54456)

- [组件固件更新上的 WinHEC 2018 视频](https://developer.microsoft.com/windows/hardware/events)

- [组件固件更新 (CFU) 协议规范](cfu-specification.md)介绍了用于更新电脑上存在的组件固件的通用 HID 协议。 此规范允许组件接受固件，而不会在下载期间中断设备操作。

  - [CFU 固件更新示例](https://github.com/Microsoft/CFU/tree/master/Firmware)包含用于实现 CFU 协议的示例固件源代码。

  - [CFU 独立工具](cfu-standalone-tool.md)可用于在开发期间在设备上测试固件更新，并将其上载到 Windows 更新。

## <a name="overview"></a>概述

若要使用 CFU 模型更新设备的固件映像，应满足以下要求：

- 为设备提供自定义 INF 文件。 此文件为将固件更新发送到设备的 CFU 收件箱驱动程序提供信息。 建议自定义以下主题中提供的示例 CFU INF 文件，以支持固件更新方案。

- 你的设备必须附带符合 [CFU 协议](cfu-specification.md) 的固件映像，以便它可以接受来自 CFU 驱动程序的更新。

- 你的设备必须在运行 CFU 收件箱驱动程序)  (向操作系统公开自身作为 HID 设备，并公开 HID Top-Level 集合 (TLC) 。 CFU 收件箱驱动程序在 TLC 上加载并将固件更新发送到设备。

这使你可以通过 Windows 更新为你的市场内设备服务。 若要更新组件的固件，请通过 Windows 更新部署固件更新映像。 当 CFU 收件箱驱动程序检测到组件的状态时，它会在主机上执行必要的操作，并将固件映像传输到设备上的主要组件。

![CFU 固件更新](images/transfer-flowchart.png)

## <a name="configure-your-custom-cfu-inf-file"></a>配置自定义 CFU INF 文件

1. 在自定义 INF 文件中，插入设备的硬件 Id，如本示例中所示。
  
    ```inf
    [Standard.NTamd64]
    %CfuVirtualHidDeviceFwUpdate.DeviceDesc%=CfuVirtualHidDeviceFwUpdate, HID\VID_045E&UP:FA00_U:00F5 ; HardwareID for VirtualHidDevice MCU
    ```

    **INF 硬件 ID 设置**

    为了使 CFU 的收件箱驱动程序与固件通信，INF 中指定的硬件 ID 应该与固件中的 Hid 描述符配置中指定的硬件 ID 匹配。

    如下所示， *CfuVirtualHidDeviceFwUpdate* 值与虚拟固件模拟驱动程序的 Hid 描述符中指定的值匹配。

    ```inf
    [Standard.NTamd64]
    %CfuVirtualHidDeviceFwUpdate.DeviceDesc%=CfuVirtualHidDeviceFwUpdate, HID\VID_045E&UP:FA00_U:00F5
    ```

    有关详细信息，请参阅 [*DmfInterface*](https://github.com/microsoft/CFU/blob/master/Host/CFUFirmwareSimulation/sys/DmfInterface.c)中的以下代码 (Hid 报表描述符) **g_CfuVirtualHid_HidReportDescriptor** 。

    ```cpp
    0x06, CFU_DEVICE_USAGE_PAGE,        // USAGE_PAGE(0xFA00)
    0x09, CFU_DEVICE_USAGE,             // USAGE(0xF5)
    ```

1. 在自定义 INF 文件中，更新此处显示的以下条目 (包括 " **SourceDisksFiles** " 和 " **CopyFiles** " 部分) ，以匹配固件更新中的文件。

    例如，virtual CFU Hid 设备示例支持 (MCU 和音频) 的两个组件。 下面的示例部分为这些组件指定了产品/服务和负载文件。

    ```inf
    ; Specify the location of the firmware offer
    ; and payload file in the registry.
    ; The files are kept in driver store.
    ; When deployed, %13% would be expanded to
    ; the actual path in driver store.
    ;
    ; You can change subkey name under CFU
    ; (for example, "CfuVirtualHidDevice_MCU"),
    ; and specify your own offer
    ; (for example, "CfuVirtualHidDevice_MCU.offer.bin")
    ; and payload (for example, "CfuVirtualHidDevice_MCU.payload.bin")
    ; file name.
    ;
    HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_MCU,Offer,   0x00000000, %13%\CfuVirtualHidDevice_MCU.offer.bin
    HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_MCU,Payload, 0x00000000, %13%\CfuVirtualHidDevice_MCU.payload.bin
    HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_Audio,Offer,   0x00000000, %13%\CfuVirtualHidDevice_Audio.offer.bin
    HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_Audio,Payload, 0x00000000, %13%\CfuVirtualHidDevice_Audio.payload.bin

    [SourceDisksFiles]
    CfuVirtualHidDevice_MCU.offer.bin=1
    CfuVirtualHidDevice_MCU.payload.bin=1
    CfuVirtualHidDevice_Audio.offer.bin=1
    CfuVirtualHidDevice_Audio.payload.bin=1

    [CfuVirtualHidDeviceFwUpdate.CopyFiles]
    CfuVirtualHidDevice_MCU.offer.bin
    CfuVirtualHidDevice_MCU.payload.bin
    CfuVirtualHidDevice_Audio.offer.bin
    CfuVirtualHidDevice_Audio.payload.bin
    ```

    有关完整的 CFU INF 示例文件，请参阅下面的 [示例 CFU inf 文件](#sample-cfu-inf-file) 。

    > [!NOTE]
    > 安装包时，OS 会将替换为 `%13%` 文件的完整路径，然后再创建注册表值。 因此，驱动程序能够枚举注册表并识别所有固件映像和提供的文件。

    > [!NOTE]
    >  在上面的示例中，"A410A898-8132-4246-AC1A-30F1E98BB0A4"、"产品/服务"、"负载" 不应更改，因为 CFU 收件箱驱动程序会在运行时查找这些值。

1. 在自定义 INF 文件中，用下面的表和示例 INF 部分所述的注册表值功能设置来指定设备的功能。

    CFU 收件箱驱动程序提供了一种方法，用于自定义驱动程序行为，以便在某些情况下优化。 这些设置通过注册表设置进行控制，如下面的 CFU 注册表值表中所述。

    例如，CFU 收件箱驱动程序需要根据固件实现的值功能使用情况详细信息。 有关详细信息和如何执行此操作的示例，请参阅以下 **INF 值功能设置** 部分。

    你可以根据固件实现需求配置每个注册表值。

    **CFU 注册表值**

    | 注册表值 | 说明 |
    |--|--|
    | 对齐方式 | 协议属性：此配置需要的 bin 记录对齐方式是什么？<p>在协议的有效负载发送阶段，驱动程序将使用有效负载填充多个 Hid 缓冲区，并逐个发送到固件。<p>此选项控制打包有效负载时的对齐要求。<p>默认情况下，使用8字节对齐。 如果不需要对齐，请将此配置为1。 |
    | UseHidSetOutputReport | 0-在发送任何输出报告时，驱动程序将使用写入请求。<p>1-驱动程序将使用用于发送任何输出报告的 IOCTL_HID_SET_OUTPUT_REPORT。<p>默认为 0。 如果基础传输不是 USB (例如，HID Over BTH) ，则将此设置为1。 |
    | OfferInputValueCapabilityUsageRangeMinimum | 提供输入报告处理的最小值功能使用情况。 |
    | OfferOutputValueCapabilityUsageRangeMinimum | 提供输出报告处理的最小值功能使用情况。 |
    | PayloadInputValueCapabilityUsageRangeMinimum | 负载输入报告处理的最小值功能使用情况。 |
    | PayloadOutputValueCapabilityUsageRangeMinimum | 负载输出报表处理的最小值功能使用情况。 |
    | VersionsFeatureValueCapabilityUsageRangeMinimum | 版本功能报表处理的最小值功能使用情况。 |

    **INF 值功能设置**

    为了使 CFU 收件箱驱动程序与固件通信，在 INF 中指定的值功能使用情况应与固件中的 Hid 描述符配置中的使用情况匹配。

    在此示例中，INF 值与虚拟固件模拟驱动程序的 Hid 描述符中指定的值匹配。

    ```inf
    [CfuVirtualHidDeviceFwUpdate_HWAddReg]
    ...
    ...
    HKR,,OfferInputValueCapabilityUsageRangeMinimum,0x00010001,0x1A
    HKR,,OfferOutputValueCapabilityUsageRangeMinimum,0x00010001, 0x1E
    HKR,,PayloadInputValueCapabilityUsageRangeMinimum,0x00010001,0x26
    HKR,,PayloadOutputValueCapabilityUsageRangeMinimum,0x00010001,0x31
    HKR,,VersionsFeatureValueCapabilityUsageRangeMinimum,0x00010001, 0x42
    ```

    有关详细信息，请参阅 [*DmfInterface*](https://github.com/microsoft/CFU/blob/master/Host/CFUFirmwareSimulation/sys/DmfInterface.c)中的以下代码 (Hid 报表描述符) **g_CfuVirtualHid_HidReportDescriptor** 。

    ```cpp
    0x85, REPORT_ID_PAYLOAD_INPUT,      // REPORT_ID(34)
    0x75, INPUT_REPORT_LENGTH,          // REPORT SIZE(32)
    0x95, 0x04,                         // REPORT COUNT(4)
    0x19, PAYLOAD_INPUT_USAGE_MIN,      // USAGE MIN (0x26)
    0x29, PAYLOAD_INPUT_USAGE_MAX,      // USAGE MAX (0x29)
    0x81, 0x02,                         // INPUT(0x02)

    0x85, REPORT_ID_OFFER_INPUT,        // REPORT_ID(37)
    0x75, INPUT_REPORT_LENGTH,          // REPORT SIZE(32)
    0x95, 0x04,                         // REPORT COUNT(4)
    0x19, OFFER_INPUT_USAGE_MIN,        // USAGE MIN (0x1A)
    0x29, OFFER_INPUT_USAGE_MAX,        // USAGE MAX (0x1D)
    0x81, 0x02,                         // INPUT(0x02)

    0x85, REPORT_ID_PAYLOAD_OUTPUT,     // REPORT_ID(32)
    0x75, 0x08,                         // REPORT SIZE(8)
    0x95, OUTPUT_REPORT_LENGTH,         // REPORT COUNT(60)
    0x09, PAYLOAD_OUTPUT_USAGE,         // USAGE(0x31)
    0x92, 0x02, 0x01,                   // OUTPUT(0x02)

    0x85, REPORT_ID_OFFER_OUTPUT,       // REPORT_ID(37)
    0x75, INPUT_REPORT_LENGTH,          // REPORT SIZE(32)
    0x95, 0x04,                         // REPORT COUNT(4)
    0x19, OFFER_OUTPUT_USAGE_MIN,       // USAGE MIN (0x1E)
    0x29, OFFER_OUTPUT_USAGE_MAX,       // USAGE MAX (0x21)
    0x91, 0x02,                         // OUTPUT(0x02)

    0x85, REPORT_ID_VERSIONS_FEATURE,   // REPORT_ID(32)
    0x75, 0x08,                         // REPORT SIZE(8)
    0x95, FEATURE_REPORT_LENGTH,        // REPORT COUNT(60)
    0x09, VERSIONS_FEATURE_USAGE,       // USAGE(0x42)
    0xB2, 0x02, 0x01,                   // FEATURE(0x02)
    ```

## <a name="deploy-the-firmware-package-through-windows-update"></a>通过 Windows 更新部署固件包

接下来，通过 Windows 更新部署包。

有关部署的信息，请参阅 [Windows 10 驱动程序发布工作流 (.docx 下载) ](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)。

## <a name="firmware-update-image-file-format"></a>固件更新图像文件格式

固件更新映像包含两部分：一个产品/服务文件和一个负载文件。 此产品/服务包含有关有效负载的必要信息，以允许设备中的主要组件接收更新，以确定有效负载是否可接受。 负载是主组件可以使用的地址范围和字节数。

### <a name="offer-format"></a>提议格式

该产品/服务文件是16字节的二进制数据，其结构必须与 CFU 协议规范的 section 5.5.1 中指定的格式匹配。

### <a name="payload-format"></a>负载格式

负载文件是二进制文件，该文件是连续存储的记录的集合。 每个记录均采用以下格式。

| Offset | 大小 | 值 | 说明 |
|--|--|--|--|
| 字节0 | DWORD | 固件地址 | 小 Endian (LSB 首先) 用于写入数据的地址。 该地址是从0开始的。 在内存中放置图像时，固件可以使用此偏移量来确定所需的地址。 |
| 字节 4 | Byte | 长度 | 负载数据的长度。 |
| 字节 5-N | 字节 | data | 有效负载数据的字节数组。 |

## <a name="firmware-update-status"></a>固件更新状态

在协议事务期间，CFU 收件箱驱动程序将写入注册表项以指明状态。  下表描述了驱动程序在协议的各个阶段中涉及的值的名称、值的格式和含义。

- \_表中的 ID_ 表示从产品/服务文件中检索到的组件 ID。 如规范中所述，组件 ID 唯一标识每个组件。

- 有关值 DWORD 的信息，请参阅规范。

| 阶段 | 位置 | Reg 值名称 | 值 (DWORD)  |
|--|--|--|--|
| Start产品/服务。 | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* CurrentFwVersion" | 设备版本 |
|  | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* FirmwareUpdateStatus" | FIRMWARE_UPDATE_STATUS_NOT_STARTED |
| 提供即将发送产品/服务。 | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* OfferFwVersion" | 发送 (或将要发送) 到设备的版本。 |
|  (拒绝提供响应)  | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* FirmwareUpdateStatusRejectReason" | 设备返回的拒绝原因。 |
| 提供响应 (设备忙碌)  | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* FirmwareUpdateStatus" | FIRMWARE_UPDATE_STATUS_BUSY_PROCESSING_UPDATE |
| 提供 (接受) 的响应即将发送有效负载。 | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* FirmwareUpdateStatus" | FIRMWARE_UPDATE_STATUS_DOWNLOADING_UPDATE |
| 已接受负载。 | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* FirmwareUpdateStatus" | FIRMWARE_UPDATE_STATUS_PENDING_RESET |
| 任何阶段出错。 | {设备硬件密钥} \ComponentFirmwareUpdate | "Component *ID* FirmwareUpdateStatus" | FIRMWARE_UPDATE_STATUS_ERROR |

## <a name="sample-cfu-inf-file"></a>示例 CFU INF 文件

```inf
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;
;  Copyright (c) Microsoft Corporation.  All rights reserved.
;
;      THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY
;      KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
;      IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR
;      PURPOSE.
;
; File:
;
:      CfuVirtualHidDeviceFwUpdate.inx
;
; Description:
;
;      Sample INF file for Cfu virtual Hid device firmware update.
;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

[Version]
Signature="$Windows NT$"
Class=Firmware
ClassGuid={f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
Provider=%ManufacturerName%
CatalogFile=CfuVirtualHidDeviceFwUpdate.cat
DriverVer = 12/16/2019,11.42.16.703
PnPLockDown=1

[SourceDisksNames]
1= %DiskName%

[DestinationDirs]
CfuVirtualHidDeviceFwUpdate.CopyFiles=13

[Manufacturer]
%ManufacturerName%=Standard,NTamd64

[Standard.NTamd64]
%CfuVirtualHidDeviceFwUpdate.DeviceDesc%=CfuVirtualHidDeviceFwUpdate, HID\VID_045E&UP:FA00_U:00F5 ; HardwareID for VirtualHidDevice MCU

[CfuVirtualHidDeviceFwUpdate.NT]
Include            = HidCfu.inf
Needs              = HidCfu.NT
CopyFiles          = CfuVirtualHidDeviceFwUpdate.CopyFiles

[CfuVirtualHidDeviceFwUpdate.NT.Wdf]
Include            = HidCfu.inf
Needs              = HidCfu.NT.Wdf

[CfuVirtualHidDeviceFwUpdate.NT.HW]
AddReg = CfuVirtualHidDeviceFwUpdate_HWAddReg

[CfuVirtualHidDeviceFwUpdate_HWAddReg]
HKR,,FriendlyName,,%FwUpdateFriendlyName%
HKR,,Alignment,0x00010001, 1                       ; (No Alignment)
HKR,,OfferInputValueCapabilityUsageRangeMinimum,0x00010001,0x1A
HKR,,OfferOutputValueCapabilityUsageRangeMinimum,0x00010001, 0x1E
HKR,,PayloadInputValueCapabilityUsageRangeMinimum,0x00010001,0x26
HKR,,PayloadOutputValueCapabilityUsageRangeMinimum,0x00010001,0x31
HKR,,VersionsFeatureValueCapabilityUsageRangeMinimum,0x00010001, 0x42

; Specify the location of the firmware offer and payload file in the registry.
; The files are kept in the driver store.
; When deployed, %13% would be expanded to the actual path
; in driver store.
;
; You can change subkey name under CFU (e.g. "CfuVirtualHidDevice_MCU"), and specify your own offer
; (e.g. "CfuVirtualHidDevice_MCU.offer.bin") and payload (e.g "CfuVirtualHidDevice_MCU.payload.bin") file name.
;
HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_MCU,Offer,   0x00000000, %13%\CfuVirtualHidDevice_MCU.offer.bin
HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_MCU,Payload, 0x00000000, %13%\CfuVirtualHidDevice_MCU.payload.bin
HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_Audio,Offer,   0x00000000, %13%\CfuVirtualHidDevice_Audio.offer.bin
HKR,A410A898-8132-4246-AC1A-30F1E98BB0A4\CfuVirtualHidDevice_Audio,Payload, 0x00000000, %13%\CfuVirtualHidDevice_Audio.payload.bin

[SourceDisksFiles]
CfuVirtualHidDevice_MCU.offer.bin=1
CfuVirtualHidDevice_MCU.payload.bin=1
CfuVirtualHidDevice_Audio.offer.bin=1
CfuVirtualHidDevice_Audio.payload.bin=1

[CfuVirtualHidDeviceFwUpdate.CopyFiles]
CfuVirtualHidDevice_MCU.offer.bin
CfuVirtualHidDevice_MCU.payload.bin
CfuVirtualHidDevice_Audio.offer.bin
CfuVirtualHidDevice_Audio.payload.bin

[CfuVirtualHidDeviceFwUpdate.NT.Services]
Include            = HidCfu.inf
Needs              = HidCfu.NT.Services

; =================== Generic ==================================

[Strings]
ManufacturerName="Surface"
CfuVirtualHidDeviceFwUpdate.DeviceDesc = "CfuVirtualHidDevice Firmware Update"
DiskName = "CfuVirtualHidDevice Firmware Update Installation Disk"
FwUpdateFriendlyName= "CfuVirtualHidDevice Firmware Update"
```

## <a name="troubleshooting"></a>疑难解答

1. 检查 Windows 软件跟踪预处理器 (WPP) 日志，以查看每个组件的驱动程序端交互。

1. 检查事件日志中是否存在任何严重错误。

1. 查看驱动程序提供的固件更新状态中所述的簿记注册表项。

## <a name="faq"></a>常见问题解答

**我有一个需要更新的组件 A，如何使 CFU 驱动程序知道组件 A？**

需要使用组件 A 创建的 TLC 的硬件 ID 配置 CFU 收件箱驱动程序 INF。

**我有两个组件：组件 A 和子组件 B。如何使 CFU 驱动程序知道组件 B？**

不需要。 驱动程序无需知道组件层次结构。 它与主组件交互。

**如何使驱动程序了解我的固件文件 (产品/服务、需要发送到组件的负载) 文件？**

固件文件信息在 INF 中设置为注册表值。

**对于主组件 A 及其子组件，我有多个固件文件、多个产品/服务、有效负载。如何使驱动程序知道哪个固件文件适用于哪个组件？**

固件文件信息在 INF 中设置为注册表值。

**我使用的是固件更新驱动程序。 如何实现知道更新是否成功？**

固件更新状态将由注册表中的驱动程序作为簿记的一部分进行更新。

## <a name="additional-resources"></a>其他资源

了解如何使用 Windows Driver Foundation 开发 Windows 驱动程序 (WDF) ：

- [使用 Windows Driver Foundation 开发驱动程序](../wdf/developing-drivers-with-wdf.md)，由 "Orwick" 和 "专家 Smith" 编写

- [使用 WDF 开发驱动程序](../wdf/using-the-framework-to-develop-a-driver.md)