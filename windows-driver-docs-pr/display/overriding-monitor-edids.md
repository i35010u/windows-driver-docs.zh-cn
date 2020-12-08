---
title: 使用 INF 替代监视器 Edid
description: 使用 INF 文件，可以覆盖任何监视器 (EDID) 的扩展显示标识数据。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa3ffe94b7589179b506a1dd45c35bf5cd196d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802593"
---
# <a name="overriding-monitor-edids-with-an-inf"></a>使用 INF 替代监视器 Edid


使用 INF 文件，可以覆盖任何监视器 (EDID) 的扩展显示标识数据。 用于演示如何执行此操作的示例 INF 文件（Monsamp）随 Windows 驱动程序)  (工具包通过 Windows 7 (WDK 7600 版) 提供。 此处将重现 Monsamp。

有关如何使用和修改 Monsamp 的信息，请参阅 [MONITOR Inf File 部分](monitor-inf-file-sections.md)。

## <a name="span-idapproaches_to_correcting_edidsspanspan-idapproaches_to_correcting_edidsspanspan-idapproaches_to_correcting_edidsspanapproaches-to-correcting-edids"></a><span id="Approaches_to_correcting_EDIDs"></span><span id="approaches_to_correcting_edids"></span><span id="APPROACHES_TO_CORRECTING_EDIDS"></span>更正 Edid 的方法


所有监视器、模拟或数字都必须支持 EDID，其中包含监视器标识符、制造商数据、硬件标识符、计时信息等信息。 此数据以视频电子标准关联 (VESA) 指定的格式存储在监视器的 EEPROM 中。

监视器为 Microsoft Windows 组件、显示器驱动程序和部分用户模式应用程序提供 EDID。 例如，在初始化期间，监视驱动程序将查询 Windows 显示驱动程序模型 (WDDM) 驱动程序的亮度查询接口和设备驱动程序接口， (DDI) 支持（在 EDID 中）。 因此，在监视器的 EEPROM 上出现不正确或无效的 EDID 信息可能会导致问题，例如设置错误的显示模式。

可以通过两种方法来更正 Edid：

-   标准解决方案是让客户将监视器发送回制造商，该制造商使用正确的 EDID reflashes 了 EEPROM，并将监视器返回给客户。
-   此处所述的更好的解决方案是让制造商实施包含正确 EDID 信息的 INF 文件，并让客户将其下载到连接到监视器的计算机。 Windows 从 INF 中提取更新后的 EDID 信息，并将其提供给组件，而不是从 EEPROM EDID 提供的信息，从而有效覆盖 EEPROM EDID。

除了替换此处所述的 EDID 信息外，供应商还可以提供监视器名称和首选显示分辨率的替代项。 此类替代通常通过包装盒中 Windows 更新或数字媒体向客户提供。 此类替代的优先级比此处提到的 EDID 替代的优先级高。 有关实现此项的指导原则，请参阅 [监视 INF 文件部分](monitor-inf-file-sections.md)。

## <a name="span-idedid_formatspanspan-idedid_formatspanspan-idedid_formatspanedid-format"></a><span id="EDID_format"></span><span id="edid_format"></span><span id="EDID_FORMAT"></span>EDID 格式


EDID 数据的格式为一个或多个128字节块：

-   EDID 版本1.0 到1.2 由每个 VESA 规范包含一个数据块。
-   对于 EDID 版本1.3 或增强型 EDID (E-EDID) ，制造商除了指定主块以外，还可以指定一个或多个扩展块。

对于初始块，每个块都从0开始编号。 若要更新 EDID 信息，制造商的 INF 指定了要更新的块号，并提供128字节的 EDID 数据来替换原始块。 监视驱动程序从注册表中获取已更正块的已更新数据，并为其余块使用 EEPROM 数据。

## <a name="span-idupdating_an_edidspanspan-idupdating_an_edidspanspan-idupdating_an_edidspanupdating-an-edid"></a><span id="Updating_an_EDID"></span><span id="updating_an_edid"></span><span id="UPDATING_AN_EDID"></span>更新 EDID


使用 INF 更新 EDID：

1.  监视器制造商实现了包含更新的 EDID 信息的 INF，并将文件下载到用户的计算机。 这可以通过 Windows 更新或通过将 CD 寄送到监视器来完成。
2.  Monitor 类安装程序从 INF 中提取更新的 EDID 信息，并将这些信息存储为以下注册表项下的值：

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY
    ```

    每个 EDID 重写都存储在一个单独的密钥下。 例如：

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY\DELA007\
          5&1608c50f&0&10000090&01&20\Device Parameters\EDID_Override
    ```

3.  监视驱动程序会在初始化期间检查注册表，并使用存储在其中的任何 EDID 信息，而不是使用 EEPROM 上的相应信息。 已添加到注册表中的 EDID 信息始终优先于 EEPROM EDID 信息。
4.  Windows 组件和用户模式应用使用更新的 EDID 信息。

## <a name="span-idoverriding_an_edid_with_an_infspanspan-idoverriding_an_edid_with_an_infspanspan-idoverriding_an_edid_with_an_infspanoverriding-an-edid-with-an-inf"></a><span id="Overriding_an_EDID_with_an_INF"></span><span id="overriding_an_edid_with_an_inf"></span><span id="OVERRIDING_AN_EDID_WITH_AN_INF"></span>使用 INF 替代 EDID


若要重写 EDID，请采用以下格式在 INF 中为要重写的每个块包含 [**AddReg 指令**](../install/inf-addreg-directive.md) ：

```inf
HKR, EDID_OVERRIDE, BlockNumber, 0x1, Byte 1, Byte 2, Byte 3, Byte 4,...
```

块号是要重写的 EDID 块的零索引值。 应将数据字节格式化为包含二进制 EDID 数据的128十六进制整数。 块号后面的 "0x1" 值是一个标志，指示此注册表值包含二进制数据 (FLG_ADDREG_BINVALUETYPE) 。

制造商必须仅更新不正确的 EDID 块。 系统从 EEPROM 获取剩余的块。 下面的示例显示了更新 EDID 块0、4和5的 INF 的相关部分。 监视驱动程序获取块 1-3 和从 EEPROM 中跟随块5的任何扩展块：

```inf
[ABC.DDInstall.HW]
ABC.AddReg
...
[ABC.AddReg]
HKR, EDID_OVERRIDE, 0, 1, 00, FF, ..., 3B
HKR, EDID_OVERRIDE, 4, 1, 1F, 3E, ..., 4E
HKR, EDID_OVERRIDE, 5, 1, 24, 5C, ..., 2D
...
```

有关 Inf 的详细信息以及 **AddReg** 和 **DDInstall** 的详细信息，请参阅 [创建 INF 文件](../hid/creating-an-inf-file.md)。

```inf
; monsamp.INF
;
; Copyright (c) Microsoft Corporation.  All rights reserved.
;
; This is a generic INF file for overriding EDIDs 
; of any monitors, starting with Windows Vista.
;

[Version]
signature="$WINDOWS NT$"
Class=Monitor
ClassGuid={4D36E96E-E325-11CE-BFC1-08002BE10318}
Provider="MS_EDID_OVERRIDE"
DriverVer=04/18/2006, 1.0.0.0

; Be sure to add the directive below with the proper catalog file after 
; WHQL certification.
;CatalogFile=Sample.cat


[DestinationDirs]
DefaultDestDir=23

[SourceDisksNames]
1=%SourceDisksNames%

; Enable the following section to copy a monitor profile.
[SourceDisksFiles]
;profile1.icm=1

[Manufacturer]
%MS_EDID_OVERRIDE%=MS_EDID_OVERRIDE,NTx86,NTamd64

; Modify the hardware ID (MON1234) to match that of the monitor being used.
[MS_EDID_OVERRIDE.NTx86]
%MS_EDID_OVERRIDE-1%=MS_EDID_OVERRIDE-1.Install, MONITOR\MON1234

; Modify the hardware ID (MON1234) to match that of the monitor being used.
[MS_EDID_OVERRIDE.NTamd64]
%MS_EDID_OVERRIDE-1%=MS_EDID_OVERRIDE-1.Install.NTamd64, MONITOR\MON1234

[MS_EDID_OVERRIDE-1.Install.NTx86]
DelReg=DEL_CURRENT_REG
AddReg=MS_EDID_OVERRIDE-1.AddReg, 1024, 1280, DPMS
CopyFiles=MS_EDID_OVERRIDE-1.CopyFiles

[MS_EDID_OVERRIDE-1.Install.NTamd64]
DelReg=DEL_CURRENT_REG
AddReg=MS_EDID_OVERRIDE-1.AddReg, 1024, 1280, DPMS
CopyFiles=MS_EDID_OVERRIDE-1.CopyFiles

[MS_EDID_OVERRIDE-1.Install.NTx86.HW]
AddReg=MS_EDID_OVERRIDE-1_AddReg

[MS_EDID_OVERRIDE-1.Install.NTamd64.HW]
AddReg=MS_EDID_OVERRIDE-1_AddReg

[MS_EDID_OVERRIDE-1_AddReg]
HKR,EDID_OVERRIDE,"0",0x01,0x00,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0x00,0x35,\
0xEE,0x34,0x12,0x01,0x00,0x00,0x00,0x0A,0x0E,0x01,0x03,0x68,0x22,0x1B,\
0x78,0xEA,0xAE,0xA5,0xA6,0x54,0x4C,0x99,0x26,0x14,0x50,0x54,0xA5,0x4B,\
0x00,0x71,0x4F,0x81,0x80,0xA9,0x40,0x01,0x01,0x01,0x01,0x01,0x01,0x01,\
0x01,0x01,0x01,0x30,0x2A,0x00,0x98,0x51,0x00,0x2A,0x40,0x30,0x70,0x13,\
0x00,0x52,0x0E,0x11,0x00,0x00,0x1E,0x00,0x00,0x00,0xFF,0x00,0x41,0x42,\
0x30,0x30,0x30,0x30,0x30,0x30,0x30,0x30,0x30,0x31,0x0A,0x00,0x00,0x00,\
0xFC,0x00,0x4D,0x53,0x20,0x31,0x32,0x33,0x34,0x0A,0x0A,0x0A,0x0A,0x0A,\
0x0A,0x00,0x00,0x00,0xFD,0x00,0x38,0x4C,0x1F,0x50,0x12,0x00,0x0A,0x20,\
0x20,0x20,0x20,0x20,0x20,0x00,0xDB

[DEL_CURRENT_REG]
HKR,MODES
HKR,,MaxResolution
HKR,,DPMS
HKR,,ICMProfile

; Pre-defined AddReg sections. These can be used for default settings 
; when a given standard resolution is used.

[1024]
HKR,,MaxResolution,,"1024,768"
[1280]
HKR,,MaxResolution,,"1280,1024"

[DPMS]
HKR,,DPMS,,1

[MS_EDID_OVERRIDE-1.AddReg]
HKR,"MODES\1024,768",Mode1,,"31.0-94.0,55.0-160.0,+,+"
HKR,"MODES\1280,1024",Mode1,,"31.0-94.0,55.0-160.0,+,+"

; Enable the following section to copy a monitor profile.
[MS_EDID_OVERRIDE-1.CopyFiles]
;PROFILE1.ICM

[Strings]
MonitorClassName="Monitor"
SourceDisksNames="MS_EDID_OVERRIDE Monitor EDID Override Installation Disk"

MS_EDID_OVERRIDE="MS_EDID_OVERRIDE"
MS_EDID_OVERRIDE-1="MS EDID Override"
```

 

