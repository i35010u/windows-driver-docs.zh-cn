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
ms.openlocfilehash: 2d5609c42f721688632bb6c70405057993588fa3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371075"
---
# <a name="inf-copyfiles-directive"></a>INF CopyFiles 指令


一个**CopyFiles**指令可以执行以下任一操作：

-   会导致单个文件要复制的源媒体中的默认目标目录。
-   引用一个或多个 INF 编写器定义中每个指定要复制到目标的源媒体中的文件列表 INF 部分。

```ini
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

一个**CopyFiles**指令可以指定任何正式语法语句中所示的部分内。 此外可以在任何以下 INF 部分中指定此指令：

-   *添加接口部分*引用的 INF [ **AddInterface** ](inf-addinterface-directive.md)指令[ * **DDInstall *。接口**](inf-ddinstall-interfaces-section.md)部分。
-   *安装接口部分*INF 中引用[ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)部分

每个命名部分引用的**CopyFiles**指令具有以下形式的一个或多个条目：

```ini
[file-list-section]
destination-file-name[,[source-file-name][,[unused][,flag]]]
...
```

INF 编写器的定义*文件列表部分*可以有任意数量的条目，每个单独的行上。

每个*文件列表部分*可以具有可选的相关联<em>文件列表部分</em>**安全**部分中的以下形式：

```ini
[file-list-section.security]
"security-descriptor-string"
```

## <a name="entries"></a>条目


<a href="" id="destination-file-name"></a>*destination-file-name*  
指定目标文件的名称。 如果没有*源文件名*是，此规范也是源文件的名称。

<a href="" id="source-file-name"></a>*source-file-name*  
指定源文件的名称。 如果文件复制操作的源和目标文件名称相同，*源文件名*可以省略。

<a href="" id="unused"></a>*未使用*  
在 Windows 2000 和更高版本的 Windows 中不再支持此项。

<a href="" id="flag"></a>*flag*  
这些可选标志，以十六进制表示法或为十进制值中的部分条目，表示可用于控制如何 （或是否） 将特定的源文件复制到目标。 可以指定一个或多个系统定义的以下标志的 （或运算） 值。 但是，某些这些标志是互斥的：

<a href="" id="0x00000001---copyflg-warn-if-skip--"></a>**0x00000001** (COPYFLG_WARN_IF_SKIP)   
如果用户选择不用于复制文件，将发送一条警告。 此标志和下一步是互斥的且都已进行数字签名的 INF 文件不相关。

<a href="" id="0x00000002--copyflg-noskip-"></a>**0x00000002** (COPYFLG_NOSKIP)  
不允许用户跳过该文件复制。 如果此标志为隐式[驱动程序包](driver-packages.md)进行签名。

<a href="" id="0x00000004--copyflg-noversioncheck-"></a>**0x00000004** (COPYFLG_NOVERSIONCHECK)  
忽略文件版本和目标目录中的现有文件上写入。 此标志与两个互相排斥。 此标志与数字签名的 INF 文件无关。

<a href="" id="0x00000008--copyflg-force-file-in-use-"></a>**0x00000008** (COPYFLG_FORCE_FILE_IN_USE)  
强制使用文件中的行为： 它当前处于打开状态时不将其复制通过具有相同名称的现有文件。 以便可以重命名并在下次重启发生时使用，而不是，复制给定的源文件以一个临时名称。

<a href="" id="0x00000010--copyflg-no-overwrite-"></a>**0x00000010** (COPYFLG_NO_OVERWRITE)  
不要使用相同名称的源文件替换的目标目录中的现有文件。 此标志不能与任何其他标志组合。

<a href="" id="0x00000020--copyflg-no-version-dialog--"></a>**0x00000020** (COPYFLG_NO_VERSION_DIALOG)   
不会覆盖目标目录中使用的源文件的文件如果现有的文件比源文件新。

较新的检查目的是使用文件版本中，从 VS_VERSIONINFO 文件版本资源中提取。 有关详细信息，请参阅 https://docs.microsoft.com/windows/desktop/menurc/version-information。 如果目标文件不是一个可执行文件或资源的映像，或该文件不包含的文件版本信息，则设备安装会假定目标文件是较旧。 

<a href="" id="0x00000040---copyflg-overwrite-older-only-"></a>**0x00000040** (COPYFLG_OVERWRITE_OLDER_ONLY)  
将源文件复制到目标目录中，仅当目标上的文件已被较新版本取代。 此标志与数字签名的 INF 文件无关。 版本检查作为 COPYFLG_NO_VERSION_DIALOG 中所述，使用相同的过程。

<a href="" id="0x00000400--copyflg-replaceonly--"></a>**0x00000400** (COPYFLG_REPLACEONLY)   
仅当该文件已存在目标目录中，请将源文件复制到目标目录。

<a href="" id="0x00000800--copyflg-nodecomp--"></a>**0x00000800** (COPYFLG_NODECOMP)   
(Windows 7 及更高版本)将源文件复制到目标目录中，而无需解压缩源文件，如果已进行压缩。

<a href="" id="0x00001000--copyflg-replace-boot-file-"></a>**0x00001000** (COPYFLG_REPLACE_BOOT_FILE)  
此文件是所需的系统加载程序。 系统将提示用户重新启动系统。

<a href="" id="0x00002000--copyflg-noprune-"></a>**0x00002000** (COPYFLG_NOPRUNE)  
不要删除此操作作为优化结果。

例如，Windows 可能会确定该文件复制操作不需要因为文件已存在。 但是，INF 的编写器知道该操作是必需的并且指示 Windows 重写其优化并执行文件操作。

此标志可以用于确保文件复制如果他们还可以指定在 INF [ **DelFiles** ](inf-delfiles-directive.md)指令或 INF [ **RenFiles** ](inf-renfiles-directive.md)指令。

<a href="" id="0x00004000--copyflg-in-use-rename-"></a>**0x00004000** (COPYFLG_IN_USE_RENAME)  
如果不能复制的源文件，因为正在使用目标文件，重命名目标文件，然后将源文件复制到目标文件，并删除已重命名的目标文件。 如果目标文件不能重命名，完成复制操作期间在下次系统重新启动。 如果不能删除已重命名的目标文件，在下次系统重新启动过程中删除已重命名的目标文件。

<a href="" id="security-descriptor-string"></a>*security-descriptor-string*  
指定要应用于命名复制的所有文件的安全描述符*文件列表部分*。 *安全描述符字符串*是标记，则指示 DACL 的字符串 (**d:**) 安全组件。

有关安全描述符字符串的信息，请参阅[安全描述符定义语言 (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379567)。 有关的安全描述符字符串格式的信息，请参阅安全描述符定义语言 (Windows)。

如果<em>文件列表部分</em>**安全**部分未指定，则文件继承的文件复制到其中的目录的安全特征。

如果<em>文件列表部分</em>**安全**指定部分，以便进行安装和升级的设备和系统服务包必须包含以下 ACE:

-   (A;GA;;SY) − 授予对本地系统的所有访问。
-   (A;GA;;BA) − 向内置管理员授予的所有访问。

不要*不*指定对非特权用户授予写入权限的 ACE 字符串。

有关如何指定安全描述符的详细信息，请参阅[创建安全的设备安装](creating-secure-device-installations.md)。

<a name="remarks"></a>备注
-------

Windows 仅复制[驱动程序包](driver-packages.md)到其目标位置，如果该文件具有 INF 的驱动程序安装的一部分**CopyFiles**指令。 时它将文件复制，操作系统将自动生成临时文件的名称，如有必要，并将复制的源文件重命名操作系统启动下一次。

INF 文件编写器还必须提供通过使用 INF 源媒体中复制的文件的路径规范[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)部分和 INF [ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分，以显式指定的源媒体中的每个源文件的 INF 文件的相对路径。

复制操作的目标受[ **INF DestinationDirs 部分**](inf-destinationdirs-section.md)。 本部分中控件所有文件复制操作的目标，如下所示：

- 如果引用的指定部分**CopyFiles**指令有一个对应的条目[ **DestinationDirs** ](inf-destinationdirs-section.md)相同 INF，明确指定条目的部分目标目标目录中的命名的节列出的所有文件都复制到其中。 如果在未列出的命名的节**DestinationDirs**部分中，Windows 使用**DefaultDestDir**中的条目**DestinationDirs** INF 文件部分。
- 如果**CopyFiles**指令使用**@** <em>filename</em>语法，Windows 使用**DefaultDestDir** 中的条目**DestinationDirs** INF 文件部分。

以下几点适用于 INF **CopyFiles**指令：

- 每个*文件列表部分*名称必须是唯一的 INF 文件，但它可以被**CopyFiles**， [ **DelFiles**](inf-delfiles-directive.md)，或[**RenFiles** ](inf-renfiles-directive.md)指令相同的 INF 文件中的其他位置。 节名称必须遵循中所述的常规规则[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。
- 文件中指定的名称**@** <em>filename</em>或*文件列表部分*项必须是源媒体上的文件的确切名称。 不能使用 %*strkey*%令牌指定的文件的名称。 详细了解 %*strkey*%令牌，请参阅[ **INF 字符串部分**](inf-strings-section.md)。
- **CopyFiles**指令不支持修饰*文件列表部分*名称与系统定义的平台扩展 (**.nt**， **.ntx86**， **.ntia64**，或 **.ntamd64**)。
- 不要使用**CopyFiles**指令以将 INF 文件复制。 有关详细信息，请参阅[复制 INF 文件](copying-inf-files.md)。

从 Windows Vista 开始，以下几点也适用于 INF **CopyFiles**指令：

-   当 DIFx 工具预安装中的驱动程序包[驱动程序存储区](driver-store.md)，它们仅将复制文件从驱动程序包源到驱动程序存储区如果文件具有相应 INF **CopyFiles**指令。
-   作为 Windows 升级的一部分，Windows 将仅复制到驱动程序包文件[驱动程序存储区](driver-store.md)如果文件具有 INF 驱动程序迁移的一部分**CopyFiles**指令。

<a name="examples"></a>示例
--------

此示例演示如何[ **SourceDisksNames**](inf-sourcedisksnames-section.md)， [ **SourceDisksFiles**](inf-sourcedisksfiles-section.md)，并[ **DestinationDirs** ](inf-destinationdirs-section.md)部分处理简单设备驱动程序 INF 中指定的路径复制文件 （和删除文件） 发生的操作。 (还作为示例的以前使用同一个 INF [**版本**](inf-version-section.md)， **SourceDisksNames**，以及**SourceDisksFiles**部分。)

```ini
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

此示例演示如何**CopyFiles**中，可以使用指令[ * **DDInstall *。共同安装程序**](inf-ddinstall-coinstallers-section.md)部分提供了两个特定于设备的共同安装程序以补充系统特定于设备的类型类安装程序的 INF 处理的设备驱动程序 INF。

```ini
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

如前面的示例中所示，可以从提供程序的名称构造的新的特定于设备的共同安装程序的名称 (显示为此处*Xx*) 和每个此类共同安装程序 DLL 的用途 (显示为此处*PreInst*并*PostInst*)。

有关如何使用 INF 的其他示例**CopyFiles**指令，请参阅 INF 文件中包含的设备驱动程序示例*src* Windows 驱动程序工具包 (WDK) 的目录。

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。接口**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**Strings**](inf-strings-section.md)

[**版本**](inf-version-section.md)

 

 






