---
title: 存储固件更新 (SFU) 驱动程序
description: 提供存储固件更新 (SFU) 驱动程序的实现细节。
ms.date: 10/07/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 9cec200580ec0ed1ee2b4e9fac6e54475fd110b8
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349785"
---
# <a name="storage-firmware-update-sfu-driver"></a>存储固件更新 (SFU) 驱动程序

更新 NVMe 存储驱动器的固件依赖于硬件供应商创建固件更新应用程序，该应用程序利用 Windows 10 中引入的特定 [固件更新 IOCTLs](/windows/win32/fileio/working-with-nvme-devices#dont-update-firmware-through-the-pass-through-mechanism) 。 通常，这些应用程序在 Windows 更新 (WU) 管道之外分发。 最终用户需要确定哪些存储磁盘在其设备中，从制造商的网站中获取正确的存储驱动器固件实用程序，然后手动下载和安装更新。

此外，在 [S 模式下运行 Windows 10](https://www.microsoft.com/windows/s-mode)的设备采用增强的安全配置，只允许用户运行经过 Microsoft 验证的应用程序，因此供应商实用程序可能无法更新驱动器固件。 这一手动流程可降低固件更新的采用，提高硬件制造商的支持成本和客户满意度问题。

> [!NOTE]
> Windows 10 in 模式仅适用于 Windows 中的 Microsoft Store 应用和在 S 模式下兼容 Windows 10 的附件。 有一种单向交换机可用。 有关详细信息，请参阅 [windows.com/SmodeFAQ](https://support.microsoft.com/help/4020089)。

使用基于驱动程序的解决方案的[Windows 更新 (WU) 服务更新设备固件](../install/updating-device-firmware-using-windows-update.md)适用于硬件供应商，并要求它们将固件更新逻辑和负载添加到现有函数驱动程序，或者提供单独的固件更新驱动程序和包。 这将导致重复跨硬件合作伙伴工作，并增加存储驱动器的总体服务成本。 有关通用驱动程序的详细信息，请参阅 [具有通用 Windows 驱动程序的入门](../develop/getting-started-with-windows-drivers.md)。

使用 Windows 10 版本 2004 (OS 版本19041.488 或更高版本时) 可以使用 Microsoft 提供的驱动程序和硬件供应商提供的固件更新包更新 NVMe 驱动器固件。 此解决方案可通过 Windows 更新 [ (CHIDs) 上使用计算机硬件 id ](../install/specifying-hardware-ids-for-a-computer.md)的目标驱动器和设备进行分发。

> [!WARNING]
> 固件更新是一种潜在的危险维护操作，只应在对新固件映像进行全面测试后分发。 不受支持的硬件上的新固件可能对可靠性和稳定性产生负面影响，或者甚至会导致数据丢失。

## <a name="drive-compatibility"></a>驱动器兼容性

若要使用 Windows 10 更新驱动器固件，你必须具有受支持的驱动器。 为确保常见的设备行为，Windows 10 为 NVMe 设备指定了可选的硬件实验室工具包 (HLK) 要求。 这些要求概述了 NVMe 存储驱动器必须支持使用基于 Windows 更新的新解决方案进行固件更新的命令。

有关硬件是否支持 Windows 更新驱动器固件的信息，请与解决方案供应商联系。

### <a name="windows-device-compat-requirements-for-nvme-devicestoragecontrollerdrivenvme---sections-57-and-58"></a>NVMe： ControllerDrive 的 Windows 设备兼容要求-5.7 和5.8 节

**ControllerDrive.. BasicFunction**

设备必须至少有一个可升级固件槽。

**5.7 固件提交**

- 应在不需要设备电源周期的情况下执行固件映像激活。

- 应通过主机启动的重置来实现激活过程，如 spec 版本 1.2 a 8.1 中所述。

- 发出固件提交命令时，Windows 将使用提交操作001b 或010b。

- 在没有电源周期的情况下成功激活的预期完成值为 00h (一般成功) 、10h 或11h。

- 如果0Bh 作为完成状态返回，Windows 将通知用户执行设备的电源周期。 强烈建议不要这样做，因为它会阻止在操作系统运行时更新固件并导致重大的工作负荷中断。

**5.8 固件映像下载**

- 设备在下载阶段不能出现 i/o 故障，并应继续为 i/o 提供服务。

有关更多详细信息，请参阅 NVMe： ControllerDrive 的 Windows 设备兼容要求 [-5.7 和5.8 节](https://partner.microsoft.com/dashboard/collaborate/packages/7840)。

> [!NOTE]
> 上述链接需要 [Microsoft 协作](https://developer.microsoft.com/dashboard/collaborate/) 门户上的有效帐户。

## <a name="scsi-identifiers-for-nvme-storage-disk-drives"></a>用于 NVMe 存储磁盘驱动器的 SCSI 标识符

从 Windows 10 版本2004开始，版本 (操作系统版本19041.488 或更高版本) ，使用支持 [STOR_RICH_DEVICE_DESCRIPTION](/windows-hardware/drivers/ddi/storport/ns-storport-_stor_rich_device_description) 结构的驱动程序的设备存储磁盘驱动器有两个新的标识符：

`SCSI\t*v(8)p(40)`

其中：

- t * 是可变长度的设备类型代码。
- v (8) 是8个字符的供应商标识符。
- p (40) 是40字符产品标识符

`SCSI\t*v(8)p(40)r(8)`

其中：

- t * 是可变长度的设备类型代码。
- v (8) 是8个字符的供应商标识符。
- p (40) 是40字符产品标识符
- r (8) 是8个字符的修订级别值。

`SCSI\t*v(8)p(40)r(80`标识符提供了一个完整的产品名称 (与 NVME 1.4 spec) 一致，并允许创建软件组件 (SWC) 节点来更新与该名称匹配的 NVME 驱动器的固件更新 (最多40个字符，8个字符固件版本) 。

有关详细信息，请参阅 [SCSI 设备的标识符](../install/identifiers-for-scsi-devices.md) 和 [STOR_RICH_DEVICE_DESCRIPTION](/windows-hardware/drivers/ddi/storport/ns-storport-_stor_rich_device_description)

## <a name="storage-firmware-update-sfu-solution-details"></a>存储固件更新 (SFU) 解决方案详细信息

在下图中，Windows 10 提供了功能驱动程序 ( # A0) 和固件更新驱动程序 ( # A1) 。 若要利用 Microsoft 提供的驱动程序更新 NVMe 驱动器固件，需要两个单独的驱动程序提交。

![存储固件更新详细信息](images/storage-firmware-update-detail.png)

### <a name="package-1---create-identity-for-drive-firmware-update"></a>包 1-创建驱动器固件更新的标识

通常，此包包含以下内容：

- 用于创建软件设备节点的扩展 INF，用作固件更新包的独立目标硬件

- 驱动程序目录

提交扩展 INF 包作为单独的驱动程序提交。

但许多设备类型不允许单个物理设备枚举多个设备节点。 在这种情况下，请使用指定 [AddComponent](../install/inf-addcomponent-directive.md) 指令的扩展 INF，以创建可 Windows 更新并在其上安装固件更新驱动程序的设备节点。 INF 文件中的以下代码片段显示了如何执行此操作：

```inf
[Manufacturer]
%Contoso%=Standard,NTamd64
[Standard.NTamd64]
%DeviceName%=Device_Install, SCSI\DiskNVMe____StorageIHVabcd
[StorageIHVabcd.Components]
AddComponent= StorageIHVabcd_component,,StorageIHVabcd_ComponentInstall
[StorageIHVabcd_ComponentInstall]
ComponentIDs = StorageIHVabcd-firmware-update
```

在上述 INF 示例中， `ComponentIDs = StorageIHVabcd-firmware-update` 指示子设备的硬件 ID 为 **SWC\StorageIHVabcd-firmware-update** 。 安装此 INF 后，会创建以下设备层次结构：

![I N F 设备层次结构](images/inf-device-hierarchy.png)

下面提供了用于为驱动器固件更新创建新标识的示例扩展 INF。 由于 **SCSI \ DiskNVMe____StorageIHVabcd** 硬件在硬件制造商内可能不是唯一的，因此扩展 INF 必须使用 [子](../install/specifying-hardware-ids-for-a-computer.md) 目标来进行分发。

### <a name="package-2---drive-firmware-update-package"></a>包 2-驱动器固件更新包

通常，此包包含以下内容：

- 类固件的通用驱动程序 INF

- 固件更新负载二进制

- 驱动程序目录

提交固件包作为单独的驱动程序提交。

驱动器固件更新包 INF 以新节点 **SWC\StorageIHVabcd-firmwareupdate** 为目标，并调用 Windows 10 存储固件更新驱动程序。 要使软件枚举的组件设备正常运行，必须启动其父项。 为了使用 StorFwUpdate 驱动器，开发人员应将每个可能的部分的 [DDInstall 部分](../install/inf-ddinstall-section.md) 中的 Include/需求 INF 指令用于如下 `[DDInstall.*]` `[StorFwUpdate.*]` 所示的相应部分，而不考虑 INF 是否为该部分指定了任何指令：

```inf
[StorFwUpdateOem.NT]
Include            = StorFwUpdate.inf
Needs              = StorFwUpdate.NT
CopyFiles          = StorFwUpdateOem.CopyFiles

[StorFwUpdateOem.NT.Wdf]
Include            = StorFwUpdate.inf
Needs              = StorFwUpdate.NT.Wdf

[StorFwUpdateOem.NT.Services]
Include            = StorFwUpdate.inf
Needs              = StorFwUpdate.NT.Services
```

有关详细信息，请参阅 [使用组件 INF 文件](../install/using-a-component-inf-file.md)。 下面提供了一个示例 NVMe 驱动器固件更新 INF 文件。 由于 **SWC\StorageIHVabcd-firmwareupdate** 软件标识在硬件制造商内可能不唯一，因此 INF 必须利用 [子](../install/specifying-hardware-ids-for-a-computer.md) 目标来实现 Windows 更新分布。

StorFwUpdate 组件不会执行任何验证 (签名验证或固件二进制负载的解密) 。 如果需要此级别的功能，则硬件伙伴可以编写自己的存储固件更新驱动程序。

## <a name="storage-drive-firmware-update-example"></a>存储驱动器固件更新示例

由于这两个 Inf 都需要 CHIDs 进行 Windows 更新分发，因此硬件合作伙伴可以使用 PNPUTIL.EXE 本地验证解决方案，如下所示。

### <a name="requirements"></a>要求

- Windows 10 版本 2004 (OS 版本19041.488 或更高版本) 

- 带有 NVMe 存储驱动器的设备使用收件箱 stornvme.sys 驱动程序

- NVMe 驱动器固件二进制

- 已正确编写 INF 文件

### <a name="view-current-nvme-disk-firmware-version"></a>查看当前 NVMe 磁盘固件版本

查看当前 NVMe 磁盘固件版本：

1. 以管理员身份打开 Powershell 窗口。

1. 键入 `Get-PhysicalDisk | Get-StorageFirmwareInformation` 以查看当前 NVMe 磁盘固件版本。

    ![当前的 N V M e 磁盘固件版本](images/media2-1.png)

请注意当前的 **ActiveSlotNumber** 和 **FirmwareVersionInSlot** 值。

有关详细信息，请参阅 [StorageFirmwareInformation](/powershell/module/storage/get-storagefirmwareinformation?view=win10-ps&preserve-view=true)。

### <a name="install-the-extension-inf-to-create-new-software-hardware-identity"></a>安装扩展 INF 以创建新软件硬件标识

1. 转到系统上包含驱动程序扩展包 INF 文件的目录。 例如，键入 `cd .\signed-DiskExtnPackage\`。

1. 验证扩展 INF 文件是否包含正在更新的驱动器的信息。 有关扩展 INF 示例，请参阅本主题中的 [磁盘扩展 inf 文件](#disk-extension-inf-sample) 。

1. 通过 Microsoft PnP 实用程序安装扩展 INF。 例如，在管理员命令提示符下，键入 `pnputil /add-driver .\OEMDiskExtnPackage.inf /install` 。 由于新的软件节点是作为启动关键设备的子级创建的，因此需要重启才能生效。

    ![ p n p util 命令输出](images/media3-2.png)

### <a name="view-the-new-software-component-swc-node"></a> (SWC) 节点上查看新的软件组件

查看新的 SWC 节点和硬件 ID：

1. 在 Windows 10 "开始" 菜单中，打开 **"控制面板** "，然后打开 **设备管理器** 。

1. 在设备管理器中，选择 " **磁盘驱动器** "，然后展开节点并选择已更新的磁盘驱动器。

1. 选择已更新的驱动器后，在 " **设备管理器****视图** " 菜单中选择 " **按连接设备** "。

1. 单击所选驱动器节点，然后单击以展开。 你将在 "驱动器" 节点下看到一个子 **通用软件组件** 。

1. 右键单击 **一般软件组件** ，然后单击 " **属性** "。

1. 在 " **属性** " 对话框窗口中，选择 " **详细信息** " 选项卡，然后从 " **属性** " 下拉列表中选择 " **硬件 id** "，查看 "驱动器" 节点上 **通用软件组件** 的硬件 id。

1. SWC \\ * 硬件 Id 应与扩展 INF 中指定的 Id 相同。

### <a name="view-and-install-the-nvme-disk-firmware-update"></a>查看并安装 NVMe 磁盘固件更新

1. 以管理员身份打开 Powershell 窗口。

1. 转到系统中包含 NVMe 磁盘固件更新 INF 文件的目录。 例如，键入 `cd .\signed-ihv-firmware\`。

1. 验证磁盘固件更新 INF 是否包含正在更新的驱动器的信息。 有关磁盘固件更新的示例，请参阅本主题中的 [磁盘固件 INF 文件](#disk-firmware-inf-sample) 。

1. 通过 Microsoft PnP 实用程序安装磁盘固件更新 INF。 例如，在管理员命令提示符下，键入 `pnputil /add-driver .\StorFwUpdateIHV.inf /install` 。

1. 以管理员身份打开 Powershell 窗口。

1. 键入 `Get-PhysicalDisk | Get-StorageFirmwareInformation` 以查看更新的 NVMe 磁盘固件信息。

    ![已更新 N V M e 磁盘固件](images/media5-4.png)

在 **ActiveSlotNumber** 和 **FirmwareVersionInSlot** 值中查看更新的 NVMe 磁盘固件信息。

有关详细信息，请参阅 [StorageFirmwareInformation](/powershell/module/storage/get-storagefirmwareinformation?view=win10-ps&preserve-view=true)。

## <a name="deploy-the-extension-inf-and-firmware-packages-through-windows-update"></a>通过 Windows 更新部署扩展 INF 和固件包

首先，通过使用 [发布测试分发](../dashboard/publishing-for-test-distribution.md) 指南 Windows 更新来验证包部署。

接下来，使用适当的 CHIDs 通过 Windows 更新部署包。

有关部署的信息，请参阅 [Windows 10 驱动程序发布工作流 (.docx 下载) ](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)。

## <a name="disk-extension-inf-sample"></a>磁盘扩展 INF 示例

下面是扩展 INF 文件的示例：

```inf
;/*++
;
;  Copyright (c) Microsoft Corporation.  All rights reserved.
;
;      THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY
;      KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
;      IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR
;      PURPOSE.
;
;  File:
;
;      OEMDiskExtnPackage.inx
;
;  Description:
;
;      INF file for installing the OEMDiskExtnPackage. This will create a SWC\ DevNode
;      which will service as the target HWID for the Disk storage firmware package.
;
;--*/

[Version]
Signature="$Windows NT$"
Class = Extension
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider=%ManufacturerName%
ExtensionId = {D91908BD-43FA-411B-92A1-C378AE5AF9FA}
CatalogFile=delta.cat
DriverVer = 08/26/2019,1.0.0.0

[SourceDisksNames]
1 = %DiskName%

[Manufacturer]
%ManufacturerName%=Standard,NTamd64

[Standard.NTamd64]
%OEMDiskExtnPackage.DeviceDesc%=StorageIHV1-87B, SCSI\DiskNVMe____StorageIHV1-87B
%OEMDiskExtnPackage.DeviceDesc%=StorageIHV1-87A, SCSI\DiskNVMe____StorageIHV1-87A
%OEMDiskExtnPackage.DeviceDesc%=StorageIHV2_KUS02020, SCSI\DiskNVMe____StorageIHV2_KUS02020
%OEMDiskExtnPackage.DeviceDesc%=StorageIHV3_KBG40ZPZ512G, SCSI\DiskNVMe____KBG40ZPZ512G_IHV300Y9
%OEMDiskExtnPackage.DeviceDesc%=StorageIHV3_KBG40ZPZ512G, SCSI\DiskNVMe____KBG40ZPZ512G_IHV30015

[StorageIHV1-87B.NT]
[StorageIHV1-87B.NT.Components]
AddComponent = StorageIHV1-87B_component,,StorageIHV1-87B_ComponentInstall

[StorageIHV1-87B_ComponentInstall]
ComponentIds=StorageIHV1-87B

[StorageIHV1-87A.NT]
[StorageIHV1-87A.NT.Components]
AddComponent = StorageIHV1-87A_component,,StorageIHV1-87A_ComponentInstall

[StorageIHV1-87A_ComponentInstall]
ComponentIds=StorageIHV1-87A

[StorageIHV2_KUS02020.NT]
[StorageIHV2_KUS02020.NT.Components]
AddComponent = StorageIHV2_KUS02020_component,,StorageIHV2_KUS02020_ComponentInstall

[StorageIHV2_KUS02020_ComponentInstall]
ComponentIds=StorageIHV2_KUS02020

[StorageIHV3_KBG40ZPZ512G.NT]
[StorageIHV3_KBG40ZPZ512G.NT.Components]
AddComponent = StorageIHV3_KBG40ZPZ512G_component,,StorageIHV3_KBG40ZPZ512G_ComponentInstall

[StorageIHV3_KBG40ZPZ512G_ComponentInstall]
ComponentIds=StorageIHV3_KBG40ZPZ512G

;*****************************************
; Strings section
;*****************************************

[Strings]
ManufacturerName = "OEM"
DiskName = "OEM Disk Extn package Installation Disk"
OEMDiskExtnPackage.DeviceDesc = "Disk Extn Package"
OEMDiskExtnPackage.SVCDESC = "Disk Extn Package"

;Non-Localizable
REG_EXPAND_SZ          = 0x00020000
REG_DWORD              = 0x00010001
REG_MULTI_SZ           = 0x00010000
REG_BINARY             = 0x00000001
REG_SZ                 = 0x00000000

SERVICE_KERNEL_DRIVER  = 0x1
SERVICE_ERROR_IGNORE   = 0x0
SERVICE_ERROR_NORMAL   = 0x1
SERVICE_ERROR_SEVERE   = 0x2
SERVICE_ERROR_CRITICAL = 0x3
```

## <a name="disk-firmware-inf-sample"></a>磁盘固件 INF 示例

下面是一个示例磁盘固件 INF 文件：

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
;   File:
;
;      StorageIHV3-Firmware-Update.inx
;
;   Description:
;
;      Driver installation file for firmware update.
;
;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

[Version]
Signature="$Windows NT$"
Class=Firmware
ClassGuid={f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
Provider=%ManufacturerName%
CatalogFile=delta.cat
DriverVer = 08/26/2019,11.37.9.948
PnPLockDown=1

[SourceDisksNames]
1= %DiskName%

[DestinationDirs]
StorFwUpdateOem.CopyFiles=13

[Manufacturer]
%ManufacturerName%=Standard,NTamd64

[Standard.NTamd64]
%StorFwUpdateOem.DeviceDesc%=StorFwUpdateOem, SWC\StorageIHV3_KBG40ZPZ512G

[StorFwUpdateOem.NT]
Include            = StorFwUpdate.inf
Needs              = StorFwUpdate.NT
CopyFiles          = StorFwUpdateOem.CopyFiles

[StorFwUpdateOem.NT.Wdf]
Include            = StorFwUpdate.inf
Needs              = StorFwUpdate.NT.Wdf

[StorFwUpdateOem.NT.HW]
AddReg = StorFwUpdateOem_HWAddReg

[StorFwUpdateOem_HWAddReg]
HKR,,FriendlyName,,%FwUpdateFriendlyName%

; Specify the location of the firmware offer and payload file in the registry.
; The files are kept in driver store. When deployed, %13% would be expanded to the actual path
; in driver store.
;
HKR,0D9EB3D6-6F14-4E8A-811B-F3B19F7ED98A\0,FirmwareImageVersion, 0x00000000, "AEMS0102"
HKR,0D9EB3D6-6F14-4E8A-811B-F3B19F7ED98A\0,FirmwareFileName, 0x00000000, %13%\AEMS0102.sig

[SourceDisksFiles]
AEMS0102.sig=1

[StorFwUpdateOem.CopyFiles]
AEMS0102.sig

[StorFwUpdateOem.NT.Services]
Include            = StorFwUpdate.inf
Needs              = StorFwUpdate.NT.Services

; =================== Generic ==================================

[Strings]
ManufacturerName="{Your Manufacturer Name}"
StorFwUpdateOem.DeviceDesc = "Storage Firmware Update (StorageIHV3) 1"
DiskName = "Storage Firmware Update Installation Disk"
FwUpdateFriendlyName= "StorageIHV3 Firmware Update"
```

## <a name="additional-resources"></a>其他资源

[SCSI 设备的标识符](../install/identifiers-for-scsi-devices.md)

[STOR_RICH_DEVICE_DESCRIPTION](/windows-hardware/drivers/ddi/storport/ns-storport-_stor_rich_device_description)