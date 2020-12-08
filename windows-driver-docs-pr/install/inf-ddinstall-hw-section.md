---
title: INF DDInstall.HW 节
description: DDInstall 部分通常用于安装多功能设备、安装 PnP 筛选器驱动程序，以及设置注册表中任何用户可访问的特定于驱动程序的信息，无论是使用显式 AddReg 指令还是包含和需要条目。
keywords:
- INF DDInstall 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.HW Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9be714b2dc1f45ed6e046aaf2a195e2316f2ef0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826209"
---
# <a name="inf-ddinstallhw-section"></a>INF DDInstall.HW 节


<em>DDInstall</em>**。HW** 部分通常用于安装多功能设备、安装 PnP 筛选器驱动程序，以及设置注册表中任何用户可访问的特定于驱动程序的信息，无论是使用显式 [**AddReg**](inf-addreg-directive.md) 指令还是 **包含** 和 **需要** 条目。

```inf
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

## <a name="entries"></a>项


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>添加注册表-节</em> \[ **，**<em>外</em>接程序 \] .。。  
对于此 <em>DDInstall</em>涵盖的设备，引用 inf 文件中其他位置的一个或多个 inf 写入器定义的 *外接程序部分***。HW** 部分。 " *添加注册表" 部分* 通常会在注册表中安装筛选器和/或存储每个设备的信息。 此类 " **HKR** " *部分* 指定设备的 *硬件密钥*，这是一个特定于设备的注册表子项，其中包含有关设备的信息。 硬件密钥也称为设备密钥。 有关详细信息，请参阅 [设备和驱动程序的注册表树和密钥](./registry-trees-and-keys.md)。 驱动程序包可以通过 INF 使用 **HKR** 规范在 **DDInstall 部分** 引用的添加注册表部分中添加设置。 

有关详细信息，请参阅 [**INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
指定一个或多个系统提供的其他 INF 文件，其中包含安装此设备所需的部分。 如果指定此项，则通常是 **需要** 输入。

有关其用法的 **包含** 项和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em> \[ **，**<em>inf-节名称</em> \] .。。  
指定在安装此设备期间必须处理的命名节。 通常，此类命名部分是 <em>DDInstall</em>**。****包含在包含** 项中的系统提供的 INF 文件中的 HW 部分。 但是，它可以是在此类 <em>DDInstall</em>中引用的任何部分 **。** 随附 INF 的 "硬件" 部分。

不能嵌套 **需求** 条目。 有关其用法的 **需求** 条目和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg =**<em>del-registry</em>-section \[ **，**<em>del</em> \] .。。  
在 INF 文件中的其他位置引用一个或多个 INF 写入 *器定义的 DDInstall 节，* 其中包含此 *DDInstall* 部分涵盖的设备的驱动程序。 此类 "删除注册表" 部分会从目标计算机中删除以前安装的设备/驱动程序的过时注册表信息。 此类 "删除注册表" 一节中的 **HKR** 规范指定了与 **AddReg** 相同的子项。

此指令很少使用，但在 INF 文件中，该文件用于升级在定义此 *DDInstall* 部分的名称的每个制造商每个 *模型* 中列出的相同设备/型号的以前安装。 有关详细信息，请参阅 [**INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section-----"></a>**BitReg =**<em>位注册表-节</em> \[ **，**<em>位注册表-节</em> \] .。。  
在此部分有效，但几乎从未使用过。 引用的 bit 注册表部分中的 **HKR** 规范指定了与 **AddReg** 相同的子项。 有关详细信息，请参阅 [**INF BitReg 指令**](inf-bitreg-directive.md)。

<a name="remarks"></a>备注
-------

在正式语法语句中显示的 *安装节名称* 不区分大小写的扩展可以插入到此类 <em>DDInstall</em>中 **。** 跨平台 INF 文件中的硬件部分名称。 有关如何使用 **系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm** 和 **Ntarm64** 扩展的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

任何 <em>DDInstall</em>**。HW** 部分必须具有以下项之一：

- **AddReg** 指令。
- 指定另一个 INF 文件的 **包含** 项。 在本例中为 <em>DDInstall</em>**。HW** 部分还必须包含指定另一 INF 文件中的部分的相应 **需求** 条目。 本节用于设置所需的注册表信息。

<em>DDInstall</em>中的每个指令 **。HW** 部分可以引用多个 INF 写入器定义的部分。 但是，必须将每个附加的命名节与下一个逗号 ( ) 。

每个此类名称在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

有关如何安装多功能设备的详细信息，请参阅 [支持多功能设备](../multifunction/index.md)。

<a name="examples"></a>示例
--------

此示例演示 cd-rom 设备类安装程序如何使用 <em>DDInstall</em>**。HW** 部分和 <em>DDInstall</em>**。** 用于通过创建合适的注册表项并将其设置为 PnP 上层筛选器驱动程序来支持 CD 音频和转换器功能的服务部分。

```inf
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

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。服务器**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

