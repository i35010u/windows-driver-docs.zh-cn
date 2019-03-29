---
title: findxmldata
description: Findxmldata 扩展从 CAB 文件包含一个内核模式小内存转储文件中检索 XML 数据。
ms.assetid: 6d0b5294-b086-4b33-ac0d-0428521a3489
keywords:
- CAB 文件中的 XML 数据
- sysdata.xml
- findxmldata Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findxmldata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be71b499f13e007b1948fb46d191f13b77c22cbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563569"
---
# <a name="findxmldata"></a>!findxmldata


**！ Findxmldata**扩展从 CAB 文件包含一个内核模式小内存转储文件中检索 XML 数据。

```dbgcmd
!findxmldata [ -d DeviceName | -h HwId ] 
!findxmldata -r Driver 
!findxmldata -chksum [ -z CabFile ]
!findxmldata -v 
```

## <a name="span-idddkfindxmldatadbgspanspan-idddkfindxmldatadbgspanparameters"></a><span id="ddk__findxmldata_dbg"></span><span id="DDK__FINDXMLDATA_DBG"></span>参数


<span id="_______-d_______DeviceName______"></span><span id="_______-d_______devicename______"></span><span id="_______-D_______DEVICENAME______"></span> **-d** *DeviceName*   
显示设备名称包含字符串的所有设备的*DeviceName*指定。

<span id="_______-h_______HwId______"></span><span id="_______-h_______hwid______"></span><span id="_______-H_______HWID______"></span> **-h** *HwId*   
显示所有设备的硬件 Id 包含字符串的*HwId*指定。 如果同时使用这两者 **-d**并 **-h**，调试器将显示满足这两个匹配项的那些设备。

<span id="_______-r_______Driver______"></span><span id="_______-r_______driver______"></span><span id="_______-R_______DRIVER______"></span> **-r** *Driver*   
显示有关驱动程序的信息的*驱动程序*参数指定，包括使用此驱动程序的所有设备。

<span id="_______-chksum______"></span><span id="_______-CHKSUM______"></span> **-chksum**   
显示 XML 文件的校验和。

<span id="_______-z_______CabFile______"></span><span id="_______-z_______cabfile______"></span><span id="_______-Z_______CABFILE______"></span> **-z** *CabFile*   
使您能够对 CabFile 参数指定，该 CAB 文件执行校验和而不是默认 Sysdata.xml 文件上。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
显示系统的版本信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

**！ Findxmldata**扩展仅在 CAB 文件中存储的内核模式小内存转储文件上的作用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何将转储文件放到 CAB 文件的详细信息，请参阅[ **.dumpcab (创建转储文件 CAB)**](-dumpcab--create-dump-file-cab-.md)。 了解有关如何调试内核模式转储文件，包括在 CAB 文件内存储的转储文件的详细信息请参阅[分析内核模式转储文件](analyzing-a-kernel-mode-dump-file.md)。

<a name="remarks"></a>备注
-------

**！ Findxmldata**扩展从 Sysdata.xml 文件存储在包含内核模式的 CAB 文件中检索数据[小内存转储](small-memory-dump.md)文件。

当不使用任何选项时，该扩展将显示所有设备。

下面的示例显示如何使用 **！ findxmldata**。

```dbgcmd
kd> !findxmldata -v
SYSTEM Info:
OSVER: 5.1.2600 2.0
OSLANGUAGE: 2052
OSNAME: Microsoft Windows XP Home Edition
kd> !findxmldata -d MIDI
Node DEVICE
 DESCRIPTION    : MPU-401 Compatible MIDI Device
        HARDWAREID     : ACPI\PNPB006
        SERVICE        : ms_mpu401
        DRIVER         : msmpu401.sys

kd> !findxmldata -r msmpu
Node DRIVER
 FILENAME       : msmpu401.sys
        FILESIZE       : 2944
        CREATIONDATE   : 05-06-2005 09:18:34
        VERSION        : 5.1.2600.0
        MANUFACTURER   : Microsoft Corporation
        PRODUCTNAME    : Microsoft« Windows« Operating System
Node DEVICE
        DESCRIPTION    : MPU-401 Compatible MIDI Device
 HARDWAREID     : ACPI\PNPB006
        SERVICE        : ms_mpu401
        DRIVER         : msmpu401.sys

kd> !findxmldata -h PCI\VEN_8086&DEV_24C3&SUBSYS_24C28086
Node DEVICE
 DESCRIPTION    : Intel(R) 82801DB/DBM SMBus Controller - 24C3
        HARDWAREID     : PCI\VEN_8086&DEV_24C3&SUBSYS_24C28086&REV_01
kd> !findxmldata -h USB\ROOT_HUB&VID8086&PID24C4&REV0001
Node DEVICE
        DESCRIPTION    : USB Root Hub
 HARDWAREID     : USB\ROOT_HUB&VID8086&PID24C4&REV0001
        SERVICE        : usbhub
        DRIVER         : usbhub.sys

kd> !findxmldata -h ACPI\PNPB006
Node DEVICE
        DESCRIPTION    : MPU-401 Compatible MIDI Device
 HARDWAREID     : ACPI\PNPB006
        SERVICE        : ms_mpu401
        DRIVER         : msmpu401.sys
```

 

 





