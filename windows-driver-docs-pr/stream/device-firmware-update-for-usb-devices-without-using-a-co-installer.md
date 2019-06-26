---
title: 设备固件更新的 USB 设备而无需使用共同安装程序
description: 概述了更新而无需辅助安装程序的 USB 设备固件的建议方法。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: b2b58da9895f456a4f8960b6cd5bfc0f89b28fa2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360190"
---
# <a name="device-firmware-update-for-usb-devices-without-using-a-co-installer"></a>设备固件更新的 USB 设备而无需使用共同安装程序

USB 设备供应商使用共同安装程序来更新设备固件对于使用收件箱 USB 设备驱动程序的设备。 但是，共同安装程序不支持由新"通用 INF"标准，这是 Windows 10 上的要求。 这是一个挑战到现有的 USB 设备固件更新过程。 本主题概述了更新而无需辅助安装程序的 USB 设备固件的建议方法。

## <a name="requirements"></a>要求

从 USB 设备固件更新过程的主要要求如下：

1. 无需用户交互的无缝的固件更新

1. 可靠的恢复机制 (例如，没有 bricking 的设备)

1. Windows 7 及更高版本的工作原理

## <a name="overview"></a>概述

在发布中字段的可更新固件时 UVC 照相机之类的 USB 设备。 没有立即更新固件的标准方法。 普遍适用于所有现有的更新机制的一件事是一些自定义软件套件在客户端上运行，并下载到设备的固件。 通常情况下，设备安装过程的一部分安装固件更新软件套件。 辅助安装程序启动启动固件更新过程。 Windows 10 上的共同安装程序缺少可防止设备供应商更新域中的这些设备上的固件。

绕过共同安装程序缺少 USB 设备固件更新方案是使用较低的筛选器驱动程序，到将启动的 USB 设备的推荐的方式启动固件更新过程。 期间[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)调用时，筛选器驱动程序将检查设备固件版本并根据需要进行更新固件。

## <a name="firmware-update-overview"></a>固件更新概述

USB 设备插入到系统，泛型收件箱驱动程序安装的设备。 安装之后的通用驱动程序，操作系统查询 Windows 更新服务器上的任何供应商特定的驱动程序包可用性并将其下载并安装驱动程序。 已安装的驱动程序包将执行固件更新。

有两种方法可以更新固件。

1. 固件更新筛选器驱动程序

    1. 供应商提供的较低的筛选器驱动程序执行固件更新。

1. 固件更新设备驱动程序

    1. 供应商提供的较低的筛选器驱动程序，将设备置于"固件更新模式"。

    1. 设备枚举为固件更新设备。

    1. 供应商提供的固件更新驱动程序将加载对此设备，并更新固件。

## <a name="method-1-firmware-update-filter-driver"></a>方法 1：固件更新筛选器驱动程序

在此方法中，将驱动程序更新过程的一部分安装 USB 设备驱动程序的较低的筛选器驱动程序。 此筛选器驱动程序将执行固件更新。

将包含 Windows 更新服务器上的驱动程序更新包：

- 固件更新 WDF 低筛选器驱动程序

- 扩展 INF 安装固件更新 WDF 较低的筛选器驱动程序

- "Firmware.bin"文件

![固件更新 UMDF 低筛选器驱动程序方法](images/fw-update-umdf-lower-filter-driver-method.png)

安装驱动程序更新包，时固件更新 WDF 筛选驱动程序的[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)将调用例程。 此例程从 WDF 筛选器驱动程序将设备固件版本从获取设备 HW 注册表项。 设备固件应已经使用 MSO 描述符到的设备硬件注册表项上的固件版本。

1. 如果设备固件版本和筛选器驱动程序预期的固件版本不同，或

1. 固件版本中不可用的设备硬件注册表项

    1. 然后，筛选器驱动程序将自身插入到设备堆栈通过返回到成功的消息[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)回调。

1. 否则，筛选器驱动程序会将自身插入设备堆栈

    1. 因为没有必要的设备具有预期的固件更新的固件。

当[EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) WDF 筛选器驱动程序回调调用在以后，筛选器驱动程序必须注册以使用 CM 设备接口更改通知\_注册\_通知或 IoRegisterPlugPlayNotification （UMDF 或 KMDF），以侦听设备接口类 USB 设备将注册到设备。 例如 RGB 照相机的固件更新筛选器驱动程序将注册为 KSCATEGORY\_视频\_照相机。 在接收通知时，筛选器驱动程序应该发布将执行固件更新工作项。

