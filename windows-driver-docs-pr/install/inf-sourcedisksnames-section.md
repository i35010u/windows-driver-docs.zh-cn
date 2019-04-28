---
title: INF SourceDisksNames 节
description: SourceDisksNames 部分标识分发磁盘或包含源代码文件，以在安装过程中传输到目标计算机的 CD-ROM 光盘。
ms.assetid: ad69521c-5185-4c7b-a851-eb825b468459
keywords:
- INF SourceDisksNames 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF SourceDisksNames Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8133d47f86875787083cb74c53bd20a019eb426a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341468"
---
# <a name="inf-sourcedisksnames-section"></a>INF SourceDisksNames 节


一个**SourceDisksNames**部分标识分发磁盘或包含源代码文件，以在安装过程中传输到目标计算机的 CD-ROM 光盘。

```ini
[SourceDisksNames] |
[SourceDisksNames.x86] | 
[SourceDisksNames.arm] | (Windows 8 and later versions of Windows)
[SourceDisksNames.arm64] | (Windows 10 version 1709 and later versions of Windows)
[SourceDisksNames.ia64] | (Windows XP and later versions of Windows)
[SourceDisksNames.amd64] (Windows XP and later versions of Windows)

diskid = disk-description[,tag-or-cab-file] |
diskid = disk-description[,[tag-or-cab-file][,[unused][,path]]] |
diskid = disk-description[,[tag-or-cab-file],[unused],[path][,flags]] |
diskid = disk-description[,[tag-or-cab-file],[unused],[path],[flags][,tag-file]]  (Windows XP and later versions of Windows)
...
```

## <a name="entries"></a>条目


<a href="" id="diskid"></a>*diskid*  
指定以十进制格式，用于标识源磁盘的非负整数。 此值不能要求超过 4 个字节的存储。 如果有多个源磁盘对于分发中，每个*diskid*在本部分中的条目必须具有唯一的值，如**1**， **2**， **3**，依次类推。

<a href="" id="disk-description"></a>*disk-description*  
指定 %*strkey*%令牌或 **"**<em>带引号的字符串</em>**"** 描述的内容和/或由标识磁盘的用途*diskid*。 安装程序可以显示此字符串的值向最终用户在安装期间，例如，若要确定源磁盘，在安装过程的某个特定阶段要插入到驱动器。

