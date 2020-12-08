---
title: INF RenFiles 指令
description: RenFiles 指令在 INF 文件中的其他位置引用由 INF 编写器定义的部分，这会导致在指定了引用 RenFiles 指令的部分中的操作上下文中重命名该文件的列表。
keywords:
- INF RenFiles 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF RenFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6778879c02bd82d43e1c8fcbd0a1e22d6a792726
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786279"
---
# <a name="inf-renfiles-directive"></a>INF RenFiles 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**RenFiles** 指令在 inf 文件中的其他位置引用由 inf 编写器定义的部分，这会导致在指定了引用 **RenFiles** 指令的部分中的操作上下文中重命名该文件的列表。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
Renfiles=file-list-section[,file-list-section]...
```

可以在正式语法语句中所示的任何部分中指定 **RenFiles** 指令。 还可以在以下任何 INF 写入器定义的部分中指定此指令：

-   [**AddInterface**](inf-addinterface-directive.md)指令在 DDInstall 中引用的 *添加接口部分* [**_DDInstall_。接口**](inf-ddinstall-interfaces-section.md)部分。
-   [**InterfaceInstall32**](inf-interfaceinstall32-section.md)节中引用的 *安装接口部分*。

**RenFiles** 指令引用的每个命名部分都具有以下形式的一个或多个条目：

```inf
[file-list-section]
 
new-dest-file-name,old-source-file-name 
...
```

*文件列表部分* 可以有任意数量的条目，每个条目都在单独的行上。

## <a name="entries"></a>项


<a href="" id="new-dest-file-name"></a>*新的-dest-文件名*  
指定要提供给目标上的文件的新名称。

<a href="" id="old-source-file-name"></a>*旧的源文件名*  
指定文件的旧名称。

<a name="remarks"></a>备注
-------

**重要提示**  必须谨慎使用此指令。 强烈建议您不要将 INF 文件中的 **RenFiles** 指令用于即插即用 (PnP) 函数驱动程序。

 

对于 INF 文件，任何 *文件列表节* 名称必须是唯一的，但它可以在同一 INF 中的其他位置通过 [**CopyFiles**](inf-copyfiles-directive.md)、 **DelFiles** 或 **RenFiles** 指令引用。 此类 INF 写入方定义的部分名称必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

**RenFiles** 指令不支持使用系统定义的平台扩展（ (**nt**、 **. ntx86**、 **ntia64**、 **ntamd64**、 **ntarm** 或 **ntarm64**) 来修饰 *文件列表节* 名称。

INF 文件的 [**DestinationDirs**](inf-destinationdirs-section.md) 部分控制所有文件重命名操作的目标，而不考虑包含特定 **RenFiles** 指令的部分。 以下规则描述了文件重命名操作：

-   如果 **RenFiles** 指令引用的命名节在同一 INF 的 [**DestinationDirs**](inf-destinationdirs-section.md) 节中具有相应的条目，则该条目显式指定目标目标目录。 在复制这些源文件之前，已命名部分中列出的所有文件都将在目标上重命名。
-   如果命名部分未在 **DestinationDirs** 节中列出，则 Windows 将使用 INF 的 **DestinationDirs** 部分中的 *DefaultDestDir* 条目。

**注意**  不能使用%*strkey*% 令牌来指定新的或旧的文件名称。 有关%*strkey*% 令牌的详细信息，请参阅 [**INF 字符串部分**](inf-strings-section.md)。

 

<a name="examples"></a>示例
--------

此示例显示了 **RenFiles** 指令引用的节。

```inf
[RenameOldFilesSec]
devfile41.sav, devfile41.sys
```

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。CoInstallers**](inf-ddinstall-coinstallers-section.md)

**DelFiles** 
[ **DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**字符串**](inf-strings-section.md)

[**版本**](inf-version-section.md)

 

 






