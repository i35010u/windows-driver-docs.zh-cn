---
title: INF DelFiles 指令
description: DelFiles 指令引用 inf 文件中其他位置的 INF 写入器定义的部分，并导致删除该文件的列表。
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
ms.openlocfilehash: d2e9b785e417a1fb2db47d63329356978acc6cd1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813123"
---
# <a name="inf-delfiles-directive"></a>INF DelFiles 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**DelFiles** 指令引用 inf 文件中其他位置的 inf 写入器定义的部分，并导致在指定了引用 **DelFiles** 指令的部分中的操作上下文中删除该文件列表。

```inf
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

可以在正式语法语句中所示的任何部分中指定 **DelFiles** 指令。 还可以在以下任何 INF 写入器定义的部分中指定此指令：

-   [**AddInterface**](inf-addinterface-directive.md)指令在 DDInstall 中引用的添加接口部分 [**_DDInstall_。接口**](inf-ddinstall-interfaces-section.md)部分。
-   [**InterfaceInstall32**](inf-interfaceinstall32-section.md)节中引用的安装界面部分

**DelFiles** 指令引用的每个命名部分都具有以下形式的一个或多个条目：

```inf
[file-list-section]
 
destination-file-name[,,,flag]
...
```

*文件列表部分* 可以有任意数量的条目，每个条目都在单独的行上。

## <a name="entries"></a>项


<a href="" id="destination-file-name"></a>*目标-文件名*  
指定要从目标中删除的文件的名称。

不要指定 [**CopyFiles**](inf-copyfiles-directive.md) 指令中列出的文件。 如果文件同时在 **CopyFiles** 引用的和 **DelFiles** 的节中列出，并且该文件当前在具有有效签名的系统上，则操作系统可能会优化掉复制操作，但执行删除操作。 这很可能 *不* 是 INF 编写器的预期。

**注意**  不能使用%*strkey*% 令牌来指定目标文件名项。 有关%*strkey*% 令牌的详细信息，请参阅 [**INF 字符串部分**](inf-strings-section.md)。

 

<a href="" id="flag"></a>*标志*  
此可选值可以是以下值之一，以十六进制表示法表示，或以十进制值表示：

<a href="" id="0x00000001--delflg-in-use-"></a>**0x00000001** (DELFLG_IN_USE)   
删除已命名的文件，可能在安装过程中使用该文件。

在 INF 中设置此标志值会将文件删除操作排队，直到系统重新启动（如果无法删除给定文件，因为该文件在处理此 INF 时正在使用）。 否则，将不会删除此类文件。

<a href="" id="0x00010000---delflg-in-use1-"></a>**0x00010000** (DELFLG_IN_USE1)   
 (Windows 2000 或更高版本的 Windows) 此标志是 DELFLG_IN_USE 标志的高词版本，它具有相同的用途和效果。 此标志仅应在基于 NT 的系统上的安装中使用。

在 INF 中设置此标志值可防止与 INF 中的 COPYFLG_WARN_IF_SKIP 标志冲突，同时包含引用相同 *文件列表部分* 的 **DelFiles** 和 [**CopyFiles**](inf-copyfiles-directive.md)指令。

<a name="remarks"></a>备注
-------

**重要提示**  必须谨慎使用此指令。 强烈建议您不要将 INF 文件中的 **DelFiles** 指令用于即插即用 (PnP) 函数驱动程序。

 

对于 INF 文件，任何 *文件列表节* 名称必须是唯一的，但它可以在同一 INF 中的其他位置通过 [**CopyFiles**](inf-copyfiles-directive.md)、 **DelFiles** 或 [**RenFiles**](inf-renfiles-directive.md) 指令引用。 此类 INF 写入方定义的部分名称必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

**DelFiles** 指令不支持使用系统定义的平台扩展（ (**nt**、 **. ntx86**、 **ntia64**、 **ntamd64**、 **ntarm** 或 **ntarm64**) 来修饰 *文件列表节* 名称。

INF 文件的 [**DestinationDirs**](inf-destinationdirs-section.md) 部分控制所有文件删除操作的目标，而不考虑包含特定 **DelFiles** 指令的部分。 如果 **DelFiles** 指令引用的命名节在同一 INF 的 **DestinationDirs** 节中具有相应的条目，则该条目显式指定将删除已命名部分中列出的所有文件的目标目标目录。 如果命名部分未在 **DestinationDirs** 节中列出，则 Windows 将在 INF 中使用 **DefaultDestDir** 条目。

<a name="examples"></a>示例
--------

此示例显示了 [**DestinationDirs**](inf-destinationdirs-section.md) 节如何指定在处理简单设备驱动程序 INF 时所发生的删除文件操作的路径。

```inf
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

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

**RenFiles** 
[**字符串**](inf-strings-section.md)

 

 






