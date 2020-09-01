---
title: USB 设备的设备固件更新（不使用共同安装程序）
description: 概述在不使用共同安装程序的情况下更新 USB 设备固件的建议方法。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08a2175e5ca25231daa0a8ac1eda16ad111d0c7b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185229"
---
# <a name="device-firmware-update-for-usb-devices-without-using-a-co-installer"></a>USB 设备的设备固件更新（不使用共同安装程序）

USB 设备供应商使用共同安装程序为使用收件箱 USB 设备驱动程序的设备更新设备固件。 但是，新的 "通用 INF" 标准不支持共同安装程序，这是 Windows 10 上的一项要求。 这对于现有 USB 设备固件更新过程是一项挑战。 本主题概述了在不使用共同安装程序的情况下更新 USB 设备固件的建议方法。

## <a name="requirements"></a>要求

USB 设备固件更新过程的主要要求如下：

1. 无缝固件更新，无用户交互

1. 可靠恢复机制 (例如，没有设备的 bricking) 

1. 适用于 Windows 7 和更高版本

## <a name="overview"></a>概述

USB 设备（如 UVC 摄像机）是通过现场可更新固件发布的。 目前尚无标准方法来更新固件。 所有现有的更新机制都有一个常见的问题是，某些自定义软件套件在客户端上运行，并将固件下载到设备。 通常，作为设备安装过程的一部分，将安装固件更新软件套件。 共同安装程序开始启动固件更新过程。 在 Windows 10 上缺少共同安装程序会阻止设备供应商在该字段中更新这些设备上的固件。

若要绕过 USB 设备固件更新方案的共同安装程序，建议使用较低的筛选器驱动程序，将启动固件更新过程。 在 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 调用期间，筛选器驱动程序将检查设备固件版本并更新固件（如有必要）。

## <a name="firmware-update-overview"></a>固件更新概述

当 USB 设备插到系统中时，将为该设备安装通用收件箱驱动程序。 安装通用驱动程序后，操作系统会在 Windows 更新服务器中查询特定于供应商的驱动程序包可用性，并将其下载并安装驱动程序。 安装的驱动程序包将执行固件更新。

可以通过两种方式来更新固件。

1. 固件更新筛选器驱动程序

    1. 供应商提供的用于执行固件更新的较低筛选器驱动程序。

1. 固件更新设备驱动程序

    1. 供应商提供的低筛选器驱动程序，它将设备置于 "固件更新模式"。

    1. 设备将枚举为固件更新设备。

    1. 供应商提供的固件更新驱动程序将针对此设备进行加载并更新固件。

## <a name="method-1-firmware-update-filter-driver"></a>方法1：固件更新筛选器驱动程序

在此方法中，将在驱动程序更新过程中安装 USB 设备驱动程序的较低筛选器驱动程序。 此筛选器驱动程序将执行固件更新。

Windows 更新服务器上的驱动程序更新包将包含：

- 固件更新 WDF lower 筛选器驱动程序

- 用于安装固件更新 WDF 较低筛选器驱动程序的扩展 INF

- "固件 bin" 文件

![固件更新 UMDF 降低筛选器驱动程序方法](images/fw-update-umdf-lower-filter-driver-method.png)

安装驱动程序更新包时，将调用固件更新 WDF 筛选器驱动程序的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。 通过此例程，WDF 筛选器驱动程序将从 device HW 注册表项中获取设备固件版本。 设备固件应使用 MSO 描述符将固件版本放置在 device HW 注册表项上。

1. 如果设备固件版本和筛选器驱动程序的固件版本不同，则为; 否则为

1. 固件版本在设备硬件注册表项中不可用

    1. 然后，筛选器驱动程序会通过将 success 返回到 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 回拨，将自身插入到设备堆栈中。

1. 否则，筛选器驱动程序不会将自身插入到设备堆栈中

    1. 由于设备具有预期固件，因此不需要更新固件。

