---
title: INF CopyFiles 指令
description: CopyFiles 指令可以执行以下任一操作
ms.assetid: 65756b1c-ea61-4bb4-90ac-4d96ceaf9665
keywords:
- INF CopyFiles 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF CopyFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10d704ae9a3031a5771b2c1fcdfdcebdd211d91c
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223265"
---
# <a name="inf-copyfiles-directive"></a>INF CopyFiles 指令


**CopyFiles**指令可以执行以下任一操作：

-   导致将单个文件从源媒体复制到默认目标目录。
-   引用 INF 中的一个或多个由 INF 编写器定义的部分，每个部分都指定要从源媒体复制到目标的文件的列表。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
CopyFiles=@filename | file-list-section[, file-list-section]... 
```

可以在正式语法语句中所示的任何部分中指定**CopyFiles**指令。 还可以在以下任何 INF 部分中指定此指令：

-   [**AddInterface**](inf-addinterface-directive.md)在*add-interface-section* [DDInstall * 中由 INF AddInterface 指令引用的添加接口部分。 *接口](inf-ddinstall-interfaces-section.md)部分。
-   INF [**InterfaceInstall32**](inf-interfaceinstall32-section.md)部分中引用的*安装界面部分*

**CopyFiles**指令引用的每个命名部分都具有以下形式的一个或多个条目：

```inf
[file-list-section]
destination-file-name[,[source-file-name][,[unused][,flag]]]
...
```

由 INF 编写器定义的*文件列表部分*可以有任意数量的条目，每个条目都在单独的行中。

每个*文件列表部分*都可以有一个可选的、关联的<em>文件列表节</em>，其中包含以下形式的 "**安全**" 部分：

```inf
[file-list-section.security]
"security-descriptor-string"
```

## <a name="entries"></a>条目


<a href="" id="destination-file-name"></a>*目标-文件名*  
指定目标文件的名称。 如果未提供*源文件名*，则此规范也是源文件的名称。

<a href="" id="source-file-name"></a>*源文件-文件名*  
指定源文件的名称。 如果文件复制操作的源和目标文件名称相同，则可以省略*源文件名*。

<a href="" id="unused"></a>*用*  
Windows 2000 和更高版本的 Windows 不再支持此项。

<a href="" id="flag"></a>*标志*  
这些可选标志（以十六进制表示法形式表示）或部分输入中的十进制值可用于控制是否将特定的源文件复制到目标。 可以为以下系统定义的标志指定一个或多个（运算）值。 但是，其中一些标志是互斥的：

<a href="" id="0x00000001---copyflg-warn-if-skip--"></a>**0x00000001** （COPYFLG_WARN_IF_SKIP）   
如果用户选择不复制文件，则发送警告。 此标志和下一标志是互斥的，并且两者都与已进行数字签名的 INF 文件无关。

<a href="" id="0x00000002--copyflg-noskip-"></a>**0x00000002** （COPYFLG_NOSKIP）  
不允许用户跳过复制文件的操作。 如果对[驱动程序包](driver-packages.md)进行了签名，则隐含此标志。

<a href="" id="0x00000004--copyflg-noversioncheck-"></a>**0x00000004** （COPYFLG_NOVERSIONCHECK）  
忽略文件版本并写入目标目录中的现有文件。 此标志和接下来的两个是互斥的。 此标志与数字签名的 INF 文件无关。

<a href="" id="0x00000008--copyflg-force-file-in-use-"></a>**0x00000008** （COPYFLG_FORCE_FILE_IN_USE）  
强制使用文件中行为：如果当前打开了同名的现有文件，请勿复制该文件。 相反，使用临时名称复制给定的源文件，以便在下次重新启动时可以重命名并使用该文件。

<a href="" id="0x00000010--copyflg-no-overwrite-"></a>**0x00000010** （COPYFLG_NO_OVERWRITE）  
不要将目标目录中的现有文件替换为具有相同名称的源文件。 此标志不能与任何其他标志组合。

<a href="" id="0x00000020--copyflg-no-version-dialog--"></a>**0x00000020** （COPYFLG_NO_VERSION_DIALOG）   
如果现有文件比源文件新，则不要使用源文件写入目标目录中的文件。

将使用文件版本完成较新的检查，如从 VS_VERSIONINFO 文件版本资源中提取。 有关详细信息，请参阅 https://docs.microsoft.com/windows/desktop/menurc/version-information。 如果目标文件不是可执行文件或资源映像，或者该文件不包含文件版本信息，则设备安装将假定目标文件较旧。 

<a href="" id="0x00000040---copyflg-overwrite-older-only-"></a>**0x00000040** （COPYFLG_OVERWRITE_OLDER_ONLY）  
仅当目标上的文件被较新版本取代时，才将源文件复制到目标目录。 此标志与数字签名的 INF 文件无关。 版本检查使用与上述 COPYFLG_NO_VERSION_DIALOG 中所述相同的过程。

<a href="" id="0x00000400--copyflg-replaceonly--"></a>**0x00000400** （COPYFLG_REPLACEONLY）   
仅当文件已存在于目标目录中时，才将源文件复制到目标目录。

<a href="" id="0x00000800--copyflg-nodecomp--"></a>**0x00000800** （COPYFLG_NODECOMP）   
（Windows 7 及更高版本）如果源文件已压缩，则将源文件复制到目标目录，而不将其解压缩。

<a href="" id="0x00001000--copyflg-replace-boot-file-"></a>**0x00001000** （COPYFLG_REPLACE_BOOT_FILE）  
此文件是系统加载程序所必需的。 系统将提示用户重新启动系统。

<a href="" id="0x00002000--copyflg-noprune-"></a>**0x00002000** （COPYFLG_NOPRUNE）  
由于优化，不要删除此操作。

例如，Windows 可能会确定文件复制操作不是必需的，因为文件已存在。 但 INF 的编写器知道该操作是必需的，并指示 Windows 重写其优化并执行文件操作。

如果文件也是在 INF [**DelFiles**](inf-delfiles-directive.md)指令或 inf [**RenFiles**](inf-renfiles-directive.md)指令中指定的，则可以使用此标志来确保复制这些文件。

<a href="" id="0x00004000--copyflg-in-use-rename-"></a>**0x00004000** （COPYFLG_IN_USE_RENAME）  
如果由于目标文件正在使用而无法复制源文件，请重命名目标文件，然后将源文件复制到目标文件，并删除重命名的目标文件。 如果无法重命名目标文件，请在下一次系统重新启动期间完成复制操作。 如果重命名的目标文件无法删除，请在下一次系统重新启动过程中删除重命名的目标文件。

<a href="" id="security-descriptor-string"></a>*安全描述符-字符串*  
指定一个安全描述符，它将应用于通过命名*文件列表部分*复制的所有文件。 *安全描述符字符串*是一个带有标记的字符串，用于指示 DACL （**D：**）安全组件。

有关安全描述符字符串的信息，请参阅[安全描述符定义语言（Windows）](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)。 有关安全描述符字符串格式的信息，请参阅安全描述符定义语言（Windows）。

如果未指定<em>文件列表节</em>，则文件将继承要将文件复制到其中的目录的安全**特性。**

如果指定了一个<em>文件列表节</em>**，则**必须包含以下 ACE，以便可以进行设备和系统 service pack 的安装和升级：

-   （A;;GA;;;SY）−授予对本地系统的所有访问权限。
-   （A;;GA;;;BA）−授予对内置管理员的所有访问权限。

不要*指定向*非特权用户授予写入权限的 ACE 字符串。

有关如何指定安全描述符的详细信息，请参阅[创建安全设备安装](creating-secure-device-installations.md)。

<a name="remarks"></a>备注
-------

如果文件具有 INF **CopyFiles**指令，则 Windows 仅将[驱动程序包](driver-packages.md)复制到其目标位置作为驱动程序安装的一部分。 当它复制文件时，操作系统会在必要时自动生成临时文件名，并在下次启动操作系统时重命名复制的源文件。

INF 文件编写器还必须为从源媒体复制的文件提供路径规范，方法是使用 INF [**SourceDisksNames**](inf-sourcedisksnames-section.md)部分和 inf [**SourceDisksFiles**](inf-sourcedisksfiles-section.md)部分显式指定每个源文件相对于源媒体中 INF 文件的路径。

复制操作的目标由[**INF DestinationDirs 部分**](inf-destinationdirs-section.md)控制。 本部分控制所有文件复制操作的目标，如下所示：

- 如果**CopyFiles**指令引用的命名节在同一 INF 的[**DestinationDirs**](inf-destinationdirs-section.md)部分中具有相应的条目，则该条目显式指定将在其中复制已命名部分中列出的所有文件的目标目标目录。 如果命名部分未在**DestinationDirs**节中列出，则 Windows 将使用 INF 文件的**DestinationDirs**部分中的**DefaultDestDir**条目。
- 如果**CopyFiles**指令使用**@** <em>filename</em>语法，则 Windows 将使用 INF 文件的**DestinationDirs**部分中的**DefaultDestDir**条目。

以下几点适用于 INF **CopyFiles**指令：

- 对于 INF 文件，每个*文件列表节*名称必须是唯一的，但可以在同一 INF 文件中的其他位置通过**CopyFiles**、 [**DelFiles**](inf-delfiles-directive.md)或[**RenFiles**](inf-renfiles-directive.md)指令引用它。 节名称必须遵循[INF 文件一般语法规则](general-syntax-rules-for-inf-files.md)中描述的常规规则。
- **@**<em>文件名</em>或*文件列表节*项中指定的文件名必须是源媒体上文件的确切名称。 不能使用%*strkey*% 令牌来指定文件名。 有关%*strkey*% 令牌的详细信息，请参阅[**INF 字符串部分**](inf-strings-section.md)。
- **CopyFiles**指令不支持使用系统定义的平台扩展（**nt**、 **. ntx86**、 **. ntia64**或**ntamd64**）修饰*文件列表节*名称。
- 请勿使用**CopyFiles**指令复制 INF 文件。 有关详细信息，请参阅[复制 INF 文件](copying-inf-files.md)。

从 Windows Vista 开始，以下点还适用于 INF **CopyFiles**指令：

-   当 DIFx 工具在[驱动程序存储区](driver-store.md)中预安装驱动程序包时，如果该文件具有相应的 INF **CopyFiles**指令，则它们仅将驱动程序包源中的文件复制到驱动程序存储区。
-   作为 Windows 升级的一部分，如果文件具有 INF **CopyFiles**指令，则 windows 仅将驱动程序包文件复制到驱动程序[存储区](driver-store.md)中。

<a name="examples"></a>示例
--------

此示例显示了[**SourceDisksNames**](inf-sourcedisksnames-section.md)、 [**SourceDisksFiles**](inf-sourcedisksfiles-section.md)和[**DestinationDirs**](inf-destinationdirs-section.md)节如何指定处理简单设备驱动程序 INF 时所发生的复制文件（以及删除文件）操作的路径。 （以前也将同一个 INF 用作[**版本**](inf-version-section.md)、 **SourceDisksNames**和**SourceDisksFiles**部分的示例。）

```inf
[SourceDisksNames]
1 = %Floppy_Description%,,,\WinNT


