---
title: 时间行程调试-使用跟踪文件
description: 本部分介绍如何使用时间行程跟踪文件
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: b420779acb6d56dc4cf28df77206f5a0c980875b
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802699"
---
# <a name="time-travel-debugging---working-with-trace-files"></a>时间行程调试-使用跟踪文件

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png) 

本部分介绍如何使用时间段调试创建和使用的文件。

## <a name="trace-file-overview"></a>跟踪文件概述

行程调试使用以下文件来调试代码执行。

- 跟踪文件包含代码执行记录，并具有。运行扩展。

- 索引文件允许快速访问跟踪文件中的信息，并具有。IDX 扩展。

- 记录错误和其他记录输出会写入调试器日志文件。


## <a name="trace-run-files"></a>轨迹.运行文件  

轨迹.使用**文件**  >  **启动调试**  >  **打开跟踪文件**来记录运行文件后，可以打开这些文件。

![突出显示打开跟踪选项的文件打开选项](images/ttd-start-debugging-options.png) 

默认情况下，所有跟踪输出文件都存储在用户文档文件夹中。 例如，对于 User1，将在此处存储 TTD 文件：

```console
C:\Users\User1\Documents
```
您可以在开始记录时更改跟踪文件的位置。 有关详细信息，请参阅 [行程调试-记录](time-travel-debugging-record.md)。

使用最近使用过的文件列表，可以快速访问以前使用过的目标配置文件。 还列出了所有最近使用过的跟踪文件或转储文件。

![文件打开列表。运行跟踪文件，显示最近使用过的跟踪文件](images/ttd-recent-trace-files.png) 

## <a name="index-idx-files"></a>编入.IDX 文件  

索引。将为关联的跟踪创建 IDX 文件。在 WinDbg Preview 中打开跟踪文件时自动运行文件。 您可以使用！ index 命令手动创建索引文件。 索引允许更快地访问跟踪信息。 

IDX 文件也可以是大，通常是大小的两倍。运行文件。  

## <a name="recreating-the-idx-file"></a>重新创建。IDX 文件
您可以重新创建。的 IDX 文件。使用命令运行文件 `!index` 。 有关详细信息，请参阅 [行程调试-！索引 (时间) ](time-travel-debugging-extension-index.md)。

```dbgcmd
0:0:001> !index
Indexed 3/3 keyframes
Successfully created the index in 49ms.
```

## <a name="sharing-ttd-trace-run-files"></a>共享 TTD 跟踪。运行文件

TTD 是仅本地的，不能远程连接到另一台计算机。

可以通过复制将 TTD 跟踪文件与其他用户共享。运行文件。 这样一来，就可以轻松地让同事帮助您找出问题。 它们不需要安装崩溃应用程序，也不需要执行任何其他相关的设置来尝试重现该问题。 它们只需加载跟踪文件并调试应用程序，就像它已安装在自己的 PC 上一样。

重播 TTD 跟踪的计算机必须支持在记录计算机上使用的所有说明，例如 AVX 指令。

您可以重命名该文件以包含任何其他信息，例如日期或 bug 号。

此.不需要复制 IDX 文件，因为可以使用以上所述的！ index 命令重新创建它。

> [!TIP]
> 与他人进行协作时，请传递与现有问题相关的任何相关跟踪位置。 协作者可以使用 `!tt x:y` 命令移动到执行代码的确切时间点。 时间位置范围可以包含在 bug 描述中，以跟踪可能出现问题的位置。
>

## <a name="error---log-file"></a>错误-日志文件

记录错误和其他记录输出会写入调试器日志文件。 若要查看日志文件，请选择 "**查看**  >  **日志**"。 

此示例将在尝试启动并记录不在 C：\Windows 目录中的名为 Foo.exe 的可执行文件时显示错误日志文本。

```console
2017-09-21:17:18:10:320 : Information : DbgXUI.dll : TTD: Output: 
Microsoft (R) TTD 1.01.02
Release: 10.0.16366.1000
Copyright (C) Microsoft Corporation. All rights reserved.
Launching C:\Windows\Foo.exe
2017-09-21:17:18:10:320 : Error : DbgXUI.dll : TTD: Errors: 
Error: Trace of C:\Windows\Foo.exe PID:0 did not complete successfully: status:27
Error: Could not open 'Foo.exe'; file not found.
Error: Corrupted trace dumped to C:\Users\User1\Documents\Foo01.run.err.
```

## <a name="trace-file-size"></a>跟踪文件大小