稍后在调用 WDF 筛选器驱动程序的 [EVT_WDF_DEVICE_D0_ENTRY](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调时，筛选器驱动程序必须使用 CM \_ Register \_ 通知或 IOREGISTERPLUGPLAYNOTIFICATION (UMDF 或 KMDF) 注册设备接口更改通知，以侦听 USB 设备将向其中注册设备的设备接口类。 例如 RGB 照相机的固件更新筛选器驱动程序将注册 KSCATEGORY \_ 视频 \_ 摄像机。 收到通知后，筛选器驱动程序应发布执行固件更新的工作项。

基于 UMDF 的固件更新驱动程序可以使用设备特定的 Api，也可以发出控制直接传输来访问 USB 设备以执行固件更新。 例如，照相机的基于 UMDF 的筛选器驱动程序将使用相机 Api 来执行固件更新。

基于 KMDF 的固件更新驱动程序可以发送特定于供应商的命令来执行固件更新。

完成固件闪烁后，设备必须断开连接，然后重新连接到该总线。 将通过新固件重新枚举设备。

建议使用 "固件更新筛选器驱动程序" 的方法，使其资源足以存放两个完整的固件映像 (更新映像和) 在设备内存上的备份映像。 原因是下载更新的固件时出现故障，设备可能会放弃更新并启动到其原始固件。 因此，不 bricking 设备。

## <a name="method-2-firmware-update-device-driver"></a>方法2：固件更新设备驱动程序

在此方法中，将在驱动程序更新过程中安装 USB 设备的较低筛选器驱动程序。 此筛选器驱动程序会将命令发送到设备以在固件更新模式下重新启动，在此模式下，设备将公开固件更新接口。 固件更新接口的驱动程序将加载并执行固件更新。

设备 Windows 更新服务器上的驱动程序更新包将包含：

1. 一个 WDF 较低筛选器驱动程序，它将设备置于固件更新模式

1. 用于安装 WDF lower 筛选器驱动程序的扩展 INF

除驱动程序更新包外，Windows 更新上还存在一个单独的固件更新设备驱动程序包，其中包含：

1. WDF 固件更新设备驱动程序及其 INF 和

1. "固件 bin" 文件。

![固件更新 WDF 驱动程序方法](images/fw-update-wdf-driver-method.png)

安装驱动程序更新包时，将调用 WDF 较低筛选器驱动程序的 AddDevice 例程。 通过此例程，筛选器驱动程序将从设备 HW 注册表项中查询设备固件版本。 设备固件应将 "固件版本" 设置为使用 MSO 描述符或 USB 设备的扩展 INF，放入设备 HW 注册表项。

1. 如果设备固件版本和筛选器驱动程序所需的固件版本不同或

1. 固件版本在设备硬件注册表项中不可用

1. 然后，WDF 筛选器驱动程序将自身插入到设备堆栈中。

1. 否则，WDF 筛选器驱动程序不会将自身插入到设备堆栈中

稍后在调用 WDF 筛选器驱动程序的 [EVT_WDF_DEVICE_D0_ENTRY](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调时，筛选器驱动程序会向设备发出特定于供应商的命令，并将其置于固件更新模式。 即，设备将断开连接并重新连接，同时公开固件更新接口。

系统将枚举固件更新设备接口。 将为此固件更新接口加载供应商在固件更新包中提供的自定义固件更新 WDF 驱动程序。 此驱动程序将更新固件。

稍后在调用 WDF 固件更新驱动程序的 [EVT_WDF_DEVICE_D0_ENTRY](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调时，驱动程序必须发布执行固件更新的工作项。

完成固件闪烁后，设备必须断开连接，然后重新连接到该总线。 将通过新固件重新枚举设备。

对于由于设备上的内存不足而无法保存已更新和原始固件映像的设备，建议使用此方法。 原因是下载更新的固件时出现故障，设备可能会放弃更新，并再次将设备启动到其固件更新模式，并且可以重试固件更新。 因此，不 bricking 设备。

## <a name="recovery"></a>恢复

由于各种原因，固件更新过程可能会失败。 如果出现这种情况，则再次枚举设备时，固件更新驱动程序可能会再次尝试更新固件并可能再次失败，并且此更新过程可能会在循环中结束。 固件更新驱动程序必须将上限限制为它可以执行的重试次数。 如果固件更新重试次数超出阈值 (例如，3次重试) 则筛选器驱动程序不应尝试再次更新固件，除非从 WU 下载了新版本的驱动程序。 固件更新驱动程序可以使用注册表来保持重试状态。

更新设备固件结束后，建议重置设备本身并重新枚举。

固件更新的两种方法都必须先停止，然后才能执行固件更新。 这可确保设备没有打开的句柄，并避免操作系统重启要求。

## <a name="sample-inf"></a>示例 INF

```INF
;==============================================================================
; Microsoft Extension INF for USB Camera Firmware Update UMDF Filter Driver
; Copyright (C) Microsoft Corporation.  All rights reserved.
;==============================================================================

[Version]
Signature="$WINDOWS NT$"
Class=Extension
ClassGUID={e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider=%CONTOSO%
ExtensionId = {BC6EE554-271C-48C8-B713-8078833962BD} ; replace with your own GUID
CatalogFile.NT = SampleExtension.cat
DriverVer=08/28/2017,10.0.1700.000

[SourceDisksFiles]
ContosoFirmwareUpdateFilterDriver.dll=1
ContosoFirmware.bin=1

[SourceDisksNames]
1 = %MediaDescription%

[DestinationDirs]
UMDriverCopy=12,UMDF ; copy to drivers\UMDF
ContosoFirmwareCopy=12,ContosoFirmware ; copy to drivers\ContosoFirmware
DefaultDestDir = 12

[UMDriverCopy]
ContosoFirmwareUpdateFilterDriver.dll

[ContosoFirmwareCopy]
ContosoFirmware.bin

[Manufacturer]
%CONTOSO% = ContosoFirmwareUpdateFilterDriver,ntamd64

[ContosoFirmwareUpdateFilterDriver.ntamd64]
; replace with your camera device VID PID
%ContosoCamera.DeviceDesc% = ContosoFirmwareUpdateFilterDriver_Install, USB\VID_1234&PID_1234&REV_1234

[ContosoFirmwareUpdateFilterDriver_Install]
CopyFiles=UMDriverCopy, ContosoFirmwareCopy

[ContosoFirmwareUpdateFilterDriver_Install.HW]
AddReg = ContosoFirmwareUpdateFilterDriver.AddReg

[ContosoFirmwareUpdateFilterDriver.AddReg]
; Load the redirector as an lower filter on this specific device.
; 0x00010008 - FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
HKR,,"LowerFilters",0x00010008,"WUDFRd"

[ContosoFirmwareUpdateFilterDriver_Install.Services]
AddService=WUDFRd,0x000001f8,WUDFRD_ServiceInstall

[WUDFRD_ServiceInstall]
DisplayName = %WudfRdDisplayName%
ServiceType = 1
StartType = 3
ErrorControl = 1
ServiceBinary = %12%\WUDFRd.sys

[ContosoFirmwareUpdateFilterDriver_Install.Wdf]
UmdfService=ContosoFirmwareUpdateFilterDriver, ContosoFirmwareUpdateFilterDriver.UmdfFilter
UmdfServiceOrder=ContosoFirmwareUpdateFilterDriver

[ContosoFirmwareUpdateFilterDriver.UmdfFilter]
UmdfLibraryVersion=2.0.0
ServiceBinary= "%12%\UMDF\ContosoFirmwareUpdateFilterDriver.dll"

[Strings]
CONTOSO = "Contoso Inc."
ContosoCamera.DeviceDesc = "Contoso Camera Extension"
MediaDescription="Contoso Camera Firmware Update Filter Driver Installation Media"
WudfRdDisplayName = "WDF Reflector Driver"
```