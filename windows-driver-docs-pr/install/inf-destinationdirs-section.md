---
title: INF DestinationDirs 节
description: DestinationDirs 部分指定的目标目标目录或目录的所有复制、 删除和/或重命名对其他位置中的 INF 文件按名称引用的文件的操作。
ms.assetid: fadebcb9-da4b-4daf-9e84-822447e5cb2a
keywords:
- INF DestinationDirs 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DestinationDirs Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e0df8123a9ab861b102b87e72d62d43f0eb7b6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567538"
---
# <a name="inf-destinationdirs-section"></a>INF DestinationDirs 节


一个**DestinationDirs**部分指定的目标目标目录或目录的所有复制、 删除和/或重命名对其他位置中的 INF 文件按名称引用的文件的操作。

```ini
[DestinationDirs]

[DefaultDestDir=dirid[,subdir]] 
[file-list-section=dirid[,subdir]]... 
```

## <a name="entries"></a>条目


<a href="" id="defaultdestdir-dirid--subdir-"></a>**DefaultDestDir=**<em>dirid</em>\[**,**<em>subdir</em>\]  
指定所有副本、 删除和/或重命名操作中未显式列出的文件的默认目标目录*文件列表部分*引用此处的其他条目。 若要确保文件操作始终发生在正确的目录，INF 文件，包括**Include**并**需要**条目不应指定默认目标目录。 有关详细信息，请参阅以下备注部分。

<a href="" id="file-list-section-dirid--subdir--------------"></a><em>文件列表部分</em>**=**<em>dirid</em>\[**，**<em>subdir</em> \] \] ...   
指定引用的一个部分的 INF 编写器确定名称[ **CopyFiles**](inf-copyfiles-directive.md)， [ **RenFiles**](inf-renfiles-directive.md)，或[ **DelFiles** ](inf-delfiles-directive.md)指令 INF 文件中的其他位置。 这一项是可选的如果此部分提供了**DefaultDestDir**条目和此 INF 中指定的所有复制文件操作具有相同的目标位置。 但是，任何*文件列表部分*所引用的**RenFiles**或**DelFiles** INF 中的其他位置的指令必须在此处列出。

<a href="" id="dirid"></a>*dirid*  
指定对引用的名称，可能是中的已命名的文件的操作的目标目录的目录标识符*文件列表部分*的 INF。 有关列表的常用*dirids*，请参阅[使用 Dirids](using-dirids.md)。

<a href="" id="subdir"></a>*subdir*  
指定的子目录 (和其路径下，如果任何标识的目录下的其余*dirid*) 中的文件操作的目标是给定*文件列表部分*。

<a name="remarks"></a>备注
-------

**DestinationDirs**中使用任何 INF 文件需要部分[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)引用或*文件列表部分*、 是否具有**CopyFiles**， [ **DelFiles**](inf-delfiles-directive.md)，或[ **RenFiles** ](inf-renfiles-directive.md)指令。

如果*Abc.inf*包括从另一个 INF 文件，部分*Def.inf*，并且这两个 INF 文件包含**DefaultDestDir**条目复制文件、 重命名文件或删除文件操作，Windows 会忽略 Def.inf 中指定并执行所有相应的文件操作中指定的默认目标目录中的默认目标目录*Abc.inf*。

为了确保文件操作始终发生在正确的目录中的 INF 文件包含**Include**并**需要**条目不应包括**DefaultDestDir**中的条目**DestinationDirs**部分。 相反，此类的 INF 文件应显式引用所有*文件列表部分*由指定的名称[ **CopyFiles**](inf-copyfiles-directive.md)， [ **RenFiles**](inf-renfiles-directive.md)，并[ **DelFiles** ](inf-delfiles-directive.md)中的指令**DestinationDirs**部分。

如果一个 INF 文件不包含**Include**并**需要**条目，可以使用 INF **DefaultDestDir**项以指定默认目标的复制、 重命名和删除文件INF 文件中的其他位置出现的操作：

-   [**CopyFiles** ](inf-copyfiles-directive.md)指令使用直接复制 (@*filename*) 表示法必须具有**DefaultDestDir**中的条目**DestinationDirs**的直接复制条目将显示的 INF 部分。
-   **CopyFiles**， [ **RenFiles**](inf-renfiles-directive.md)，或[ **DelFiles** ](inf-delfiles-directive.md)部分中没有直接引用**DestinationDirs**部分必须具有**DefaultDestDir**中的条目**DestinationDirs**复制、 重命名和删除文件的部分显示的 INF 部分。

<a name="examples"></a>示例
--------

此示例设置所有复制文件、 删除文件和重命名文件操作的默认目标目录。 此类简单**DestinationDirs**部分是普遍适用于新的外围设备的 INF 文件，因为此类 INF 通常只是将一组源代码文件复制到目标计算机上的单个目录。

```ini
[DestinationDirs]
DefaultDestDir = 12 ; dirid = \Drivers on WinNT platforms
```

此示例演示的一个片段**DestinationDirs**显示/视频驱动程序 INF 部分。

```ini
[DestinationDirs]
DefaultDestDir     = 11 ; dirid = \system32 on WinNT platforms

; ... 

; list of per-Manufacturer, per-Models, per-DDInstall-section, and
; CopyFiles-referenced xxx.Miniport/xxx.Display sections omitted here
; along with several other miniport/display paired drivers
; ...
vga.Miniport     = 12
vga.Display      = 11
xga.Miniport     = 12
xga.Display      = 11

; all video miniports copied into \system32\drivers on WinNT platforms
; all paired display drivers copied into \system32
```

## <a name="see-also"></a>请参阅


[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**使用 Dirids**](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)

[**版本**](inf-version-section.md)

 

 






