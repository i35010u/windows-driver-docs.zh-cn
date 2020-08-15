---
title: 启用内核模式转储文件
description: 启用内核模式转储文件
ms.assetid: 4faf389f-764e-4439-9e45-fdd53890b0d1
keywords:
- 转储文件，启用内核模式转储文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0521bb1eb67ecec6ccfefba0129af6453b217f3e
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253119"
---
# <a name="enabling-a-kernel-mode-dump-file"></a>启用内核模式转储文件


## <span id="ddk_enabling_a_kernel_mode_dump_file_dbg"></span><span id="DDK_ENABLING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


在系统崩溃期间，Windows 崩溃转储设置确定是否将创建转储文件，如果是，则转储文件的大小。

Windows "控制面板" 控制内核模式故障转储设置。 只有系统管理员可以修改这些设置。

若要更改这些设置，请转到 **"控制面板" " &gt; 系统和安全 &gt; 系统**"。 选择 " **高级系统设置**"。 在 " **启动和恢复**" 下，选择 " **设置**"。

你将看到以下对话框：

!["启动和恢复" 对话框的屏幕截图](images/crashpanel.png)

在 " **写入调试信息**" 下，可以指定内核模式转储文件设置。 对于任何给定的崩溃，只能创建一个转储文件。 有关不同转储文件设置的描述，请参阅 [各种内核模式转储文件](varieties-of-kernel-mode-dump-files.md) 。

还可以选择或取消选择 "将 **事件写入系统日志** 并 **自动重新启动** " 选项。

你选择的设置将应用于系统崩溃创建的任何内核模式转储文件，无论系统崩溃是意外发生还是由调试器引起的，都是如此。 有关导致故意崩溃的详细信息，请参阅 [强制系统崩溃](forcing-a-system-crash.md) 。

但是，这些设置不会影响 [**dump 命令所创建的转储文件**](-dump--create-dump-file-.md) 。 有关使用此命令的详细信息，请参阅 [不使用系统崩溃创建转储文件](creating-a-dump-file-without-a-system-crash.md) 。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式转储文件](kernel-mode-dump-files.md)

[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)

 

 






