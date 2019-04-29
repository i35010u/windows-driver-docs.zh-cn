---
title: 重写使用 INF 监视器 EDIDs
description: 使用 INF 文件可以重写扩展显示标识数据 (EDID) 的任何监视器。
ms.assetid: AA7DC29B-54D5-461A-8252-600D84F0F581
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007e804eb65b6713ae015c6ae16a506bbedc5ed6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366208"
---
# <a name="overriding-monitor-edids-with-an-inf"></a>重写使用 INF 监视器 EDIDs


使用 INF 文件可以重写扩展显示标识数据 (EDID) 的任何监视器。 示例 INF 文件，Monsamp.inf，演示如何执行此操作提供的 Windows 7 (WDK 版本 7600) 通过使用 Windows Driver Kit (WDK)。 Monsamp.inf，此处重现。

有关如何使用和修改 Monsamp.inf 的信息，请参见[监视器 INF 文件部分](monitor-inf-file-sections.md)。

## <a name="span-idapproachestocorrectingedidsspanspan-idapproachestocorrectingedidsspanspan-idapproachestocorrectingedidsspanapproaches-to-correcting-edids"></a><span id="Approaches_to_correcting_EDIDs"></span><span id="approaches_to_correcting_edids"></span><span id="APPROACHES_TO_CORRECTING_EDIDS"></span>更正 EDIDs 方法


所有监视器，模拟或数字，必须都支持 EDID，其中包含如监视器标识符、 制造商数据、 硬件标识符、 计时信息等的信息。 此数据存储在监视器的 EEPROM 中指定了通过视频电子标准协会 (VESA) 的格式。

监视器提供对 Microsoft Windows 组件 EDID、 显示驱动程序和某些用户模式应用程序。 例如，在初始化期间监视器驱动程序会查询其亮度查询接口和设备驱动程序接口 (DDI) 支持，这是在 EDID 的 Windows 显示器驱动程序模型 (WDDM) 驱动程序。 监视器的 EEPROM 的不正确或无效 EDID 信息可能因此会导致问题，例如设置不正确的显示模式。

有两种方法可以更正 EDIDs:

-   标准的解决方案是让客户将发回给制造商，reflashes 与正确的 EDID EEPROM 并返回给客户的监视器的监视器。
-   更好的解决方案，此处所述，为制造商联系，以实现 INF 文件，其中包含正确的 EDID 信息，是让客户将其下载到计算机连接到监视器。 Windows 将从 INF 提取更新的 EDID 信息然后将其从 EEPROM EDID，有效地重写 EEPROM EDID 而不是信息的组件提供。

除了此处所述，请替换 EDID 信息，一个供应商可以提供替代监视器的名称和喜欢的显示分辨率。 此类替代经常对可用客户通过 Windows Update 或传送框中的数字媒体。 此类重写接收优先权要高于此处提及的 EDID 重写。 可在指导原则来实现此目的[监视器 INF 文件部分](monitor-inf-file-sections.md)。

## <a name="span-idedidformatspanspan-idedidformatspanspan-idedidformatspanedid-format"></a><span id="EDID_format"></span><span id="edid_format"></span><span id="EDID_FORMAT"></span>EDID 格式


EDID 数据格式化为一个或多个 128 字节块为单位：

-   EDID 版本 1.0 到 1.2 包含每 VESA 规范数据的单个块。
-   EDID 1.3 版或增强的 EDID (E EDID)，制造商可以指定除主块的一个或多个扩展基块。

每个块是，从 0 开始编号的初始块。 若要更新 EDID 信息，制造商的 INF 指定要更新的块的数量，并提供 128 字节的 EDID 数据来替换原始块。 监视器驱动程序从注册表获取更新后的数据的已更正的块，并使用剩余的块的 EEPROM 数据。

## <a name="span-idupdatinganedidspanspan-idupdatinganedidspanspan-idupdatinganedidspanupdating-an-edid"></a><span id="Updating_an_EDID"></span><span id="updating_an_edid"></span><span id="UPDATING_AN_EDID"></span>正在更新 EDID


若要使用 INF 更新 EDID:

1.  监视器制造商实现 INF 包含已更新的 EDID 信息并将文件下载到用户的计算机。 这可以通过 Windows 更新或传送的监视器 CD。
2.  监视器类安装程序将从 INF 提取更新的 EDID 信息并将信息存储为此注册表项下的值：

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY
    ```

    每个 EDID 重写存储在单独的密钥下。 例如：

    ```registry
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\DISPLAY\DELA007\
          5&1608c50f&0&10000090&01&20\Device Parameters\EDID_Override
    ```

3.  监视器驱动程序在初始化期间检查注册表，并使用任何 EDID 信息存储在此处而不是 EEPROM 功能的相应信息。 EDID 信息已添加到注册表始终优先于 EEPROM EDID 信息。
4.  Windows 组件和用户模式应用使用已更新的 EDID 信息。

## <a name="span-idoverridinganedidwithaninfspanspan-idoverridinganedidwithaninfspanspan-idoverridinganedidwithaninfspanoverriding-an-edid-with-an-inf"></a><span id="Overriding_an_EDID_with_an_INF"></span><span id="overriding_an_edid_with_an_inf"></span><span id="OVERRIDING_AN_EDID_WITH_AN_INF"></span>重写使用 INF EDID


若要重写 EDID，包括[ **AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)中为每个你想要重写，采用以下格式的块 INF:

```inf
HKR, EDID_OVERRIDE, BlockNumber, Byte 1, Byte 2, Byte 3, Byte 4,...
```

块号后跟包含二进制 EDID 数据的 128 十六进制整数。

制造商必须更新仅 EDID 的块不正确。 系统从 EEPROM 获取剩余的块。 下面的示例演示更新 EDID 块 0、 4 和 5 INF 的相关部分。 监视器驱动程序将获取块 1-3 和任何扩展基块，EEPROM 遵循块 5:

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

有关详细信息中常规、 Inf 和**AddReg**和**DDInstall**信息，请参见[创建 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff538378)。

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

 

 





