---
title: 自动内存转储
description: 自动内存转储
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19586e2d0dbfea297b7be5edc2f5e1565c3ff2fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819295"
---
# <a name="automatic-memory-dump"></a>自动内存转储


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


*自动内存转储* 包含与 [内核内存转储](kernel-memory-dump.md)相同的信息。 这两者之间的差异不是转储文件本身，而是 Windows 设置系统分页文件大小的方式。

如果系统分页文件大小设置为 **系统管理的大小**，并且内核模式故障转储设置为 **自动内存转储**，则 Windows 可以将页面文件的大小设置为小于 RAM 大小。 在这种情况下，Windows 会设置足够大的页面文件大小，以确保大多数时间都可以捕获内核内存转储。

如果计算机崩溃且页面文件不够大，无法捕获内核内存转储，Windows 会将页面文件的大小增加到至少大小的 RAM。 此事件的时间记录在注册表中：

**HKLM** \\**系统** \\**CurrentControlSet** \\**控件** \\**CrashControl** \\**LastCrashTime**

增加的分页文件大小将保留4周，然后返回到较小的大小。 如果要在4周之前返回到较小的页面文件，可以删除注册表项。

若要查看页面文件设置，请参阅 **"控制面板 &gt; 系统和安全 &gt; 系统 &gt; 高级系统设置**"。 在 " **性能**" 下，选择 " **设置**"。 在 " **高级** " 选项卡上的 " **虚拟内存**" 下，选择 " **更改**"。 在 "虚拟内存" 对话框中，可以看到页面文件设置。

!["虚拟内存" 对话框的屏幕截图。](images/virtualmemorydialog.png)

默认情况下，自动内存转储文件写入% SystemRoot% \\ Memory。

Windows 8 及更高版本中提供自动内存转储。

**注意**  若要在调试自动内存转储时取消丢失页错误消息，请使用 " [**忽略 \_ 缺少的 \_ 页**](-ignore-missing-pages--suppress-missing-page-errors-.md) " 命令。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)

[内核模式转储文件](kernel-mode-dump-files.md)

[创建内核模式转储文件](creating-a-kernel-mode-dump-file.md)

 

 






