---
title: findxmldata
description: Findxmldata 扩展从包含内核模式小内存转储文件的 CAB 文件中检索 XML 数据。
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
ms.openlocfilehash: 04cf887e0356a47cc82f59cc0a9e735160898398
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815539"
---
# <a name="findxmldata"></a>!findxmldata


**！ Findxmldata** extension 从包含内核模式小内存转储文件的 CAB 文件中检索 XML 数据。

```dbgcmd
!findxmldata [ -d DeviceName | -h HwId ] 
!findxmldata -r Driver 
!findxmldata -chksum [ -z CabFile ]
!findxmldata -v 
```

## <a name="span-idddk__findxmldata_dbgspanspan-idddk__findxmldata_dbgspanparameters"></a><span id="ddk__findxmldata_dbg"></span><span id="DDK__FINDXMLDATA_DBG"></span>参数


<span id="_______-d_______DeviceName______"></span><span id="_______-d_______devicename______"></span><span id="_______-D_______DEVICENAME______"></span>**-d** *DeviceName*   
显示其设备名称包含 *DeviceName* 指定的字符串的所有设备。

<span id="_______-h_______HwId______"></span><span id="_______-h_______hwid______"></span><span id="_______-H_______HWID______"></span>**-h** *HwId*   
显示其硬件 Id 包含 *HwId* 指定的字符串的所有设备。 如果同时使用 **-d** 和 **-h**，则调试器只显示满足这两个匹配项的那些设备。

<span id="_______-r_______Driver______"></span><span id="_______-r_______driver______"></span><span id="_______-R_______DRIVER______"></span>**-r** *驱动程序*   
显示有关 *driver* 参数指定的驱动程序的信息，包括使用此驱动程序的所有设备。

<span id="_______-chksum______"></span><span id="_______-CHKSUM______"></span>**-chksum**   
显示 XML 文件的校验和。

<span id="_______-z_______CabFile______"></span><span id="_______-z_______cabfile______"></span><span id="_______-Z_______CABFILE______"></span>**-z** *CabFile*   
使你能够对 CabFile 参数指定的 CAB 文件执行校验和，而不是在默认 Sysdata.xml 文件上执行。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
显示系统版本信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

**！ Findxmldata** extension 仅适用于存储在 CAB 文件中的内核模式小内存转储文件。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何将转储文件放入 CAB 文件的详细信息，请参阅 [**。 dumpcab (创建转储文件 CAB)**](-dumpcab--create-dump-file-cab-.md)。 有关如何调试内核模式转储文件的详细信息（包括 CAB 文件中存储的转储文件），请参阅 [分析 Kernel-Mode 转储文件](analyzing-a-kernel-mode-dump-file.md)。

<a name="remarks"></a>备注
-------

**！ Findxmldata** extension 从存储在包含内核模式 [小内存转储](small-memory-dump.md)文件的 CAB 文件中的 Sysdata.xml 文件中检索数据。

如果不使用任何选项，则扩展将显示所有设备。

下面的示例演示如何使用 **！ findxmldata**。

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

 

 





