---
title: INF DelFiles 指令
description: DelFiles 指令引用其他位置在 INF 文件中，INF 编写器定义部分，并导致的要删除文件的列表。
ms.assetid: e163f88f-e0ab-41e7-97df-49853ec0836f
keywords:
- INF DelFiles 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DelFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca4df3872f33d49efb001c62d77b2a75008b241e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564489"
---
# <a name="inf-delfiles-directive"></a>INF DelFiles 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**DelFiles**指令引用其他位置在 INF 文件中，INF 编写器定义部分，并导致该列表中删除对在其中的内容的操作的上下文中的文件引用**DelFiles**指定指令。

```ini
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows) 
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows) 
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows) 


  
Delfiles=file-list-section[,file-list-section]... 
```

一个**DelFiles**指令可以指定任何正式语法语句中所示的部分内。 此外可以在任何 INF 编写器定义以下各节中指定此指令：

-   由引用添加的接口的部分[ **AddInterface** ](inf-addinterface-directive.md)指令[ * **DDInstall *。接口**](inf-ddinstall-interfaces-section.md)部分。
-   安装-接口-部分中引用[ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)部分

每个命名部分引用的**DelFiles**指令具有以下形式的一个或多个条目：

```ini
[file-list-section]
 
destination-file-name[,,,flag]
...
```

一个*文件列表部分*可以有任意数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="destination-file-name"></a>*destination-file-name*  
指定要从目标中删除的文件的名称。

未指定文件中列出[ **CopyFiles** ](inf-copyfiles-directive.md)指令。 如果某个文件列出在这种**CopyFiles**的引用和一个**DelFiles**-引用部分中，并且该文件是否具有有效签名的系统上当前存在，操作系统可能优化掉复制操作但执行删除操作。 这是很有可能*不*适用哪些 INF 的编写器。

**请注意**  不能使用 %*strkey*%令牌，以指定目标文件名条目。 详细了解 %*strkey*%令牌，请参阅[ **INF 字符串部分**](inf-strings-section.md)。

 

<a href="" id="flag"></a>*flag*  
此可选值可以是以下值之一所示此处或为十进制值，以十六进制表示法表示：

<a href="" id="0x00000001--delflg-in-use-"></a>**0x00000001** (DELFLG_IN_USE)  
后它在安装过程中使用可能删除的命名的文件。

如果无法删除给定的文件，因为它正在使用此 INF 在处理时，系统已重新启动之前，设置此标志中 INF 值排队文件删除操作。 否则，将删除此类文件。

<a href="" id="0x00010000---delflg-in-use1-"></a>**0x00010000** (DELFLG_IN_USE1)  
（Windows 2000 或更高版本的 Windows）此标志是 DELFLG_IN_USE 标志的高 word 版本，它具有相同的目的和效果。 仅对在基于 NT 的系统上安装，应在使用此标志。

设置此标志中 INF 值可防止在两个 INF COPYFLG_WARN_IF_SKIP 标志与冲突**DelFiles**并[ **CopyFiles** ](inf-copyfiles-directive.md)引用指令相同*文件列表部分*。

<a name="remarks"></a>备注
-------

**重要**  必须谨慎使用此指令。 我们强烈建议不要使用**DelFiles**指令 Plug and play INF 文件中 (PnP) 函数驱动程序。

 

任何*文件列表部分*名称必须是唯一的 INF 文件，但它可以被[ **CopyFiles**](inf-copyfiles-directive.md)， **DelFiles**，或[ **RenFiles** ](inf-renfiles-directive.md)指令相同 INF 中的其他位置。 此类 INF 编写器定义的节名称必须遵循的一般规则用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

**DelFiles**指令不支持修饰*文件列表部分*名称与系统定义的平台扩展 (**.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，或 **.ntarm64**)。

[ **DestinationDirs** ](inf-destinationdirs-section.md) INF 文件的部分控制的所有文件删除操作，而不考虑包含特定的部分目标**DelFiles**指令。 如果引用的指定部分**DelFiles**指令有一个对应的条目**DestinationDirs**相同 INF，该条目的部分显式指定从目标目标目录在命名的节中列出的所有文件将被都删除。 如果在未列出的命名的节**DestinationDirs**部分中，Windows 使用**DefaultDestDir** INF 中的条目。

<a name="examples"></a>示例
--------

此示例演示如何[ **DestinationDirs** ](inf-destinationdirs-section.md)部分处理简单设备驱动程序 INF 中指定删除文件操作，它的路径。

```ini
[DestinationDirs]
DefaultDestDir = 12  ; DIRID_DRIVERS 

; ... 

[AHA154X]
CopyFiles=@AHA154x.MPD
DelFiles=ASPIDEV ; defines delete-files section name
; ... some other directives and sections omitted here

[ASPIDEV]
VASPID.SYS ; name of file to be deleted, if it exists on target 
; ...
```

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

**RenFiles**
[**Strings**](inf-strings-section.md)

 

 