[SourceDisksFiles.x86]
aha154x.sys = 2,\x86 ; on distribution disk 2, in subdir \WinNT\x86

[DestinationDirs]
DefaultDestDir = 12  ; DIRID_DRIVERS 
                     ; == \System32\Drivers on Windows platforms
; ... Manufacturer and Models sections omitted here


DelFiles= AHA154X.DelFiles
 ; defines a delete-files section not shown here
; ... some other directives and sections omitted here

[AHA154X.NTx86]
CopyFiles=@AHA154x.SYS 
; ... some other directives and sections omitted here
; ...
```

此示例演示如何在**CopyFiles** [ *DDInstall 中使用 CopyFiles 指令。](inf-ddinstall-coinstallers-section.md)设备驱动程序的 inf 的 CoInstallers 部分，提供两个特定于设备的共同安装程序来补充特定于系统设备类型的类安装程序的 inf 处理。

```inf
[DestinationDirs]
XxDev_Coinstallers_CopyFiles = 11  ; DIRID_SYSTEM
; ... other file-list entries and DefaultDestDirs omitted here

; ... Manufacturer, Models, and DDInstall sections omitted here

[XxDev_Install.CoInstallers] 
CopyFiles=XxDev_Coinstallers_CopyFiles
; ... AddReg omitted here

[XxDev_Coinstallers_CopyFiles]
XxPreInst.dll   ; dev-specific co-installer run before class installer
XxPostInst.dll  ; run after class installer (post processing)
```

如前面的示例所示，可以根据提供程序的名称（此处显示为*Xx*）以及每个此类共同安装程序 DLL 的预期用途（如*PreInst*和*PostInst*所示）来构造新设备特定的共同安装程序的名称。

有关如何使用 INF **CopyFiles**指令的其他示例，请参阅 Windows 驱动程序工具包（WDK）的*src*目录中包含的设备驱动程序示例的 INF 文件。

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall*.接口**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**字符串**](inf-strings-section.md)

[**版本**](inf-version-section.md)

 

 






