---
title: INF UpdateIniFields 指令
description: UpdateIniFields 指令引用一个或多个命名节，其中可以指定 INI 文件的行内的精细修改。
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
ms.openlocfilehash: e9954df67dcb77de51b5dad19612fd5ae9d431ff
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223090"
---
# <a name="inf-updateinifields-directive"></a>INF UpdateIniFields 指令


**注意：**  如果要生成通用或移动驱动程序包，则此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**UpdateIniFields**指令引用一个或多个命名节，其中可以指定 INI 文件的行内的精细修改。

```inf
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

**UpdateIniFields**指令引用的每个命名部分都具有以下形式：

```inf
[update-inifields-section]
 
ini-file,ini-section,profile-name[,old-field][,new-field][,flags]
...
```

*Inifields*可以有任何由 INF 编写器决定的条目数，每个条目在单独的行中。

## <a name="entries"></a>条目


<a href="" id="ini-file"></a>*ini-文件*  
指定在源媒体上提供的 INI 文件的名称，并在目标计算机上隐式指定要更新的 INI 文件的名称。 此值可以表示为*文件名*，也可以表示为在 INF 文件的[**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌。

<a href="" id="ini-section"></a>*ini-部分*  
指定指定 INI 文件中包含要修改的行的节的名称。

<a href="" id="profile-name"></a>*配置文件-名称*  
指定要在给定 INI 部分内修改的行的名称。 必须至少指定一个*旧字段*和/或*新字段*项，才能修改此行。

<a href="" id="old-field"></a>*旧字段*  
指定给定行中的现有字段。 如果从此节条目中省略了 "*新字段*"，则将从给定行中删除此字段。 否则，给定的*新字段*值应替换此字段。

<a href="" id="new-field"></a>*新建-字段*  
为给定的*旧字段*指定替换项; 如果省略了*旧字段*，则为添加到给定行。

<a href="" id="flags"></a>*随意*  
指定在将给定的 * 新字段追加到给定行时，如何解释给定的*旧*-*字段*和/或*新*-*字段*，如果其中一个或两个都包含星号（**\\**<em>）和/或（在第1位）</em> ，则应使用分隔符：

<a href="" id="bit-zero---0"></a>位 0 = **0**  
在 INI 文件的\*给定行中搜索匹配项时，将在指定的*旧字段*和/或*新字段*项中按原义解释任意星号（），而不是通配符。 这是默认值。

<a href="" id="bit-zero---1"></a>位 0 = **1**  
在 INI 文件的\*给定行中搜索匹配项时，将指定的*旧字段*和/或*新字段*项中的任意星号（）解释为通配符。

<a href="" id="bit-one---0"></a>位 one = **0**  
将指定的*新字段*项添加到 INI 文件的给定行时，请使用空格字符作为分隔符。 这是默认值。

<a href="" id="bit-one---1"></a>位 one = **1**  
将指定的*新字段*项添加到 INI 文件的给定行时，请使用逗号（，）作为分隔符。

<a name="remarks"></a>备注
-------

在 INF 文件中，在 Windows 上的安装中几乎从未指定**UpdateIniFields**指令，因为没有必要在其分发媒体上安装 INI 文件。 但是， **UpdateIniFields**指令在正式语法语句中所示的任何节中有效，在[**AddInterface**](inf-addinterface-directive.md)指令引用的 INF 编写器定义的部分中有效，或在[**InterfaceInstall32**](inf-interfaceinstall32-section.md)节中引用。

对于 INF 文件，每个*inifields 节*名称必须是唯一的。 在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

与[**UpdateInis**](inf-updateinis-directive.md)指令引用的节不同， **UpdateIniFields**引用的节在现有 INI 文件行中替换、添加或删除行的部分，而不会影响特定行的整个值。 必须在每个节条目中指定至少一个*旧字段*值和/或*新字段*值。

将删除修改后的 INI 文件行中的所有注释，因为在根据此部分做出的更改后可能不适用。 在 INI 文件的行中查找字段时，空格、制表符和逗号被解释为字段分隔符。 但是，在将新字段追加到行时，空格字符将用作默认分隔符。

INF 通过以下方式之一在分发介质上提供给定*ini 文件*的完整路径：

-   在 IHV/OEM 提供的 INF 文件中，通过使用此 INF 的 " [**SourceDisksNames**](inf-sourcedisksnames-section.md) " 和 " [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) " 部分显式指定每个命名的源文件的完整路径，该文件不在分发媒体的根目录中。
-   在系统提供的 INF 文件中，通过提供一个或多个其他 INF 文件，在 INF 文件的[**版本**](inf-version-section.md)部分的**LayoutFile**项中标识。

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**字符串**](inf-strings-section.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**版本**](inf-version-section.md)

 

 






