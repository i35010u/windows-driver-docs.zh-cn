---
title: INF ProfileItems 指令
description: 更多是部分项配置文件的包含项或组添加或删除从开始菜单或 ProfileItems 指令使用 INF DDInstall 节到一个列表中。
ms.assetid: 8cdd6dcd-de5d-4652-8842-6b0be6f5fb59
keywords:
- INF ProfileItems 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF ProfileItems Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 604a781f1f8cf400d73783ae1af5132bb6b88e5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526157"
---
# <a name="inf-profileitems-directive"></a>INF ProfileItems 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**ProfileItems**中使用指令[ **INF *DDInstall*部分**](inf-ddinstall-section.md)到一个或多个列表*配置文件项部分*的包含项或组添加或从开始菜单中删除。

```ini
[DDInstall] 
 
ProfileItems=profile-items-section[,profile-items-section]...
...
```

每个命名部分引用的**ProfileItems**指令具有以下形式：

```ini
[profile-items-section]
 
Name=link-name[,name-attributes]
CmdLine=dirid,[subdir],filename
[SubDir=path]
[WorkingDir=wd-dirid,wd-subdir]
[IconPath=icon-dirid,[icon-subdir],icon-filename]
[IconIndex=index-value]
[HotKey=hotkey-value]
[Infotip=info-tip]
[DisplayResource="ResDllPath\ResDll",ResID]
```

Windows XP 和更高版本的 Windows 中支持此指令。

## <a name="entries"></a>条目


<a href="" id="name-link-name--name-attributes-"></a>**Name=**<em>link-name</em>\[**,**<em>name-attributes</em>\]  
*链接名称*而不指定菜单项或组，链接的名称 *.lnk*扩展。 此值可以是字符串或 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md) INF 文件部分。 如果**DisplayResource**未指定项，则*链接名称*也是显示字符串。

可选*名称属性*值指定一个或多个标志会影响操作的菜单项。 此值表示为或运算的位掩码的系统定义的标志值。 可能的标志包括：

<a href="" id="0x00000001--flg-profitem-currentuser-"></a>**0x00000001** (FLG_PROFITEM_CURRENTUSER)  
指示 Windows 创建或删除当前用户的配置文件中的开始菜单项。 如果未指定此标志，Windows 将处理所有用户的项。

<a href="" id="0x00000002---flg-profitem-delete-"></a>**0x00000002** (FLG_PROFITEM_DELETE)  
指示 Windows 删除菜单项。 如果未指定此标志，则创建项。

<a href="" id="0x00000004--flg-profitem-group-"></a>**0x00000004** (FLG_PROFITEM_GROUP)  
指示 Windows 创建或删除在开始下的开始菜单组\\程序。 如果未指定此标志，Windows 将创建或删除菜单项，而不是菜单组。

如果不指定任何标志，则 Windows 将创建所有用户的菜单项。

<a href="" id="cmdline-dirid--subdir--filename"></a>**CmdLine=**<em>dirid</em>**,**\[*subdir*\]**,**<em>filename</em>  
*Dirid*指定一个值，标识命令程序所在的目录。 例如， *dirid* 11 的指示系统目录。 可能*dirid*的说明中列出了值*dirid*中的值[ **DestinationDirs** ](inf-destinationdirs-section.md)部分。

如果*subdir*存在字符串，该命令程序引用的目录的子目录中*dirid*。 *Subdir*指定的子目录。 如果没有*subdir*的程序在引用的目录的指定*dirid*。

*文件名*指定与菜单项关联的程序的名称。

<a href="" id="subdir-path"></a>**SubDir=**<em>path</em>  
此可选项指定在开始下的子目录 （子菜单）\\程序所在的菜单项。 如果省略此项，则该路径默认为起点\\程序。

例如，如果*配置文件项部分*包含的条目"Subdir = 附件\\游戏"，然后在菜单项创建或删除在入门\\程序\\附件\\游戏子菜单。

**请注意**  为指定如果 FLG_PROFITEM_GROUP*名称特性*，则**SubDir**条目被忽略。

 

<a href="" id="workingdir-wd-dirid--wd-subdir-"></a>**WorkingDir=**<em>wd-dirid</em>\[**,**<em>wd-subdir</em>\]  
此可选条目指定命令程序的工作目录。 如果省略此项，则工作目录将默认为命令程序所在的目录。

*Wd dirid*值标识的工作目录。 有关可能的列表*dirid*值，请参阅[使用 Dirids](using-dirids.md)。