TTD 跟踪文件可能非常大，因此请务必确保有足够的可用磁盘空间。  如果只记录了几分钟的应用或过程，则跟踪文件可能会增长到几 gb。  跟踪文件的大小取决于下面所述的许多因素。  

TTD 不会将跟踪文件的最大大小设置为允许复杂长时间运行的方案。 快速重新创建问题，会使跟踪文件的大小尽可能小。

### <a name="trace-file-size-factors"></a>跟踪文件大小因素

不能提供跟踪文件大小的确切估计值，但有几个经验法则可帮助你了解 TTD 文件大小。

以下因素可能会影响跟踪文件的大小：

- 记录正在运行的应用程序或进程时在所有线程上执行的代码指令的数目
- 记录应用或进程的时间长度 (仅因为这会影响记录的代码指令数) 
- 应用或进程使用的内存数据的大小

执行和记录的指令数是影响跟踪文件大小的最大因素。  跟踪通常需要在每个指令执行1个位和1个字节之间。  当记录的程序执行少量的不同函数并对一组较小的数据进行操作时，跟踪可能会接近该范围的下限。  当记录的程序执行大量不同的函数或对较大的一组数据进行操作时，跟踪可能会接近该范围的更高。

### <a name="trace-file-size-rule-of-thumb"></a>跟踪文件大小经验的规则

记录活动的应用程序或进程时，跟踪文件大约每秒增长5MB 到50MB，具体取决于上面确定的跟踪文件大小因素。

如果正在记录的应用程序或进程处于空闲状态 (例如等待输入) 时，跟踪文件将不会增长。

当前没有跟踪文件的最大文件大小限制。  WinDbg Preview 可以重播大小很大的文件。

### <a name="index-file-size"></a>索引文件大小

首次打开跟踪时，WinDbg Preview 会自动创建索引文件。  它包含有助于调试器更有效地重播跟踪和查询内存信息的信息。  其大小通常介于跟踪文件大小的1到2倍之间。  影响其大小的因素类似于影响跟踪文件大小的因素。

首先，索引文件的大小相对于跟踪的长度进行缩放。  包含较多记录指令的跟踪通常具有较大的索引。

其次，索引相对于内存访问范围的大小进行缩放。  如果经常访问的程序是大量不同的内存位置，则索引通常会大于以下情况：如果记录的程序访问的是不同的内存位置，或者如果访问内存位置不太频繁。

由于这些因素与影响跟踪文件大小的因素相似，因此，索引文件的大小通常会相对于索引 (文件的大小进行缩放，因此，我们的估计值通常介于1x 到) 的跟踪文件大小的2倍之间。

### <a name="what-if-i-run-out-of-disk-space"></a>如果磁盘空间不足，该怎么办？

TTD 跟踪和索引文件都写入磁盘。 当前跟踪或索引文件没有最大文件大小限制。 跟踪文件的大小会增加，直到停止记录或超出可用磁盘空间量。

*录制期间：* TTD 会将最后一页写出到跟踪文件，然后有效地等待，直到它再次被写入。 WinDbg 会继续显示录制对话框，但在记录过程中磁盘空间不足时不会显示错误/警告消息。  

在记录过程中磁盘空间不足将导致跟踪文件中包含代码执行的不完整记录。 不完整的跟踪文件可以在 WinDbg Preview 中打开，但如果在写入跟踪文件时磁盘空间不足后发生错误，则可能不包括实际问题。

解决方法：打开文件资源管理器并检查磁盘 (（即 C：驱动器) 可用空间是否接近零。 或者， ( 观看跟踪。在文件资源管理器中运行) 文件 (默认情况下在 "文档" 文件夹中) 如果没有定期增长，则记录可能正在等待。 选择 WinDbg 中的 "停止" 和 "调试" 按钮，释放空间或保存到其他磁盘，然后重新开始记录。

*在索引期间：* 调试器可能会生成无效的索引文件，导致调试器中出现不可预知的行为，否则调试器引擎主机可能会崩溃。

解决方法：关闭调试器并删除 ( 的索引文件。 idx) 跟踪可能存在。  释放足够的磁盘空间，或将跟踪文件移动到具有足够可用空间的其他磁盘上。  在调试器中再次打开跟踪，然后运行！ index，以创建一个新的、正确的索引。  索引编制不会修改原始跟踪文件 (。运行) ，因此不会丢失任何数据。

## <a name="see-also"></a>另请参阅

[时光穿越调试 - 概述](time-travel-debugging-overview.md)
