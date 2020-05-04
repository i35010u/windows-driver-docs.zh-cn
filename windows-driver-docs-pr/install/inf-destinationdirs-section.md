---
title: INF DestinationDirs 节
description: DestinationDirs 节指定 INF 文件中其他位置对其名称所引用的文件的所有复制、删除和/或重命名操作的目标目录。
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
ms.openlocfilehash: 81c8c448a6f5c8d5aef5ce87fe965ec7deea8fb4
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223177"
---
# <a name="inf-destinationdirs-section"></a>INF DestinationDirs 节


**DestinationDirs**节指定 INF 文件中其他位置对其名称所引用的文件的所有复制、删除和/或重命名操作的目标目录。

```inf
[DestinationDirs]

[DefaultDestDir=dirid[,subdir]] 
[file-list-section=dirid[,subdir]]... 
```

## <a name="entries"></a>条目


<a href="" id="defaultdestdir-dirid--subdir-"></a>**DefaultDestDir =**<em>dirid</em>\[**，**<em>subdir</em>\]  
指定对文件的所有复制、删除和/或重命名操作的默认目标目录，这些操作未显式列出在此处其他条目引用的*文件列表部分*。 若要确保文件操作始终出现在正确的目录中，包含 "**包含**" 和 "**需要**" 条目的 INF 文件不应指定默认目标目录。 有关更多信息，请参见下面的“备注”部分。

<a href="" id="file-list-section-dirid--subdir--------------"></a><em>文件列表-section</em>**=**<em>dirid</em>\[**，**<em>subdir</em> \] \] .。。   
指定由 inf 文件中其他位置的[**CopyFiles**](inf-copyfiles-directive.md)、 [**RenFiles**](inf-renfiles-directive.md)或[**DELFILES**](inf-delfiles-directive.md)指令引用的由 inf 编写器决定的部分名称。 如果此部分包含**DefaultDestDir**项并且此 INF 中指定的所有复制文件操作都具有相同的目标目标，则此项是可选的。 但是，INF 中其他位置的**RenFiles**或**DelFiles**指令所引用的任何*文件列表部分*都必须在此处列出。

<a href="" id="dirid"></a>*dirid*  
为名称所引用的文件（可能在 INF 的命名*文件列表部分*内）执行的操作指定目标目录的目录标识符。 有关常用*dirids*的列表，请参阅[使用 dirids](using-dirids.md)。

<a href="" id="subdir"></a>*subdir*  
指定子目录（并且其路径的其余部分，如果有的话，在*dirid*标识的目录下）成为给定*文件列表部分*中文件操作的目标。

<a name="remarks"></a>备注
-------

无论是否使用**CopyFiles**、 [**DelFiles**](inf-delfiles-directive.md)或[**RenFiles**](inf-renfiles-directive.md)指令，都需要使用[**inf CopyFiles 指令**](inf-copyfiles-directive.md)或引用*文件列表部分*的任何 INF 文件中的**DestinationDirs**部分。

如果*Abc*包含来自另一个 inf 文件和版本 *.def*的部分，并且这两个 inf 文件包含用于复制文件、重命名文件或删除文件操作的**DefaultDestDir**条目，则 Windows 将忽略在 .def 中指定的默认目标目录，并在*Abc. inf*中指定的默认目标目录中执行所有相应的文件操作。

若要确保文件操作始终出现在正确的目录中，包含和**需要**条目的 INF 文件不应在**DestinationDirs**节**中包含** **DefaultDestDir**条目。 相反，此类 INF 文件应显式引用由**DestinationDirs**部分中的[**CopyFiles**](inf-copyfiles-directive.md)、 [**RenFiles**](inf-renfiles-directive.md)和[**DelFiles**](inf-delfiles-directive.md)指令指定的所有*文件列表节*名称。

如果 INF 文件不包括 "**包括**" 和 "**需要**" 条目，则 inf 可以使用**DEFAULTDESTDIR**项来指定在 INF 文件中的其他位置出现的复制、重命名和删除文件操作的默认目标：

-   使用直接复制（@*filename*）表示法的[**CopyFiles**](inf-copyfiles-directive.md)指令必须在显示直接复制条目的 INF 的**DestinationDirs**部分中具有**DefaultDestDir**条目。
-   **DestinationDirs**部分中未直接引用的**CopyFiles**、 [**RenFiles**](inf-renfiles-directive.md)或[**DelFiles**](inf-delfiles-directive.md)节必须在 INF （其中显示了 "复制"、"重命名" 和 "删除文件" 部分）的**DefaultDestDir**部分中具有**DestinationDirs**条目。

<a name="examples"></a>示例
--------

此示例为所有复制文件、删除文件和重命名文件操作设置默认目标目录。 这种简单的**DestinationDirs**部分是用于新外围设备的 inf 文件所共有的，因为此类 inf 通常只是将一组源文件复制到目标计算机上的一个目录中。

```inf
[DestinationDirs]
DefaultDestDir = 12 ; dirid = \Drivers on WinNT platforms
```

此示例显示了 INF 对于显示/视频驱动程序的**DestinationDirs**部分的片段。

```inf
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

## <a name="see-also"></a>另请参阅


[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**使用 Dirids**](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)

[**版本**](inf-version-section.md)

 

 






