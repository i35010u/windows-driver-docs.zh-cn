---
title: INF SourceDisksFiles 节
description: SourceDisksFiles 节名称源代码文件、 安装磁盘和安装过程中使用的目录路径。
ms.assetid: 4a20b2e7-3371-47c1-8f51-bcc7af044382
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
ms.openlocfilehash: 410a84f32309842a2437d6c6fdd9572dd5b28b01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380218"
---
# <a name="inf-sourcedisksfiles-section"></a>INF SourceDisksFiles 节


**SourceDisksFiles**部分名称在安装过程中使用的源文件，标识包含这些文件的安装磁盘并提供的目录路径，如果有包含在分布磁盘上单个文件。

中的驱动程序文件或应用程序文件是作为一个已签名的一部分的顺序[驱动程序包](driver-packages.md)，该文件必须具有相应 INF **SourceDisksFiles**部分条目和相应[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)。

```ini
[SourceDisksFiles] | 
[SourceDisksFiles.x86] | 
[SourceDisksFiles.arm] | (Windows 8 and later versions of Windows)
[SourceDisksFiles.arm64] | (Windows 10 version 1709 and later versions of Windows)
[SourceDisksFiles.ia64] | (Windows XP and later versions of Windows)
[SourceDisksFiles.amd64] (Windows XP and later versions of Windows)

filename=diskid[,[ subdir][,size]]
...  
```

## <a name="entries"></a>条目


<a href="" id="filename"></a>*filename*  
指定源磁盘上文件的名称。

<a href="" id="diskid"></a>*diskid*  
指定用于标识包含该文件的源磁盘的整数。 此值，以及初始*subdir*(ectory) 路径 （如果有），其中包含命名的文件，必须在定义[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)相同 INF 部分。

<a href="" id="subdir"></a>*subdir*  
此可选值指定的子目录 (相对于*路径*的值**SourceDisksNames**部分中，如果有) 已命名的文件所在的位置的源磁盘上。

如果条目中省略此值，则假定命名的源文件处于*路径*中指定的目录**SourceDisksFiles**部分，了解给定磁盘或者，如果没有*路径*指定了目录，在*安装根目录*。

<a href="" id="size"></a>*size*  
此可选值以字节为单位，给定文件的指定的未压缩的大小。

<a name="remarks"></a>备注
-------

一个**SourceDisksFiles**部分可以具有任意数量的条目，一个用于分发磁盘上每个文件。 与任何 INF **SourceDisksFiles**节还必须具有[ **INF SourceDisksNames 部分**](inf-sourcedisksnames-section.md)。 按照约定， **SourceDisksNames**并**SourceDisksFiles**部分按照[ **INF 版本部分**](inf-version-section.md)。 (改为指定系统提供 INF 中省略了这些部分**LayoutFile**中的条目及其**版本**部分。)

每个*文件名*条目都必须指定源磁盘上的文件的确切名称。 不能使用 %*strkey*%令牌指定的文件的名称。 详细了解 %*strkey*%令牌，请参阅[ **INF 字符串部分**](inf-strings-section.md)。

若要支持多个系统体系结构上的驱动程序文件的分发，可以指定一个体系结构特定于**SourceDisksFiles**通过添加部分 **.x86**， **.ia64**， **.amd64**， **.arm**，或 **.arm64**扩展**SourceDisksFiles**。 请注意，与其他节，例如不同***DDInstall***部分中，为这些平台扩展**SourceDisksFiles**部分不 **.ntx86**， **。ntia64**，或 **.ntamd64**。

例如，若要指定的源磁盘对于基于 x86 的系统名称部分，使用**SourceDisksFiles.x86**部分中，不**SourceDisksFiles.ntx86**部分。 同样，使用**SourceDisksFiles.ia64**部分，以指定用于基于 Itanium 的系统和一个**SourceDisksFiles.amd64**部分以指定的基于 x64 的系统。

在安装期间，安装程序 Api 函数查找特定于体系结构**SourceDisksFiles**部分之前使用的泛型部分。 例如，如果，在安装期间的基于 x86 的平台上，Windows 复制的文件，名为*driver.sys*，则将该文件的说明中查找 [**SourceDisksFiles.x86**] 中查找之前[**SourceDisksFiles**]。

**重要**  不要使用**SourceDisksFiles**将 INF 文件复制到的部分。 有关如何将 INF 文件复制的详细信息，请参阅[复制 Inf](copying-inf-files.md)。

 

<a name="examples"></a>示例
--------

下面的示例演示[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)部分和相应的 SourceDisksFiles 节。  请注意，此示例仅具有**SourceDisksFiles.x86**部分中，指定的文件的 x86 体系结构。  支持另一个体系结构 INF 需要相应**SourceDisksFiles**部分，了解该体系结构或使用的未修饰 [**SourceDisksFiles**] 部分中，它支持所有体系结构。

```ini
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


[**CopyFiles,**](inf-copyfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**Strings**](inf-strings-section.md)

[**版本**](inf-version-section.md)

 

 






