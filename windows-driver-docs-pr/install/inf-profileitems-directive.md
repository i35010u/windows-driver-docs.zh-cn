---
title: INF ProfileItems 指令
description: 在 INF DDInstall 节中使用 ProfileItems 指令来列出一个或多个配置文件项-包括要添加到 "开始" 菜单或从 "开始" 菜单中删除的项或组的部分。
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
ms.openlocfilehash: 1e74eeb050677a3e8f7267f2288dff0e17e7df5d
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223129"
---
# <a name="inf-profileitems-directive"></a>INF ProfileItems 指令


**注意：**  如果要生成通用或移动驱动程序包，则此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

在[**INF *DDInstall*节**](inf-ddinstall-section.md)中使用**ProfileItems**指令来列出一个或多个*配置文件项-* 包括要添加到 "开始" 菜单或从 "开始" 菜单中删除的项或组的部分。

```inf
[DDInstall] 
 
ProfileItems=profile-items-section[,profile-items-section]...
...
```

**ProfileItems**指令引用的每个命名部分都具有以下形式：

```inf
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

Windows XP 和更高版本的 Windows 支持此指令。

## <a name="entries"></a>条目


<a href="" id="name-link-name--name-attributes-"></a>**Name =**<em>链接名称</em>\[**，**<em>名称-属性</em>\]  
*链接名称*指定菜单项或组的链接的名称，不含 *.lnk*扩展名。 此值可以是在 INF 文件的[**字符串**](inf-strings-section.md)部分中定义的字符串或%*strkey*% 令牌。 如果未指定**DisplayResource**项，则*链接名称*也是显示字符串。

可选的*name-attributes*值指定影响菜单项上操作的一个或多个标志。 此值表示为系统定义的标志值的运算位掩码。 可能的标志包括：

<a href="" id="0x00000001--flg-profitem-currentuser-"></a>**0x00000001** （FLG_PROFITEM_CURRENTUSER）  
指示 Windows 创建或删除当前用户的配置文件中的 "开始" 菜单项。 如果未指定此标志，则 Windows 将为所有用户处理该项。

<a href="" id="0x00000002---flg-profitem-delete-"></a>**0x00000002** （FLG_PROFITEM_DELETE）  
指示 Windows 删除菜单项。 如果未指定此标志，则创建项。

<a href="" id="0x00000004--flg-profitem-group-"></a>**0x00000004** （FLG_PROFITEM_GROUP）  
指示 Windows 创建或删除 "启动\\程序" 下的 "开始" 菜单组。 如果未指定此标志，则 Windows 将创建或删除菜单项，而不是菜单组。

如果未指定标志，则 Windows 将为所有用户创建菜单项。

<a href="" id="cmdline-dirid--subdir--filename"></a>**CmdLine =**<em>dirid</em>**，**\[*subdir*\]**，**<em>filename</em>  
*Dirid*指定一个值，该值标识命令程序所在的目录。 例如， *dirid* 11 表示系统目录。 可能的*dirid*值列在[**DestinationDirs**](inf-destinationdirs-section.md)部分的*dirid*值的说明中。

如果存在*subdir*字符串，则命令程序位于*dirid*引用的目录的子目录中。 *Subdir*指定子目录。 如果未指定*subdir* ，则程序位于*dirid*引用的目录中。

*Filename*指定与菜单项关联的程序的名称。

<a href="" id="subdir-path"></a>**SubDir =**<em>path</em>  
此可选条目指定菜单项所在的 "启动\\程序" 下的子目录（子菜单）。 如果省略此项，则路径默认为 "启动\\程序"。

例如，如果 "*配置文件项" 部分*包含 "Subdir = 配件\\游戏" 条目，则在 "启动\\程序\\附件\\" 游戏子菜单中创建或删除菜单项。

**注意**  如果为*名称-属性*指定了 FLG_PROFITEM_GROUP，则将忽略**SubDir**条目。

 

<a href="" id="workingdir-wd-dirid--wd-subdir-"></a>**WorkingDir =**<em>wd-dirid</em>\[**，**<em>wd-subdir</em>\]  
此可选条目指定命令程序的工作目录。 如果省略此项，则工作目录将默认为命令程序所在的目录。

*Wd-dirid*值标识工作目录。 有关可能的*dirid*值的列表，请参阅[使用 Dirids](using-dirids.md)。

*Wd-subdir*字符串（如果存在）将*wd-dirid*的子目录指定为工作目录。 使用此参数可指定不具有系统定义的*dirid*的目录。 如果省略此参数， *wd-dirid*值将单独指定工作目录。

<a href="" id="iconpath-icon-dirid--icon-subdir--icon-filename"></a>**IconPath =**<em>dirid</em>**，**\[icon-*subdir*\]**，**<em>icon filename</em>  
此可选条目指定包含菜单项的图标的文件的位置。

*Dirid*字符串标识包含图标的 DLL 的目录。 有关可能的*dirid*值的列表，请参阅[使用 Dirids](using-dirids.md)。

*图标-subdir*值（如果存在）指示 DLL 位于*dirid*的子目录中。 *Subdir*值指定子目录。

*图标 filename*值指定包含该图标的 DLL。

如果省略此项，则 Windows 将在**CmdLine**项中指定的文件中查找图标。

<a href="" id="iconindex-index-value"></a>**IconIndex =**<em>索引-值</em>  
此可选条目指定 DLL 中要用于菜单项的图标。 有关如何为 DLL 中的图标编制索引的信息，请参阅 Microsoft Windows SDK 文档。

如果指定了**IconPath**项，则*索引值*索引到该 DLL。 否则，此值将索引到在**CmdLine**项中指定的文件。

<a href="" id="hotkey-hotkey-value"></a>**热键 =**<em>热键-值</em>  
此可选条目指定菜单项的键盘快捷键。

有关热键的详细信息，请参阅 Windows SDK 文档。

<a href="" id="infotip-info-tip"></a>**Infotip=**<em>信息提示 = 信息提示</em>  
此可选条目指定菜单项的信息提示。

此值可以是在 INF 文件的[**字符串**](inf-strings-section.md)部分中定义的字符串或%*strkey*% 令牌。

*信息提示*值还可以指定为 **"@**<em>ResDllPath</em>**\\**<em>ResDll</em>**，-**<em>resid 标识</em>**"**，其中*ResDllPath*和*ResDll*指定资源 DLL 的路径和文件名，-*resid 标识*是表示资源 ID 的负值。

使用此格式可支持 Windows 多语言用户界面（MUI）。 示例如下所示：

```inf
InfoTip = "@%11%\shell32.dll,-22531"
```

<a href="" id="displayresource--resdllpath-resdll--resid"></a>**DisplayResource = "**<em>ResDllPath\\ResDll</em>**"，**<em>resid 标识</em>  
此可选条目指定一个字符串资源，用于标识要在 "开始" 菜单中用作快捷方式或组的显示名称的可本地化的字符串。

*ResDllPath*和*RESDLL*指定资源 DLL 的路径和文件名，而*resid 标识*是表示资源 ID 的正值。 示例如下所示：

```inf
DisplayResource="%11%\shell32.dll",22019
```

使用此项可支持 Windows 多语言用户界面（MUI）。 如果未使用此项，则显示**名称**项指定的字符串。

<a name="remarks"></a>备注
-------

给定的*配置文件项-节*名称在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

每个*配置文件项-部分*包含有关创建或删除一个 "开始" 菜单项或组的详细信息。 若要从一个 INF 操作多个菜单项或组，请创建多个*profile-items 节*，并列出**ProfileItems**指令中的部分。

可以使用%*strkey*% 令牌来指定*配置文件项-节*项中指定的任何字符串参数，如[INF 文件一般语法规则](general-syntax-rules-for-inf-files.md)中所述。

<a name="examples"></a>示例
--------

以下 INF 文件摘录演示了如何使用*配置文件项-部分*将计算器添加到 "开始" 菜单。

```inf
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

以下 INF 文件摘录演示了如何使用**DisplayResource**条目来安装相同的软件，以创建本地化的菜单项。

```inf
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

 

 






