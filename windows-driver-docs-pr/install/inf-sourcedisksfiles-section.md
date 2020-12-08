---
title: INF SourceDisksFiles 节
description: SourceDisksFiles 节命名在安装期间使用的源文件、安装磁盘和目录路径。
keywords:
- INF SourceDisksFiles 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF SourceDisksFiles Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 950d1cee7376b77f0d486176bae32fee6265c4d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840347"
---
# <a name="inf-sourcedisksfiles-section"></a>INF SourceDisksFiles 节


**SourceDisksFiles** 部分将在安装过程中使用的源文件命名为标识包含这些文件的安装磁盘，并在包含单个文件的分发磁盘上提供目录路径（如果有）。

为了使驱动程序文件或应用程序文件作为签名的 [驱动程序包](driver-packages.md)的一部分包含，该文件必须具有相应的 inf **SourceDisksFiles** 节条目和相应的 [**inf CopyFiles 指令**](inf-copyfiles-directive.md)。

```inf
[SourceDisksFiles] | 
[SourceDisksFiles.x86] | 
[SourceDisksFiles.arm] | (Windows 8 and later versions of Windows)
[SourceDisksFiles.arm64] | (Windows 10 version 1709 and later versions of Windows)
[SourceDisksFiles.ia64] | (Windows XP and later versions of Windows)
[SourceDisksFiles.amd64] (Windows XP and later versions of Windows)

filename=diskid[,[ subdir][,size]]
...  
```

## <a name="entries"></a>项


<a href="" id="filename"></a>*名字*  
指定源磁盘上的文件的名称。

<a href="" id="diskid"></a>*diskid*  
指定一个整数，该整数标识包含文件的源磁盘。 此值与初始 *subdir* (ectory) 路径 (如果包含命名文件的任何) 都必须在同一 INF 的 [**SourceDisksNames**](inf-sourcedisksnames-section.md) 节中定义。

<a href="" id="subdir"></a>*subdir*  
此可选值指定子目录 (相对于 **SourceDisksNames** 部分的 *路径* 值（如果指定文件所在的源磁盘上的任何) ）。

如果在某个条目中省略此值，则假定指定的源文件位于给定磁盘的 **SourceDisksFiles** 部分中指定的 *路径* 目录中，或者，如果未指定 *路径* 目录，则假定在 *安装根目录* 中。

<a href="" id="size"></a>*规格*  
此可选值指定给定文件的未压缩大小（以字节为单位）。

<a name="remarks"></a>备注
-------

**SourceDisksFiles** 节可以包含任意数量的条目，每个条目对应于分发磁盘上的每个文件。 具有 **SourceDisksFiles** 部分的任何 inf 都必须具有 [**INF SourceDisksNames 部分**](inf-sourcedisksnames-section.md)。 按照约定， **SourceDisksNames** 和 **SourceDisksFiles** 部分遵循 [**INF 版本部分**](inf-version-section.md)。  (从系统提供的 INF 中省略这些部分，而是在其 **版本** 部分中指定 **LayoutFile** 项。 ) 

每个 *文件名* 条目都必须指定源磁盘上某个文件的确切名称。 不能使用%*strkey*% 令牌来指定文件名。 有关%*strkey*% 令牌的详细信息，请参阅 [**INF 字符串部分**](inf-strings-section.md)。

若要支持在多个系统体系结构上分发驱动程序文件，可以通过将 **arm64** 扩展添加 **.ia64** 到 **SourceDisksFiles** 来指定特定于体系结构 **.amd64** 的 **SourceDisksFiles** 部分 **.arm** **。** 请注意，与其他部分（如 **_DDInstall_*_ 部分）不同，_ SourceDisksFiles 部分的平台扩展*** 不是 **ntx86**、 **ntia64** 或 **ntamd64**。

例如，若要为基于 x86 的系统指定源磁盘名称部分，请使用 **SourceDisksFiles** 部分，而不是 **SourceDisksFiles。 ntx86** 节。 同样，可以使用 **SourceDisksFiles** 部分指定基于 Itanium 的系统，使用 **SourceDisksFiles** 部分指定基于 x64 的系统。

在安装过程中，Setupapi.log 函数在使用通用节之前查找特定于体系结构的 **SourceDisksFiles** 部分。 例如，如果在基于 x86 的平台上安装期间，Windows 将复制名为 *driver.sys* 的文件，则在 [**SourceDisksFiles**] 中查找之前，它将在 [**SourceDisksFiles**] 中查找文件的描述。

**重要提示**  不要使用 **SourceDisksFiles** 部分来复制 INF 文件。 有关如何复制 INF 文件的详细信息，请参阅 [复制 inf](copying-inf-files.md)。

 

<a name="examples"></a>示例
--------

下面的示例演示了 [**SourceDisksNames**](inf-sourcedisksnames-section.md) 节和相应的 SourceDisksFiles 节。  请注意，此示例仅包含 **SourceDisksFiles** 部分，它指定了 x86 体系结构的文件。  支持另一种体系结构的 INF 需要该体系结构的相应 **SourceDisksFiles** 部分，或者使用了不支持所有体系结构的未经修饰的 [**SourceDisksFiles**] 部分。

```inf
[SourceDisksNames]
;
; diskid = description[, [tagfile] [, <unused>, subdir]]
;
1 = %Floppy_Description%,,,\WinNT

[SourceDisksFiles.x86]
aha154x.sys = 1,\x86 ; on distribution disk 1, in subdir \WinNT\x86

; ...
```

## <a name="see-also"></a>请参阅


[**CopyFiles**](inf-copyfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**字符串**](inf-strings-section.md)

[**版本**](inf-version-section.md)

 

 