每个 %*strkey*必须在 INF 中定义在本部分中的 %规范**字符串**部分。 任何*磁盘描述*，它是不是 %*strkey*%令牌是必须由两个双引号字符分隔的用户可见字符串 (**"**) 如果它具有任何前导或尾随空格。

<a href="" id="tag-or-cab-file"></a>*tag-or-cab-file*  
此可选值指定的名称*标记文件*或*cabinet (.cab) 文件*分发在磁盘上，在提供*安装根目录*或子目录中通过指定*路径*(如果有）。 该值应指定的文件名和扩展名，没有任何目录或子目录。

Windows 使用的标记文件来验证用户插入正确的安装磁盘。 标记文件所需的可移动媒体，而对于固定媒体是可选的。

如果 Windows 找不到安装文件的安装介质上的名称，并且*标记或 cab 文件*具有扩展名 **。**<em>cab</em>，Windows 将它作为包含安装文件的 cab 文件的名称。

如果。*cab*指定为扩展时，Windows 将该文件视为标记文件和 cab 文件，如以下所述**备注**部分。

对于 Windows XP 和更高版本的 Windows，另请参阅*标志*并*标记文件*条目的值。

<a href="" id="unused"></a>*未使用*  
此项不再支持 Windows 2000 和更高版本的 Windows。

<a href="" id="path"></a>*path*  
此可选值指定包含源文件的分发磁盘上的目录路径。 *路径*相对于*安装根目录*，表示为**\\** <em>dirname1</em>  **\\** <em>dirname2</em>...等等。 如果此值从条目中省略，假定文件分发磁盘的安装根目录中。

可以使用**INF SourceDisksFiles 部分**必须位于给定的路径目录中或安装根路径中。

<a href="" id="flags"></a>*flags*  
从 Windows XP 中，此值设置为**0x10**强制 Windows 以使用*标记或 cab 文件*作为 cabinet 文件名称，并使用*标记文件*作为标记文件名称。 否则为*标志*是仅供内部使用。

<a href="" id="tag-file"></a>*tag-file*  
如果从 Windows XP*标志*设置为**0x10**，此可选值指定的名称*标记文件*上分发介质，在提供*安装根*或在指定的子目录*路径*。 该值应指定文件名和扩展名不包含路径信息。 有关详细信息，请参阅“备注”部分。

<a name="remarks"></a>备注
-------

一个**SourceDisksNames**部分可以具有任意数量的条目，一个用于分发的每个磁盘。 与任何 INF **SourceDisksNames**节还必须具有[ **INF SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)。 (按照惯例， **SourceDisksNames**并**SourceDisksFiles**部分按照[ **INF 版本部分**](inf-version-section.md)。)

这些部分永远不会出现系统提供 INF 文件中。 相反，系统提供的 INF 文件指定**LayoutFile**中的条目及其**版本**部分。

中的条目**SourceDisksNames**部分可以具有两种格式，其中之一是支持仅在 Windows XP 及更高版本的 Windows 的版本之一。

在第一个格式*标记或 cab 文件*参数可以指定*标记文件*或*cab 文件*。 如果遇到这种格式，Windows 将使用以下算法：

1.  将视为*标记或 cab 文件*值作为标记文件名称，并查找安装介质上的文件。 如果媒体为可移动媒体且未找到标记文件时，提示用户输入正确的媒体。 如果可以找到标记文件和要安装的第一个文件都不固定的介质，提示用户输入正确的媒体。
2.  尝试将安装文件复制直接从该介质。
3.  将视为*标记或 cab 文件*值为.cab 文件，并查找该文件。
4.  尝试将从安装文件复制 *.cab*文件。
5.  提示用户输入找不到文件。

在 Windows XP 和更高版本的 Windows 支持第二个格式。 使用此格式，可以使用*标记或 cab 文件*，*标志*，并*标记文件*条目同时指定 *.cab*文件和标记文件。 如果遇到这种格式，Windows 将使用以下算法：

1.  如果可移动的安装介质，寻找标记匹配的文件的文件的名称指定的*标记文件*。 如果找不到该文件，提示用户输入正确的媒体。 如果该介质得到解决，查找标记文件或 cabinet 文件。 如果找到任一文件，则提示用户输入正确的媒体。
2.  尝试将从安装文件复制 *.cab*指定的文件*标记或 cab 文件*。
3.  提示用户输入找不到文件。

有关这两种格式，必须为每个版本的驱动程序文件的不同的文件名称提供不同的标记文件。

若要支持多个系统体系结构上的驱动程序文件的分发，可以指定一个体系结构特定于**SourceDisksNames**通过添加部分 **.x86**， **.ia64**，或 **.amd64**扩展**SourceDisksNames**。

请注意，与其他节，例如不同*DDInstall*部分中，为这些平台扩展**SourceDisksNames**部分不 **.ntx86**， **。ntia64**，或 **.ntamd64**。 例如，若要指定的源磁盘对于基于 x86 的系统名称部分，使用**SourceDisksNames.x86**部分中，不**SourceDisksNames.ntx86**部分。 同样，使用**SourceDisksNames.ia64**部分，以指定用于基于 Itanium 的系统和一个**SourceDisksNames.amd64**部分以指定的基于 x64 的系统。

在安装期间，安装程序 Api 函数查找特定于体系结构**SourceDisksNames**部分之前使用的泛型部分。 例如，如果在安装期间的基于 x86 的平台上，一个 INF 文件引用磁盘"2"，则[SetupAPI](setupapi.md)函数将查找磁盘"2"的条目**SourceDisksNames.x86**中查找之前**SourceDisksNames**。

安装程序 Api 函数使用**SourceDisksNames**并**SourceDisksNames。**<em>体系结构</em>部分中相同的 INF 文件作为相关[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分。

<a name="examples"></a>示例
--------

在以下示例中， *write.exe*文件是相同的所有 Windows 平台，它位于*\\常见*CD-ROM 分发光盘上安装根下的子目录，.*Cmd.exe*文件是仅在基于 x86 的平台使用一个特定于平台的文件。

```ini
[SourceDisksNames]
1 = "Windows NT CD-ROM",file.tag,,\common

[SourceDisksNames.x86]
2 = "Windows NT CD-ROM",file.tag,,\x86

[SourceDisksFiles]
write.exe = 1
cmd.exe = 2
```

下面的示例使用包含单独的规范的条目 *.tag*文件并 *.cab*文件。

```ini
[Version]
signature = "$Windows NT$"
Provider = %Msft%

[SourceDisksNames]
1 = "Dajava","Dajava.cab",,,0x10,"Dajava.tag"
2 = "Osc","Osc.cab",,,0x10,"OSC.tag"
3 = "Win","Win.cab",,,0x10,"Win.tag"
4 = "XMLDSO","XMLDSO.cab",,,0x10,"XMLDSO.tag"

[SourceDisksFiles]
ArrayBvr.class=1
BvrCallback.class=1
BvrsToRun.class=1
choice.osc=2
custom.osc=2
login.osc=2
mwcload.exe=3
mwcloadw.exe=3
mwclw32.dll=3
Atom.class=4
DTD.class=4
Entity.class=4
Entry.class=4

[DestinationDirs]
Test = 16430,InfTest    ; %SystemRoot%\System32

[DefaultInstall]
CopyFiles = Test

[Test]
ArrayBvr.class
mwcloadw.exe
Entity.class
custom.osc
BvrCallback.class
BvrsToRun.class
choice.osc
login.osc
mwcload.exe
mwclw32.dll
Atom.class
DTD.class
Entry.class

[Strings]
Msft = "Microsoft"
```

## <a name="see-also"></a>请参阅


[**DestinationDirs**](inf-destinationdirs-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**版本**](inf-version-section.md)

 

 






