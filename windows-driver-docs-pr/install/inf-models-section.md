---
title: INF Models 节
description: 模型部分标识设备、 引用其 DDInstall 部分中，并指定设备的硬件标识符。
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
ms.openlocfilehash: 3b3f67c559898f2126af1024f2ae095bcfd5130a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566663"
---
# <a name="inf-models-section"></a>INF Models 节


每个制造商*模型*部分标识至少一台设备，引用*DDInstall*部分中的该设备的 INF 文件，并指定唯一---模型-部分[硬件标识符 (ID)](hardware-ids.md)为该设备。

每个制造商中的任何条目*模型*部分还可以指定一个或多个其他设备 Id 与设备兼容的模型的指定初始硬件 ID，由相同的驱动程序进行控制。

```ini
[models-section-name] |
[models-section-name.TargetOSVersion]  (Windows XP and later versions of Windows)

device-description=install-section-name[,hw-id][,compatible-id...]
[device-description=install-section-name[,hw-id][,compatible-id]...] ...
```

## <a name="entries"></a>条目


<a href="" id="device-description"></a>*device-description*  
标识设备安装，表示为可见的字符或作为任何唯一组合**%** <em>strkey</em> **%** 定义标记在中[ **INF 字符串部分**](inf-strings-section.md)。 以字符为单位的设备描述的最大长度是 LINE_LEN。

<a href="" id="install-section-name"></a>*install-section-name*  
指定要用于设备 （和兼容型号的设备，如果有） 的 INF 安装部分的未修饰的名。 有关详细信息，请参阅[ **INF *DDInstall*部分**](inf-ddinstall-section.md)。

<a href="" id="hw-id"></a>*hw-id*  
指定供应商定义[硬件 ID](hardware-ids.md)标识设备，即插即用管理器使用来查找此设备的 INF 文件匹配的字符串。 此类的硬件 ID 具有以下格式之一：

<a href="" id="enumerator-enumerator-specific-device-id"></a>*enumerator\\enumerator-specific-device-id*  
是单个报告到 PnP 管理器的单个枚举器的即插即用设备的典型格式。 例如，`USB\VID_045E&PID_00B`标识 USB 总线上的 Microsoft HID 键盘设备。 不同的枚举器，此类规范甚至可以包括设备的硬件修订号为，例如， `PCI\VEN_1011&DEV_002&SUBSYS_00000000&REV_02`。

<a href="" id="-enumerator-specific-device-id"></a>*\*enumerator-specific-device-id*  
指示用星号 (\*) 设备支持的多个枚举器。 例如，`*PNP0F01`标识 Microsoft 串行老鼠，它还具有兼容 id 规范的`SERENUM\PNP0F01`。

<a href="" id="device-class-specific-id"></a>*device-class-specific-ID*  
是 I/O 总线特定的格式，总线，为该类型的 I/O 总线上的所有外围设备的硬件 Id 的硬件规范中所述。

注意，单个设备可以有多个*hw id*值。 PnP 管理器使用每个此类*hw id*值，该值通常提供基础的总线时枚举其子设备，若要在注册表中创建一个用于每个此类设备的子项**枚举**分支。 对于手动安装的设备，系统的安装程序代码使用其*hw id*在其各自的 INF 文件，若要创建每个此类注册表子项中根据指定的值。

<a href="" id="compatible-id"></a>*compatible-id*  
指定供应商定义[兼容 ID](compatible-ids.md)兼容的设备标识字符串。 任意数量的*兼容 id*中的条目，可以指定值*模型*部分中，每个与下一个逗号分隔 (**，**)。 为指定的初始设备相同的驱动程序控制所有此类兼容的设备和/或设备型号*hw id*。

<a name="remarks"></a>备注
-------

每个*模型节名称*必须列在[ **INF 制造商部分**](inf-manufacturer-section.md)的 INF 文件。 在任何每个制造商可以有一个或多个条目*模型*部分中，具体取决于由特定制造商生产的多少设备 （和驱动程序） 安装的 INF 文件。

每个*安装的部分名称*INF 文件中必须唯一，并且必须按照定义的节名称中, 所述的一般规则[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。 [ ***DDInstall*** ](inf-ddinstall-section.md)节名称在每个制造商中引用*模型*部分还可以扩展附加到给定*安装的部分名称*，因此定义其他*DDInstall*的部分，了解特定于操作系统的或特定于平台的安装给定的设备。 有关如何在跨平台系统文件中使用扩展的详细信息，请参阅还[创建一个 INF 文件](overview-of-inf-files.md)。

指定任何*hw id*或*兼容 id*还中指定值[ **INF ControlFlags 部分**](inf-controlflags-section.md)以防止该设备显示给最终用户在手动安装过程。 有关详细信息*hw id*并*兼容 id*值，请参阅[设备标识字符串](device-identification-strings.md)。

对于每个设备和驱动程序，它使用 INF 文件进行安装，设备安装程序使用中提供的信息[ **INF 制造商部分**](inf-manufacturer-section.md)和每个制造商*模型*部分，以生成设备描述，制造商名称、 设备 ID （如果是手动安装），以及可能的兼容性列表值项在注册表中的。

一个*模型节名称*可以包括*TargetOSVersion*修饰。 有关此修饰的详细信息，请参阅[ **INF 制造商部分**](inf-manufacturer-section.md)，特别是备注部分。

**重要**  从 Windows Server 2003 SP1 开始，INF 文件必须修饰*模型节名称*INF 中的条目**制造商**部分中的，以及相关INF*模型*与部分名称， **.ntia64**或 **.ntamd64**平台扩展，以指定非 x86 目标操作系统版本。 对于基于 x86 的目标操作系统版本的 INF 文件或非 PnP 驱动程序 INF 文件 （例如基于 x64 的体系结构的文件系统驱动程序 INF 文件） 中不需要这些平台扩展。 在每个条目*模型*有时称为部分*驱动程序节点*。

 

<a name="examples"></a>示例
--------

此示例显示了每个制造商*模型*节替换系统鼠标类安装程序的 INF 文件中，一些具有代表性条目定义[ ***DDInstall*** ](inf-ddinstall-section.md)某些设备/型号的部分。

```ini
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

## <a name="see-also"></a>请参阅


[**ControlFlags**](inf-controlflags-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[**制造商**](inf-manufacturer-section.md)

[**Strings**](inf-strings-section.md)

 

 






