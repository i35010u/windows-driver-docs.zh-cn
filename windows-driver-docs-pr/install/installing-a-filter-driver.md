---
title: 安装筛选器驱动程序
description: 安装筛选器驱动程序
ms.assetid: 48ffa6db-3254-4108-b8bb-5884b9168a9d
keywords:
- 设备设置 WDK 设备安装，筛选器驱动程序
- 设备安装 WDK，筛选器驱动程序
- 安装设备 WDK，筛选器驱动程序
- 筛选器驱动程序 WDK 设备安装
- 设备特定的筛选器驱动程序 WDK 设备安装
- 类筛选器驱动程序 WDK 设备安装
- SetupInstallFilesFromInfSection
- UpperFilters
- LowerFilters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e1fd1a586e0968dc216f7ba29c516d12bb146c8
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361313"
---
# <a name="installing-a-filter-driver"></a>安装筛选器驱动程序





PnP 筛选器驱动程序可以支持特定设备或安装程序类中的所有设备，并可附加到设备的功能驱动程序 (更低的筛选器) 或高于设备的函数驱动程序 (上限筛选) 。 有关 PnP 驱动程序层的详细信息，请参阅 [WDM 驱动程序的类型](../kernel/types-of-wdm-drivers.md) 。

### <a name="installing-a-device-specific-filter-driver"></a><a href="" id="ddk-installing-a-device-specific-filter-driver-dg"></a>安装 Device-Specific 筛选器驱动程序

若要注册特定于设备的筛选器驱动程序，请通过 <em>DDInstall</em>中的 **AddReg** 项创建一个注册表项 **。** 设备 INF 文件的硬件部分。 对于特定于设备的筛选器，请创建名为 **UpperFilters** 的条目。 对于特定于设备的低筛选器，请创建名为 **LowerFilters** 的条目。 例如，以下 INF 摘录将 *cdaudio* 安装为 *cdrom* 驱动程序上的上限筛选器：

```cpp
:
; Installation section for cdaudio. Sets cdrom as the service 
; and adds cdaudio as a PnP upper filter driver. 
;
[cdaudio_install]
CopyFiles=cdaudio_copyfiles, cdrom_copyfiles
 
[cdaudio_install.HW]
AddReg=cdaudio_addreg
 
[cdaudio_install.Services]
AddService=cdrom,0x00000002,cdrom_ServiceInstallSection
AddService=cdaudio,,cdaudio_ServiceInstallSection
: 

[cdaudio_addreg] 
HKR,,"UpperFilters",0x00010000,"cdaudio" ; REG_MULTI_SZ value 
:

[cdaudio_ServiceInstallSection]
DisplayName    = %cdaudio_ServiceDesc%
ServiceType    = 1     ; SERVICE_KERNEL_DRIVER
StartType      = 3     ; SERVICE_DEMAND_START
ErrorControl   = 1     ; SERVICE_ERROR_NORMAL
ServiceBinary  = %12%\cdaudio.sys
:
```

### <a name="installing-a-class-filter-driver"></a><a href="" id="ddk-installing-a-class-filter-driver-dg"></a>安装类筛选器驱动程序

若要为 [设备安装程序类](./overview-of-device-setup-classes.md)安装类级或更低级别的筛选器，可以提供安装所需服务的 *设备安装应用程序* 。 然后，应用程序可以将该服务注册为所需的设备安装程序类的上限筛选器或下限筛选器。 若要复制服务二进制文件，应用程序可以使用 **SetupInstallFilesFromInfSection** 。 若要安装服务，应用程序可以使用 **SetupInstallServicesFromInfSection** 。 若要将服务注册为特定设备安装程序类的上限和/或下限筛选器，应用程序将使用从 [**SetupDiOpenClassRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkey)为 *RelativeKeyRoot* 参数检索到的注册表项句柄，为相关的每个设备安装程序类调用 **SetupInstallFromInfSection** 。 例如，请考虑以下 INF 部分：

```cpp
:

[DestinationDirs]
upperfilter_copyfiles = 12

[upperfilter_inst]
CopyFiles = upperfilter_copyfiles
AddReg = upperfilter_addreg

[upperfilter_copyfiles]
upperfilt.sys,,,0x00004000  ; COPYFLG_IN_USE_RENAME

[upperfilter_addreg]
; append this service to existing REG_MULTI_SZ list, if any
HKR,,"UpperFilters",0x00010008,"upperfilt" 

[upperfilter_inst.Services]
AddService = upperfilt,,upperfilter_service

[upperfilter_service]
DisplayName   = %upperfilter_ServiceDesc%
ServiceType   = 1   ; SERVICE_KERNEL_DRIVER
StartType     = 3   ; SERVICE_DEMAND_START
ErrorControl  = 1   ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\upperfilt.sys
:
```

设备安装应用程序将：

1.  为 **SetupInstallFilesFromInfSection** \[ Upperfilter_inst 节调用 SetupInstallFilesFromInfSection \] 。

2.  为 **SetupInstallServicesFromInfSection** Upperfilter_inst 调用 SetupInstallServicesFromInfSection \[ 。服务 \] 部分。

3.  **SetupInstallFromInfSection** \[ \] 对于 upperfilter_inst 节，为它要为其注册 *upperfilt* 服务的每个类键调用 SetupInstallFromInfSection。

每次调用都会为 *Flags* 参数指定 **SPINST_REGISTRY** ，以指示只需执行注册表修改。

