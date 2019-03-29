---
title: 调试-使用跟踪文件按时间顺序查看
description: 本部分介绍如何处理时间旅行跟踪文件
ms.date: 09/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c609e8104f15f0a2561af667e878ba1f0e3244e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568129"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png) 

# <a name="time-travel-debugging---working-with-trace-files"></a>调试-使用跟踪文件按时间顺序查看

本部分介绍如何使用创建和使用的时间旅行调试文件。

## <a name="trace-file-overview"></a>跟踪文件概述

时间旅行调试使用以下文件来调试代码执行。

- 包含代码执行记录，但不在跟踪文件。运行扩展。

- 索引文件可以快速访问信息的跟踪文件中并且具有。IDX 扩展。

- 记录错误和其他记录输出写入调试器日志文件。


## <a name="trace-run-files"></a>将跟踪中。运行文件  

将跟踪中。在记录使用后，可以打开运行的文件**文件** > **开始调试** > **打开跟踪文件**。

![文件打开选项显示突出显示打开的跟踪选项](images/ttd-start-debugging-options.png) 

所有跟踪输出文件默认存储在用户文档文件夹中。 例如，为 User1 TTD 文件将存储在此处：

```console
C:\Users\User1\Documents
```
当你开始记录，可以更改跟踪文件的位置。 有关详细信息，请参阅[调试-记录按时间顺序查看](time-travel-debugging-record.md)。

最近使用过的文件列表，可以快速访问以前使用过目标配置文件。 最近使用的任何跟踪文件或转储文件也将列出。 

![文件打开列出的.run 跟踪文件显示 5 个最近使用的跟踪文件](images/ttd-recent-trace-files.png) 


## <a name="index-idx-files"></a>索引。IDX 文件  

一种索引。有关关联跟踪创建 IDX 文件。在 WinDbg 预览中打开跟踪文件时自动运行文件。 您可以通过使用手动创建的索引文件 ！ 索引命令。 索引可以更快地访问跟踪信息。 

IDX 文件也可能很大，通常两次的大小。运行文件。  

## <a name="recreating-the-idx-file"></a>重新创建。IDX 文件
你可以重新创建。从 IDX 文件。运行文件，请使用`!index`命令。 有关详细信息，请参阅[调试旅行时间-！ 索引 （时程）](time-travel-debugging-extension-index.md)。

```dbgcmd
0:0:001> !index
Indexed 3/3 keyframes
Successfully created the index in 49ms.
```

## <a name="sharing-ttd-trace-run-files"></a>共享 TTD 跟踪。运行文件

可以通过复制与他人共享 TTD 跟踪文件。运行文件。 这可以非常方便地让同事帮助找出问题。 它们无需安装故障的应用程序或执行任何其他相关安装程序以尝试重现此问题。 它们只是可以加载跟踪文件，并像它已安装在其电脑上调试应用程序。 

您可以重命名文件以包括任何其他信息，例如日期或 bug 数量。

。IDX 文件不需要复制，因为它可以重新创建使用 ！ 索引命令，如上文所述。


> [!TIP]
> 当与其他人协作，将传递在与手头的问题相关的任何相关的跟踪位置上。 协作者可以使用`!tt x:y`命令中的代码的执行时间，将移动到的确切点。 时间位置范围可以包含在 bug 说明来跟踪可能会发生可能存在问题的位置。
>


## <a name="error---log-file"></a>错误-日志文件

记录错误和其他记录输出写入调试器日志文件。 若要查看日志文件，请选择**视图** > **日志**。 

此示例显示错误日志文本时尝试启动并记录名为 Foo.exe C:\Windows 目录中不是一个可执行文件。

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


## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---






