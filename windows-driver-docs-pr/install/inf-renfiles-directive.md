---
title: INF RenFiles 指令
description: RenFiles 指令引用 INF 文件，这将导致对在其中指定引用的 RenFiles 指令的部分操作的上下文中的文件要重命名该列表中的其他位置 INF 编写器定义部分。
ms.assetid: 269171f7-88f6-47bb-9997-8fdcbe3fa688
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
ms.openlocfilehash: 091ef81745c7af19203f6d45dd16d0638a176193
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534044"
---
# <a name="inf-renfiles-directive"></a>INF RenFiles 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**RenFiles**指令引用 INF 文件，这将导致对在其中的内容的操作的上下文中的文件要重命名该列表中的其他位置 INF 编写器定义部分引用**RenFiles**指定指令。

```ini
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

一个**RenFiles**指令可以指定任何正式语法语句中所示的部分内。 此外可以在任何 INF 编写器定义以下各节中指定此指令：

-   *添加接口部分*所引用的[ **AddInterface** ](inf-addinterface-directive.md)指令[ * **DDInstall *。接口**](inf-ddinstall-interfaces-section.md)部分。
-   *安装接口部分*中引用[ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)部分。

每个命名部分引用的**RenFiles**指令具有以下形式的一个或多个条目：

```ini
[file-list-section]
 
new-dest-file-name,old-source-file-name 
...
```

一个*文件列表部分*可以有任意数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="new-dest-file-name"></a>*new-dest-file-name*  
指定要提供给目标上的文件的新名称。

<a href="" id="old-source-file-name"></a>*old-source-file-name*  
指定文件的旧名称。

<a name="remarks"></a>备注
-------

**重要**  必须谨慎使用此指令。 我们强烈建议不要使用**RenFiles**指令 Plug and play INF 文件中 (PnP) 函数驱动程序。

 

任何*文件列表部分*名称必须是唯一的 INF 文件，但它可以被[ **CopyFiles**](inf-copyfiles-directive.md)， **DelFiles**，或**RenFiles**指令相同 INF 中的其他位置。 此类 INF 编写器定义的节名称必须遵循的一般规则用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

**RenFiles**指令不支持修饰*文件列表部分*名称与系统定义的平台扩展 (**.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，或 **.ntarm64**)。

[ **DestinationDirs** ](inf-destinationdirs-section.md) INF 文件一部分的所有文件重命名操作，而不考虑包含特定的部分控制目标**RenFiles**指令。 以下规则描述该文件重命名操作：

-   如果引用的指定部分**RenFiles**指令有一个对应的条目[ **DestinationDirs** ](inf-destinationdirs-section.md)相同 INF，明确指定条目中的部分目标目标目录。 在命名的节中列出的所有文件在目标上进行重都命名这些源文件被复制前。
-   如果命名的节中未列出**DestinationDirs**部分中，Windows 使用*DefaultDestDir*中的条目**DestinationDirs** INF 部分。

**请注意**  不能使用 %*strkey*%令牌来指定新的或旧的文件名。 详细了解 %*strkey*%令牌，请参阅[ **INF 字符串部分**](inf-strings-section.md)。

 

<a name="examples"></a>示例
--------

此示例演示引用一个部分**RenFiles**指令。

```ini
[RenameOldFilesSec]
devfile41.sav, devfile41.sys
```

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

**DelFiles**
[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**Strings**](inf-strings-section.md)

[**版本**](inf-version-section.md)

 

 






