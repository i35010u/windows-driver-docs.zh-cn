---
title: INF DDInstall.HW 节
description: DDInstall.HW 部分通常用于安装多功能设备的、 用于安装即插即用的筛选器驱动程序，以及用于设置在注册表中，任何用户访问的特定于设备的但独立于驱动程序的信息是否显式 AddReg指令或使用 Include 和需求条目。
ms.assetid: 417a4ab0-9723-4b3b-aa8c-342598874d61
keywords:
- INF DDInstall.HW 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.HW Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23052d536b36ab488c793e9b70ee9fecc019d951
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377917"
---
# <a name="inf-ddinstallhw-section"></a>INF DDInstall.HW 节


<em>DDInstall</em>**。HW**部分通常用于安装多功能设备的、 用于安装即插即用的筛选器驱动程序，以及用于设置在注册表中，任何用户访问的特定于设备的但独立于驱动程序的信息是否显式[**AddReg** ](inf-addreg-directive.md)指令或使用**Include**并**需要**条目。

```ini
[install-section-name.HW] |
[install-section-name.nt.HW] |
[install-section-name.ntx86.HW] |
[install-section-name.ntarm.HW] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.HW] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.HW] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.HW]  (Windows XP and later versions of Windows)
 
[AddReg=add-registry-section[,add-registry-section]...] ...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[DelReg=del-registry-section[,del-registry-section]...] ...
[BitReg=bit-registry-section[,bit-registry-section] ...] 
```

## <a name="entries"></a>条目


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=**<em>add-registry-section</em>\[**,**<em>add-registry-section</em>\]...  
引用了一个或多 INF 编写器的定义*添加注册表部分*涵盖此设备的 INF 文件中的其他位置<em>DDInstall</em>**。HW**部分。 *添加注册表部分*通常安装筛选器和/或存储在注册表中的每个设备的信息。 **HKR**在此类规范*添加注册表部分*指定的设备*硬件密钥*，包含有关的信息特定于设备的注册表子项设备。 硬件密钥也称为设备密钥。 有关详细信息，请参阅[注册表树和设备和驱动程序的密钥](https://docs.microsoft.com/windows-hardware/drivers/install/registry-trees-and-keys)。 驱动程序包可以使用添加设置通过 INF **HKR**中引用的一个添加的注册表-部分规范**DDInstall.HW 部分**。 

有关详细信息，请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include=**<em>filename</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
指定一个或多个其他系统提供 INF 文件包含安装此设备所需的部分。 如果指定此项时，通常那么**需要**条目。

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
指定必须在此设备的安装过程中处理命名的部分。 通常情况下，此类指定的部分是<em>DDInstall</em>**。HW**中列出系统提供 INF 文件中的节**Include**条目。 但是，它可以是任何部分此类中被引用<em>DDInstall</em>**。HW**包含 INF 部分。

**需要**条目不能嵌套。 有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=**<em>del-registry-section</em>\[**,**<em>del-registry-section</em>\]...  
引用了一个或多 INF 编写器的定义*删除注册表部分*其他位置中的设备驱动程序的 INF 文件受*DDInstall*部分。 此类删除注册表部分从目标计算机中删除以前安装的设备/驱动程序的旧注册信息。 **HKR**规范删除注册表节中的指定与相同的子项**AddReg**。

很少使用此指令，但在 INF 文件中每个制造商中每个列出以前安装的每个模型的设备相同的升级-*模型*定义的此名称的部分*DDInstall*部分。 有关详细信息，请参阅[ **INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section-----"></a>**BitReg=**<em>bit-registry-section</em>\[**,**<em>bit-registry-section</em>\] ...  
在本部分中中, 有效，但几乎从不使用。 **HKR**规范引用位注册表部分中的指定与相同的子项**AddReg**。 有关详细信息，请参阅[ **INF BitReg 指令**](inf-bitreg-directive.md)。

<a name="remarks"></a>备注
-------

不区分大小写的扩展*安装的部分名称*所示在正式语法语句可插入到此类<em>DDInstall</em>**。HW**跨平台 INF 文件中的节名称。 有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

任何<em>DDInstall</em>**。HW**部分必须具有以下项之一：

- **AddReg**指令。
- **Include**指定另一个 INF 文件的条目。 在这种情况下， <em>DDInstall</em>**。HW**部分中还必须包含相应**需要**其他 INF 文件中指定的部分的条目。 本部分中用于设置必需的注册表信息。

中的每个指令<em>DDInstall</em>**。HW**部分可以引用多个 INF 编写器定义部分。 但是，必须用逗号 （，） 分隔每个其他的指定的部分。

每个此类部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

有关如何安装多功能设备的详细信息，请参阅[支持多功能设备](https://msdn.microsoft.com/library/windows/hardware/ff542743)。

<a name="examples"></a>示例
--------

此示例演示如何使用 CD-ROM 设备类安装程序<em>DDInstall</em>**。HW**各节和<em>DDInstall</em>**。服务**部分以通过创建相应的注册表部分中，并设置这些设置作为即插即用上部的筛选器驱动程序支持这两个 CD 音频和换带机功能。

```ini
;;
;; Installation section for cdaudio. Sets cdrom as the service 
;; and adds cdaudio as a PnP upper filter driver. 
;;
[cdaudio_install]
CopyFiles=cdaudio_copyfiles,cdrom_copyfiles

[cdaudio_install.HW]
AddReg=nosync_addreg,cdaudio_addreg
 ; cdaudio_addreg required to register this as a PnP filter driver

[cdaudio_install.Services]
AddService=cdrom,0x00000002,cdrom_ServiceInstallSection
AddService=cdaudio,,cdaudio_ServiceInstallSection

[changer_install]
CopyFiles=changer_copyfiles,cdrom_copyfiles

[changer_install.HW]
AddReg=changer_addreg

; ... changer_install.Services section similar to cdaudio's

; ... some similar cdrom_install(.HW)/addreg sections omitted 

[cdaudio_addreg] ; changer_addreg section has similar entry
HKR,,"UpperFilters",0x00010000,"cdaudio" ; [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) value 

;
; Use next section to disable synchronous transfers to this device. 
; Sync transfers will always be turned off by default in this INF 
; for any cdrom-type device.
;
[nosync_addreg]
HKR,,"DefaultRequestFlags",0x00010001,8

[autorun_addreg]
HKLM,"System\CurrentControlSet\Services\cdrom","AutoRun",0x00010003,1
;;
;; service-install sections for cdrom, cdaudio, and changer
;;
[cdrom_ServiceInstallSection]
DisplayName    = %cdrom_ServiceDesc%
ServiceType    = 1
StartType      = 1
ErrorControl   = 1
ServiceBinary  = %12%\cdrom.sys
LoadOrderGroup = SCSI CDROM Class
AddReg         = autorun_addreg

[cdaudio_ServiceInstallSection]
DisplayName    = %cdaudio_ServiceDesc%
ServiceType    = 1
StartType      = 1
ErrorControl   = 1
ServiceBinary  = %12%\cdaudio.sys

; ... changer_ServiceInstallSection similar to cdaudio's
```

## <a name="see-also"></a>请参阅


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