*Wd subdir*字符串，如果存在，则指定的子目录*wd dirid*为工作目录。 使用此参数指定不具有系统定义的目录*dirid*。 如果省略此参数，则*wd dirid*值本身指定的工作目录。

<a href="" id="iconpath-icon-dirid--icon-subdir--icon-filename"></a>**IconPath=**<em>icon-dirid</em>**,**\[*icon-subdir*\]**,**<em>icon-filename</em>  
此可选项指定包含菜单项的图标的文件的位置。

*图标 dirid*字符串标识对于包含图标的 DLL 的目录。 有关可能的列表*dirid*值，请参阅[使用 Dirids](using-dirids.md)。

*图标 subdir*值，如果存在，则指示该 DLL 正在的子目录*图标 dirid*。 *图标 subdir*值指定的子目录。

*图标文件名*值指定包含图标的 DLL。

如果省略此项，则 Windows 会查找中指定的文件中的图标**CmdLine**条目。

<a href="" id="iconindex-index-value"></a>**IconIndex=**<em>index-value</em>  
此可选条目在 DLL 要使用的菜单项中指定的图标。 有关如何将索引在 DLL 中的图标的信息，请参阅 Microsoft Windows SDK 文档。

如果**IconPath**指定项时，*索引值*到该 DLL 的索引。 此值中指定的文件中的索引，否则**CmdLine**条目。

<a href="" id="hotkey-hotkey-value"></a>**HotKey=**<em>hotkey-value</em>  
此可选项指定菜单项的键盘加速器。

有关热键的详细信息，请参阅 Windows SDK 文档。

<a href="" id="infotip-info-tip"></a>**Infotip=**<em>info-tip</em>  
此可选项指定菜单项的信息性提示。

此值可以是字符串或 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md) INF 文件部分。

*信息提示*还可以将值指定为 **"@**<em>ResDllPath</em>**\\**<em>ResDll</em> **，-**<em>resID</em>**"**，其中*ResDllPath*并*ResDll*指定的路径和文件名称的资源 DLL，和-*resID*是负值，表示资源 id。

使用此格式支持 Windows 多语言用户界面 (MUI)。 示例如下所示：

```ini
InfoTip = "@%11%\shell32.dll,-22531"
```

<a href="" id="displayresource--resdllpath-resdll--resid"></a>**DisplayResource="**<em>ResDllPath\\ResDll</em>**",**<em>ResID</em>  
此可选条目指定标识可本地化的字符串，要在开始菜单中用作快捷方式或组的显示名称的字符串资源。

*ResDllPath*并*ResDll*指定的资源 DLL 路径和文件名称和*resID*为正的值，该值表示资源 id。 示例如下所示：

```ini
DisplayResource="%11%\shell32.dll",22019
```

使用此项以支持 Windows 多语言用户界面 (MUI)。 如果未使用此项，指定的字符串**名称**显示项。

<a name="remarks"></a>备注
-------

给定*配置文件项部分*名称必须是唯一的 INF 文件中的和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

每个*配置文件项部分*包含用于创建或删除一个开始菜单项或组的详细的信息。 若要处理多个菜单项或用户组 INF，创建多个*配置文件项部分*和列表中的部分**ProfileItems**指令。

中指定的字符串任何的参数*配置文件项部分*可以通过使用 %指定条目*strkey*%令牌，如中所述[的 INF 文件一般语法规则](general-syntax-rules-for-inf-files.md).

<a name="examples"></a>示例
--------

以下的 INF 文件摘录显示了如何使用*配置文件项部分*要添加到开始菜单的计算器。

```ini
[CalcInstallItems]
Name = %Calc_DESC%
CmdLine = 11,, calc.exe
SubDir = %Access_GROUP%
WorkingDir = 11
InfoTip = %Calc_TIP%
:
:
[Strings]
AccessGroup = "Accessories"
Calc_DESC = "Calculator"
Calc_TIP = "Performs basic arithmetic tasks with an on-screen calculator"
```

以下的 INF 文件摘录显示了如何使用安装的相同软件**DisplayResource**条目来创建本地化的菜单项。

```ini
[CalcInstallItems]
Name = %Calc_DESC%
CmdLine = 11,, calc.exe
SubDir = %Access_GROUP%
WorkingDir = 11
InfoTip = "@%11%\shell32.dll,-22531"
DisplayResource="%11%\shell32.dll",22019
:
:
[Strings]
Access_GROUP = "Accessories"
Calc_DESC = "Calculator"
```

## <a name="see-also"></a>另请参阅


[***DDInstall***](inf-ddinstall-section.md)

 

 






