---
title: INF SourceDisksNames 节
description: SourceDisksNames 节标识了包含要在安装过程中传输到目标计算机的源文件的分发磁盘或 CD-ROM 光盘。
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
ms.openlocfilehash: 38100bc721bd4c2846b32621eed0a2b36679c9e7
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361361"
---
# <a name="inf-sourcedisksnames-section"></a>INF SourceDisksNames 节


**SourceDisksNames** 节标识了包含要在安装过程中传输到目标计算机的源文件的分发磁盘或 cd-rom 光盘。

```inf
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

## <a name="entries"></a>项


<a href="" id="diskid"></a>*diskid*  
指定标识源磁盘的非负整数（十进制格式）。 此值不能要求超过4个字节的存储空间。 如果有多个源磁盘用于分发，此部分中的每个 *diskid* 条目都必须有一个唯一值，如 **1** 、 **2** 、 **3** 等。

<a href="" id="disk-description"></a>*磁盘-描述*  
指定% *strkey* % 令牌或 **"**<em>带引号的字符串</em>**"** ，描述由 *diskid* 标识的磁盘的内容和/或用途。 例如，在安装过程中，安装程序可以将此字符串的值显示给最终用户，以标识在安装过程的特定阶段要插入驱动器的源磁盘。

本部分中的每个% *strkey* % 规范必须在 INF 的 **字符串** 部分中定义。 不是% *strkey* % 令牌的任何 *磁盘描述* 都是用户可见的字符串，必须由双引号字符分隔 ( **"** ) （如果它有任何前导空格或尾随空格）。

<a href="" id="tag-or-cab-file"></a>*标记或 cab 文件*  
此可选值指定在分发磁盘上提供的 *标记文件* 或 *cabinet ( .cab) 文件* 的名称，无论是在 *安装根目录* 中还是在 *path* 指定的子目录中（如果有）。 该值仅应指定文件的名称和扩展名，而不应指定任何目录或子目录。

Windows 使用标记文件来验证用户是否插入了正确的安装磁盘。 标记文件是可移动媒体所必需的，并且对于固定媒体是可选的。

如果 Windows 无法在安装介质上按名称找到安装文件，并且 *标记或 cab 文件* 具有扩展名，则为 **。**<em>cab</em>，Windows 将其用作包含安装文件的 cab 文件的名称。

如果为。指定了 *cab* 扩展，Windows 将该文件视为标记文件和 cabinet 文件，如下面的 " **备注** " 部分所述。

对于 Windows XP 和更高版本的 Windows，还应查看 *标志* 和 *标记文件* 条目值。

<a href="" id="unused"></a>*用*  
Windows 2000 和更高版本的 Windows 不再支持此项。

<a href="" id="path"></a>*通道*  
此可选值指定分发磁盘上包含源文件的目录路径。 *路径* 相对于 *安装根* ，表示为 **\\** <em>dirname1</em> **\\** <em>dirname2</em>.。。依此类推。 如果在某个条目中省略此值，则假定文件位于分发磁盘的安装根目录中。

可以使用 [**INF SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md) 来指定包含源文件的相对于给定路径目录的子目录。 但标记文件和 *cabinet 文件* 必须位于给定的路径目录中或安装根目录中。

<a href="" id="flags"></a>*随意*  
从 Windows XP 开始，将此设置为 **0x10** 将强制 Windows 使用 *标记或 cab 文件* 作为 cabinet 文件名，并将 *标记文件* 用作标记文件名。 否则， *标志* 仅供内部使用。

<a href="" id="tag-file"></a>*标记文件*  
从 Windows XP 开始，如果 *标志* 设置为 **0x10** ，则此可选值指定在分发介质上提供的 *标记文件* 的名称，无论是在 *安装根目录* 中，还是在 *path* 指定的子目录中。 该值应指定不含路径信息的文件名和扩展名。 有关详细信息，请参阅“备注”部分。

<a name="remarks"></a>备注
-------

**SourceDisksNames** 节可以包含任意数量的条目，每个条目对应于每个分发磁盘。 具有 **SourceDisksNames** 部分的任何 inf 都必须具有 [**INF SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)。  (按照约定， **SourceDisksNames** 和 **SourceDisksFiles** 部分遵循 [**INF 版本部分**](inf-version-section.md)。 ) 

这些部分决不会出现在系统提供的 INF 文件中。 相反，系统提供的 INF 文件会在其 **版本** 部分中指定 **LayoutFile** 项。

**SourceDisksNames** 节中的条目可以采用两种格式，其中一种格式仅在 windows XP 和更高版本的 windows 中受支持。

在第一种格式中， *标记或 cab 文件* 参数可以指定 *标记文件* 或 *cabinet 文件* 。 当遇到此格式时，Windows 使用以下算法：

1.  将 *标记或 cab 文件* 值视为标记文件名，并在安装介质上查找文件。 如果介质是可移动的并且找不到标记文件，则提示用户输入正确的介质。 如果介质是固定的，并且找不到标记文件和第一个要安装的文件，则提示用户输入正确的介质。
2.  尝试直接从介质中复制安装文件。
3.  将 *标记或 cab 文件* 值视为 .cab 文件，然后查找文件。
4.  尝试从 *.cab* 文件复制安装文件。
5.  提示用户找不到文件。

Windows XP 和更高版本的 Windows 支持第二种格式。 使用此格式，可以使用 *标记或 cab 文件* 、 *标志* 和 *标记文件* 项来指定 *.cab* 文件和标记文件。 当遇到此格式时，Windows 使用以下算法：

1.  如果安装介质是可移动的，请查找与 *标记文件* 指定的文件名相匹配的标记文件。 如果找不到该文件，则提示用户输入正确的介质。 如果介质是固定的，请查找标记文件或 cabinet 文件。 如果未找到任何文件，则提示用户输入正确的介质。
2.  尝试复制由 *标记或 cab 文件* 指定的 *.cab* 文件中的安装文件。
3.  提示用户找不到文件。

无论采用哪种格式，都必须为驱动程序文件的每个版本提供不同的标记文件，并具有不同的文件名。

若要支持在多个系统体系结构上分发驱动程序文件，可以通过将 **SourceDisksNames** 添加到 **x86** 、 **ia64** 或 **amd64** 扩展名来指定特定于体系结构的 **SourceDisksNames** 部分。

请注意，与其他部分（如 *DDInstall* ）不同， **SourceDisksNames** 节的平台扩展不是 **ntx86** 、 **ntia64** 或 **ntamd64** 。 例如，若要为基于 x86 的系统指定源磁盘名称部分，请使用 **SourceDisksNames** 部分，而不是 **SourceDisksNames。 ntx86** 节。 同样，可以使用 **SourceDisksNames** 部分指定基于 Itanium 的系统，使用 **SourceDisksNames** 部分指定基于 x64 的系统。

在安装过程中，Setupapi.log 函数在使用通用节之前查找特定于体系结构的 **SourceDisksNames** 部分。 例如，如果在基于 x86 的平台上安装期间 INF 文件引用磁盘 "2"，则 [setupapi.log](setupapi.md)函数将在 **SourceDisksNames** 中查找磁盘 "2 **" 的条目** 。

Setupapi.log 函数使用 **SourceDisksNames** 和 **SourceDisksNames。** 与相关 [**SourceDisksFiles**](inf-sourcedisksfiles-section.md)部分位于同一 INF 文件中的 <em>体系结构</em>部分。

<a name="examples"></a>示例
--------

在下面的示例中，所有 Windows 平台的 *write.exe* 文件都是相同的，位于 cd-rom 分发光盘上安装根目录下的 *\\ 公共* 子目录中。 *cmd.exe* 文件是仅在基于 x86 的平台上使用的特定于平台的文件。

```inf
[SourceDisksNames]
1 = "Windows NT CD-ROM",file.tag,,\common

[SourceDisksNames.x86]
2 = "Windows NT CD-ROM",file.tag,,\x86

[SourceDisksFiles]
write.exe = 1
cmd.exe = 2
```

下面的示例使用包含 *标记* 文件和 *.cab* 文件的单独规范的条目。

```inf
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

 

 






