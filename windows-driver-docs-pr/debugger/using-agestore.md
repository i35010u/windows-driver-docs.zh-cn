---
title: 使用 AgeStore
description: 使用 AgeStore
ms.assetid: 188eac5c-e84c-45a4-a4ea-1c9bfaa93cca
keywords:
- AgeStore，使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa9da713879906cf40472fc5350e9c98ef2f840a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541600"
---
# <a name="using-agestore"></a>使用 AgeStore


AgeStore 是一种工具，可删除文件的目录或目录树中，基于其上次访问日期。 其主要用途是用于从符号服务器或源服务器，以便节省磁盘空间使用的下游存储区中删除旧文件。 它还可以用作常规文件删除工具。

AgeStore 可以删除单个目录中的所有文件 (*目标目录*)，或在树中的所有目录中 (*目标树*)。 -S 选项指示整个树要设定为目标。

有三种方法来指定目标目录或目标树中的文件将被删除。 Agestore-日期 = 月-日-年命令删除在指定日期之前访问上一次的所有文件。 Agestore-天 = 的 NumberOfDays 命令可删除所有文件上次访问的多个指定的天前的数。 Agestore-大小 = 的 SizeRemaining 命令可删除在目标目录或目标树中的所有文件的开头的最少最近访问的文件，直到剩余文件的总大小小于或等于*SizeRemaining*.

例如，以下命令将删除 c： 驱动器中的所有文件\\MyDir 上次访问在 2008 年 1 月 7 日之前的：

```console
agestore c:\mydir -date=01-07-2008
```

以下命令将删除从属到 c： 目录树中的所有文件\\符号\\downstreamstore 上次访问超过 30 天前的：

```console
agestore c:\symbols\downstreamstore -days=30 -s
```

以下命令将删除从属到 c: 目录树中\\符号\\downstreamstore，开始使用这些访问的时间最长年前，直到此树中的所有文件的总大小是否小于或等于 50000 字节：

```console
agestore c:\symbols\downstreamstore -size=50000 -s
```

-L 选项将使 AgeStore 删除任何文件，但只是为了要列出此选项不会删除的所有文件。 在使用任何 AgeStore 命令，应使用添加-l 选项运行的是目标的命令之前，若要验证，它会删除这些文件进行准确你意图使其删除。

有关完整的命令行语法，请参阅[ **AgeStore 命令行选项**](agestore-command-line-options.md)。

### <a name="span-idrunningagestoreonwindowsvistaandlaterspanspan-idrunningagestoreonwindowsvistaandlaterspanrunning-agestore-on-windows-vista-and-later"></a><span id="running_agestore_on_windows_vista_and_later"></span><span id="RUNNING_AGESTORE_ON_WINDOWS_VISTA_AND_LATER"></span>运行 Windows Vista 及更高版本的 AgeStore

由于 AgeStore 删除根据上次访问的文件，它可以成功地运行仅当在文件系统存储上次访问时间 (LAT) 数据。 在 NTFS 文件系统中，LAT 数据存储可以是已启用或禁用。 如果已禁用，AgeStore 不会运行，但将改为显示以下错误消息：

```console
Last-Access-Time support is disabled on this computer.
Please read the documentation for more details.
```

在 Windows Vista 和更高版本的 Windows，默认情况下，禁用 LAT 数据存储，并因此 AgeStore 将不运行，除非你先启用此数据。

在 Windows Vista 和更高版本的 Windows 中，您可以使用 FSUtil (Fsutil.exe) 工具来启用 LAT 数据的收集。 从命令提示符窗口中，发出以下命令：

```console
fsutil behavior set disablelastaccess 0 
```

若要禁用收集 LAT 数据，使用以下命令：

```console
fsutil behavior set disablelastaccess 1 
```

这些更改 Windows 在下次重新启动后生效。

FAT32 文件系统始终存储 LAT 信息 （尽管存储仅显示日期，而非时间）。 因此，AgeStore 配合 FAT32 文件系统。 但是，由于 NTFS LAT 处于禁用状态时，不会运行 AgeStore，因此必须启用 NTFS LAT，即使在文件系统是 FAT32。

 

 





