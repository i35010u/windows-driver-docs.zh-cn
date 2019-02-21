---
title: 安装筛选器驱动程序
description: 安装筛选器驱动程序
ms.assetid: 48ffa6db-3254-4108-b8bb-5884b9168a9d
keywords:
- 设备安装程序 WDK 设备安装，筛选器驱动程序
- 设备安装 WDK，筛选器驱动程序
- 安装设备 WDK，筛选器驱动程序
- 筛选器驱动程序 WDK 设备安装
- 特定于设备的筛选器驱动程序 WDK 设备安装
- 类筛选器驱动程序 WDK 设备安装
- SetupInstallFilesFromInfSection
- UpperFilters
- LowerFilters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02b1d844be1a359d193adf3a17f59f4f31155b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546130"
---
# <a name="installing-a-filter-driver"></a>安装筛选器驱动程序





即插即用的筛选器驱动程序可以支持特定设备或所有设备安装程序类中，并可以将附加以下设备的功能驱动程序 （较低筛选器） 或更高版本设备的功能驱动程序 （上部筛选器）。 请参阅[WDM 驱动程序类型](https://msdn.microsoft.com/library/windows/hardware/ff564862)有关即插即用驱动程序层的详细信息。

### <a href="" id="ddk-installing-a-device-specific-filter-driver-dg"></a>安装特定于设备的筛选器驱动程序

若要注册的设备特定的筛选器驱动程序，创建注册表项，通过**AddReg**中的条目<em>DDInstall</em>**。HW**设备的 INF 文件部分。 对于特定于设备的上层筛选器，创建一个名为词条**上边的筛选程序**。 对于特定于设备的低层筛选器，创建一个名为词条**下边的筛选程序**。 例如，将安装以下 INF 摘录*cdaudio*作为上的上限筛选器*cdrom*驱动程序：

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

### <a href="" id="ddk-installing-a-class-filter-driver-dg"></a>安装类筛选器驱动程序

若要安装类范围上限的或较低的筛选器安装必要的服务的设备安装程序类。 应用程序然后可以将此服务注册为正在上限-或较低的筛选器所需的设备安装程序类。 若要复制的服务二进制文件，该应用程序可以使用**SetupInstallFilesFromInfSection**。 若要安装的服务，该应用程序可以使用**SetupInstallServicesFromInfSection**。 若要注册服务作为上限和/或特定设备安装程序类的较低筛选器，在应用程序调用**SetupInstallFromInfSection**感兴趣的每个设备安装程序类，使用注册表项句柄是在检索从[ **SetupDiOpenClassRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552065)有关*RelativeKeyRoot*参数。 例如，考虑以下 INF 部分：

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

设备安装应用程序，则应该：

1.  调用**SetupInstallFilesFromInfSection**有关\[upperfilter_inst\]部分。

2.  调用**SetupInstallServicesFromInfSection**为\[upperfilter_inst。服务\]部分。

3.  调用**SetupInstallFromInfSection**有关\[upperfilter_inst\]部分中，一旦它想要注册的每个类键*upperfilt*服务。

将指定每次调用**SPINST_REGISTRY**有关*标志*参数，以指示需要执行仅注册表修改。

 

 