UMDF 基于固件更新驱动程序可以使用设备特定的 Api 或问题控件将传输直接以访问 USB 设备执行固件更新。 例如，照相机 UMDF 基于筛选器驱动程序会使用相机 Api 执行固件更新。

KMDF 基于固件更新驱动程序可以发送供应商特定命令来执行固件更新。

闪烁的固件完成后，设备必须断开连接并重新连接到总线。 设备将使用新固件重新枚举。

方法使用"固件更新筛选器驱动程序"，对于设备具有足够的资源以容纳两个完整的固件映像 （更新映像和备份映像） 上的设备内存的建议。 原因是如果下载已更新的固件期间出现故障，设备可以放弃该更新，并启动到其原始的固件。 因此，不 bricking 设备。

## <a name="method-2-firmware-update-device-driver"></a>方法 2：固件更新设备驱动程序

在此方法中，将驱动程序更新过程的一部分安装到 USB 设备的较低的筛选器驱动程序。 此筛选器驱动程序会将命令发送到设备固件更新模式，在重新启动设备在其中公开固件更新接口。 固件更新接口的驱动程序将加载并执行固件更新。

将包含设备的 Windows 更新服务器上的驱动程序更新包：

1. WDF 低筛选器驱动程序，将设备置于固件更新模式

1. 扩展 INF 安装 WDF 较低的筛选器驱动程序

除了驱动程序更新包，单独的固件更新设备驱动程序包将会显示在 Windows 更新，请使用：

1. WDF 固件更新设备驱动程序和其 INF 和

1. "Firmware.bin"文件中。

![固件更新 WDF 驱动程序方法](images/fw-update-wdf-driver-method.png)

安装驱动程序更新包，WDF 更低时，将调用筛选器驱动程序的 AddDevice 例程。 从该例程中，筛选器驱动程序将查询从设备 HW 注册表项的设备固件版本。 设备固件应已置于"固件版本"，使用 MSO 描述符或 USB 设备的扩展 INF，到设备硬件注册表项。

1. 如果设备固件版本和筛选器驱动程序应固件版本不一致或

1. 固件版本中不可用的设备硬件注册表项

1. 然后，WDF 筛选器驱动程序将自身插入到设备堆栈。

1. 否则，WDF 筛选器驱动程序会将自身插入设备堆栈

当[EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) WDF 筛选器驱动程序回调调用在以后，筛选器驱动程序将发出一个供应商特定命令到设备会将它置于固件更新模式。 即设备将断开连接并重新连接，公开该固件更新接口。

系统将枚举固件更新设备接口。 由供应商，固件更新包中提供的自定义的固件更新 WDF 驱动程序将加载此固件更新接口。 此驱动程序将更新的固件。

当[EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)在稍后的某个时刻调用回调 WDF 固件更新驱动程序、 驱动程序必须发布将执行固件更新工作项。

闪烁的固件完成后，设备必须断开连接并重新连接到总线。 设备将使用新固件重新枚举。

建议使用此方法不能在设备上保存由于内存不足的更新和原始的固件映像的设备。 原因是如果在下载已更新的固件期间出现故障，设备可以放弃该更新并重新启动到其固件更新模式的设备和固件更新可以重试。 因此，不 bricking 设备。

## <a name="recovery"></a>恢复

固件更新过程可能会出于各种原因而失败。 如果出现这种情况，当再次枚举设备时，固件更新驱动程序可能会尝试再次更新固件可能再次失败和此更新过程的最终可能会在循环中。 固件更新驱动程序必须让它可以执行的重试次数上限。 固件更新时重试获取超出了阈值 （例如，试 3 次），则筛选器驱动程序不应尝试更新固件试，直到从 WU 下载新版本的驱动程序。 固件更新驱动程序可能使用注册表来保留重试状态。

在进行设备固件更新结束时，我们建议在设备重置，并重新枚举。

这两种方法的固件更新，必须在执行固件更新之前停止设备函数。 这可确保有到设备的任何打开句柄，并避免任何操作系统重新启动要求。

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
