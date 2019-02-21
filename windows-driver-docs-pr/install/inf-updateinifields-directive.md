---
title: INF UpdateIniFields 指令
description: UpdateIniFields 指令引用一个或多个命名的部分可以在其中指定 INI 文件的行内的精细修改。
ms.assetid: fda645c9-9ecb-46fe-9d21-1c042d56acd3
keywords:
- INF UpdateIniFields 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF UpdateIniFields Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a9b390b501f20d0d00c59c0c184da33b1e36cae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520019"
---
# <a name="inf-updateinifields-directive"></a>INF UpdateIniFields 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**UpdateIniFields**指令引用一个或多个命名的部分可以在其中指定 INI 文件的行内的精细修改。

```ini
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
UpdateIniFields=update-inifields-section[,update-inifields-section]...
```

每个命名部分引用的**UpdateIniFields**指令具有以下形式：

```ini
[update-inifields-section]
 
ini-file,ini-section,profile-name[,old-field][,new-field][,flags]
...
```

*更新 inifields 部分*可以具有任意 INF 编写器确定数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="ini-file"></a>*ini-file*  
指定提供的源媒体在和上，隐式的目标计算机上的将更新 INI 文件 INI 文件的名称。 此值可以表示为*文件名*或作为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md) INF 文件部分。

<a href="" id="ini-section"></a>*ini-section*  
指定包含要修改的行中给定的 INI 文件的部分的名称。

<a href="" id="profile-name"></a>*profile-name*  
指定要在给定的 INI 部分内修改的行的名称。 在至少一个*old-field*和/或*新字段*条目必须指定要影响这行的修改。

<a href="" id="old-field"></a>*old-field*  
指定给定行中的现有字段。 如果*新字段*省略此部分条目，此字段删除从给定的行。 否则为给定*新字段*值应替换为此字段。

<a href="" id="new-field"></a>*new-field*  
指定的替换给定*old-field* ; 如果*old-field*省略，则对给定行的补充。

<a href="" id="flags"></a>*flags*  
（以位 0） 指定如何解释给定*旧*-*域*和/或*新*-*字段*如果或两个都包含一个星号 (**\\**<em>)，和/或 （以位 1） 的分隔符字符追加时要使用给定 * 新字段</em>到给定的行，按如下所示：

<a href="" id="bit-zero---0"></a>Bit 0 = **0**  
解释任何星号 (\*) 中指定*old-field*和/或*新字段*条目按字面意思不是作为通配符字符，搜索给定行的 INI 文件中的匹配项时。 这是默认值。

<a href="" id="bit-zero---1"></a>Bit 0 = **1**  
解释任何星号 (\*) 中指定*old-field*和/或*新字段*作为通配符字符搜索给定行的 INI 文件中的匹配项时的条目。

<a href="" id="bit-one---0"></a>一个位 = **0**  
添加指定时将空格字符用作分隔符*新字段*到给定行的 INI 文件条目。 这是默认值。

<a href="" id="bit-one---1"></a>一个位 = **1**  
添加指定时，使用逗号 （，） 作为分隔符*新字段*到给定行的 INI 文件条目。

<a name="remarks"></a>备注
-------

**UpdateIniFields**因为不再需要将其分发媒体的 INI 文件安装在 Windows 上的 INF 文件几乎永远不会指定指令。 但是， **UpdateIniFields**指令中所示在正式语法语句中，以及引用的 INF 编写器定义部分中的部分是有效[ **AddInterface**](inf-addinterface-directive.md)指令或在引用[ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)部分。

每个*更新 inifields 部分*名称必须是唯一的 INF 文件。 每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

与引用的一个部分不同[ **UpdateInis** ](inf-updateinis-directive.md)指令，引用的一个部分**UpdateIniFields** 、 添加、 删除或替换现有 INI 文件中的行的部分而不是影响特定行的整个值的行。 在至少一个*old-field*和/或*新字段*必须在每个部分条目中指定值。

因为它们可能不适用于根据本部分中进行了更改后，会删除要修改 INI 文件行中的任何注释。 在查看 INI 文件中的行中的字段，空格、 制表符和逗号解释为字段分隔符。 但是，空格字符是作为默认分隔符时使用新的字段将附加到行。

INF 提供的完整路径给定*ini 文件*中通过以下方式之一在分发媒体：

-   在提供 IHV/OEM INF 文件中，通过使用[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)并[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分到此 INF 显式指定在分发媒体的根目录 （或目录） 中不是每个命名的源文件的完整路径。
-   在系统提供 INF 文件中，通过提供一个或多个附加 INF 文件中标识**LayoutFile**中的条目[**版本**](inf-version-section.md) INF 文件部分。

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**Strings**](inf-strings-section.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**版本**](inf-version-section.md)

 

 






