---
title: INF Models 节
description: 模型部分确定设备，引用其 DDInstall 部分，并指定设备的硬件标识符。
ms.assetid: b870e8fb-21b4-439b-b858-c45bf9be2ec1
keywords:
- INF 模型部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF Models Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82192c109d14ff783586df81590281127983bdd6
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223133"
---
# <a name="inf-models-section"></a>INF Models 节


每个制造商的*型号*部分识别至少一个设备，引用该设备的 INF 文件的*DDInstall*部分，并为该设备指定一个唯一的模型部分的[硬件标识符（ID）](hardware-ids.md) 。

每个制造商的*型号*部分中的任何条目都可以为与由初始硬件 ID 指定的设备兼容并由同一驱动程序控制的设备指定一个或多个附加设备 id。

```inf
[models-section-name] |
[models-section-name.TargetOSVersion]  (Windows XP and later versions of Windows)

device-description=install-section-name,[hw-id][,compatible-id...]
[device-description=install-section-name,[hw-id][,compatible-id]...] ...
```

> [!NOTE]
> Inf 需要至少为 "模型" 部分中的每个条目指定一个设备 ID。  这可能是硬件 ID 或兼容 ID。

## <a name="entries"></a>条目


<a href="" id="device-description"></a>*设备-描述*  
**%** 标识要安装的设备，表示为可见字符的任意唯一组合或在[**INF 字符串部分**](inf-strings-section.md)中定义的<em>strkey</em> **%** 标记。 设备说明 LINE_LEN 的最大长度（以字符为字符）。

<a href="" id="install-section-name"></a>*安装-节名称*  
指定要用于设备的 INF 安装部分的未修饰名称（如果有）。 有关详细信息，请参阅[**INF *DDInstall*部分**](inf-ddinstall-section.md)。

<a href="" id="hw-id"></a>*hw-id*  
指定供应商定义的[硬件 ID](hardware-ids.md)字符串，该字符串用于标识设备，PnP 管理器使用该设备查找此设备的 INF 文件匹配项。 此类硬件 ID 具有以下格式之一：

<a href="" id="enumerator-enumerator-specific-device-id"></a>*枚举\\器特定的设备 id*  
由单个枚举器报告给 PnP 管理器的单个 PnP 设备的典型格式。 例如， `USB\VID_045E&PID_00B`标识 USB 总线上的 Microsoft HID 键盘设备。 根据枚举器，此类规范甚至可以包含设备的硬件修订号，例如`PCI\VEN_1011&DEV_002&SUBSYS_00000000&REV_02`。

<a href="" id="-enumerator-specific-device-id"></a>*\*特定于枚举器的设备 id*  
用星号（\*）指示该设备受多个枚举器支持。 例如， `*PNP0F01`标识 Microsoft 串行鼠标，它也具有的兼容 id 规范`SERENUM\PNP0F01`。

<a href="" id="device-class-specific-id"></a>*设备-类特定 ID*  
是 i/o 总线特定的格式，如总线硬件规范中所述，适用于该类型的 i/o 总线上的所有外围设备的硬件 Id。

请注意，一个设备可以有多个*hw id*值。 PnP 管理器使用每个此类*hw id*值，这些值通常在枚举其子设备时由基础总线提供，用于为注册表**枚举**分支中的每个此类设备创建子项。 对于手动安装的设备，系统的安装代码将使用其各自 INF 文件中指定的*hw id*值来创建每个此类注册表子项。

<a href="" id="compatible-id"></a>*兼容-id*  
指定标识兼容设备的供应商定义的[兼容 ID](compatible-ids.md)字符串。 可以为 "*模型*" 部分中的条目指定任意数量的*兼容 id*值，每个值由逗号（**，**）分隔。 所有此类兼容设备和/或设备型号由初始*hw id*指定的设备的相同驱动程序进行控制。

<a name="remarks"></a>备注
-------

每个*模型-名称*必须在 inf 文件的 " [**inf 制造商" 部分**](inf-manufacturer-section.md)列出。 任何 "每个制造商的*型号*" 部分中可以有一个或多个条目，具体取决于 INF 文件为特定制造商安装了多少设备（和驱动程序）。

每个*安装节名称*在 inf 文件中必须唯一，并且必须遵循用于定义节名称的常规规则，如[INF 文件一般语法规则](general-syntax-rules-for-inf-files.md)中所述。 在每个制造商的*型号*部分中引用的[***DDInstall***](inf-ddinstall-section.md)节名称还可以将扩展附加到给定的*安装节名称*，从而为特定设备的特定于操作系统或特定于平台的安装定义其他*DDInstall*部分。 有关如何在跨平台系统文件中使用扩展的详细信息，请参阅[创建 INF 文件](overview-of-inf-files.md)。

还可以在[**INF ControlFlags 部分**](inf-controlflags-section.md)中指定任何指定的*硬件 id*或*兼容 id*值，以防止在手动安装过程中将该设备显示给最终用户。 有关*hw id*和*兼容 id*值的详细信息，请参阅[设备标识字符串](device-identification-strings.md)。

对于使用 INF 文件安装的每个设备和驱动程序，设备安装程序使用在[**Inf 制造商部分**](inf-manufacturer-section.md)和每个制造商的*型号*部分中提供的信息来生成设备说明、制造商名称、设备 ID （如果安装为手动），并且可能会在注册表中生成兼容列表值项。

*模型节名称*可以包含*TargetOSVersion*修饰。 有关此修饰的详细信息，请参阅[**INF 制造商部分**](inf-manufacturer-section.md)，尤其是 "备注" 部分。

**重要提示：**  从 Windows Server 2003 SP1 开始，inf 文件必须修饰 "inf**制造商**" 部分中的 "*模型-名称*" 条目以及关联的 "inf*模型*" 部分名称，其中**ntia64**或 **. ntamd64**平台扩展用于指定非 x86 目标操作系统版本。 在基于 x86 的目标操作系统版本或非 PnP 驱动程序 INF 文件（如基于 x64 的体系结构的文件系统驱动程序 INF 文件）的 INF 文件中，这些平台扩展不是必需的。 "*模型*" 部分中的每个条目有时称为 "*驱动程序" 节点*。

 

<a name="examples"></a>示例
--------

此示例显示了一个每个制造商的*型号*部分，其中包含系统老鼠类安装程序的 INF 文件中的一些代表条目，为某些设备/型号定义[***DDInstall***](inf-ddinstall-section.md)部分。

```inf
[Manufacturer]
%StdMfg%    =StdMfg         ; (Standard types)
%MSMfg%     =MSMfg          ; Microsoft
; ... %otherMfg% omitted here

[StdMfg]  ; per-Manufacturer Models section 
  ; Std serial mouse
%*pnp0f0c.DeviceDesc%= Ser_Inst,*PNP0F0C,SERENUM\PNP0F0C,SERIAL_MOUSE
  ; Std InPort mouse
%*pnp0f0d.DeviceDesc%      = Inp_Inst,*PNP0F0D
; ... more StdMfg entries 
```

## <a name="see-also"></a>另请参阅


[**ControlFlags**](inf-controlflags-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[**制造商**](inf-manufacturer-section.md)

[**字符串**](inf-strings-section.md)

 

 






