---
title: 使用 AgeStore
description: 使用 AgeStore
keywords:
- AgeStore，使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f64309812a5f57212fe01f3fd03458da1db72ec8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803193"
---
# <a name="using-agestore"></a>使用 AgeStore


AgeStore 是一种工具，它基于其上次访问日期删除目录或目录树中的文件。 其主要用途是从符号服务器或源服务器使用的下游存储中删除旧文件，以节省磁盘空间。 它还可用作常规文件删除工具。

AgeStore 可以删除 (*目标目录*) 的单个目录中的所有文件，或 (*目标树*) 中的所有目录中的所有文件。 -S 选项指示将以整个树为目标。

有三种方法可以指定要删除的目标目录或目标树中的哪些文件。 Agestore = Month 年日期的命令将删除在指定日期之前上次访问的所有文件。 Agestore = NumberOfDays 命令将删除上次访问时间超过指定天数的所有文件。 Agestore = SizeRemaining 命令将删除目标目录或目标树中的所有文件，以最近访问最少的文件开头，直到剩余文件的总大小小于或等于 *SizeRemaining*。

例如，下面的命令删除在 \\ 2008 年1月7日之前访问的 C： MyDir 中的所有文件：

```console
agestore c:\mydir -date=01-07-2008
```

以下命令将删除目录树中从到 C： downstreamstore 的目录树中的所有文件 \\ \\ ，这些符号是在三十天前最后一次访问的：

```console
agestore c:\symbols\downstreamstore -days=30 -s
```

以下命令将删除目录树中从到 C： downstreamstore 的目录树中的文件 \\ \\ ，从访问时间最长的之前开始，直到此树中所有文件的总大小小于或等于50000字节：

```console
agestore c:\symbols\downstreamstore -size=50000 -s
```

-L 选项导致 AgeStore 不删除任何文件，只是列出在没有此选项的情况下删除的所有文件。 在使用任何 AgeStore 命令之前，你应运行添加了-l 选项的预期命令，以验证它是否将正好删除你要删除的文件。

有关完整的命令行语法，请参阅 [**AgeStore Command-Line 选项**](agestore-command-line-options.md)。

### <a name="span-idrunning_agestore_on_windows_vista_and_laterspanspan-idrunning_agestore_on_windows_vista_and_laterspanrunning-agestore-on-windows-vista-and-later"></a><span id="running_agestore_on_windows_vista_and_later"></span><span id="RUNNING_AGESTORE_ON_WINDOWS_VISTA_AND_LATER"></span>在 Windows Vista 和更高版本上运行 AgeStore

由于 AgeStore 根据上次访问文件的时间删除文件，因此只有在文件系统存储上次访问时间 (LAT) 数据时，才可以成功运行。 在 NTFS 文件系统中，可以启用或禁用 LAT 数据存储。 如果它被禁用，AgeStore 将不会运行，但会改为显示以下错误消息：

```console
Last-Access-Time support is disabled on this computer.
Please read the documentation for more details.
```

在 Windows Vista 和更高版本的 Windows 中，默认情况下会禁用 LAT 数据存储，因此除非你首先启用此数据，否则 AgeStore 将不会运行。

在 Windows Vista 和更高版本的 Windows 中，可以使用 FSUtil ( # A0) 工具来启用 LAT 数据的收集。 在命令提示符窗口中，发出以下命令：

```console
fsutil behavior set disablelastaccess 0 
```

若要禁用数据收集，请使用以下命令：

```console
fsutil behavior set disablelastaccess 1 
```

这些更改将在下一次重启 Windows 后生效。

FAT32 文件系统始终存储 LAT 信息 (尽管仅) 存储日期，而不存储时间。 因此，AgeStore 适用于 FAT32 文件系统。 但是，由于禁用 NTFS LAT 后 AgeStore 不会运行，因此必须启用 NTFS LAT，即使文件系统为 FAT32 也是如此。

 

 





