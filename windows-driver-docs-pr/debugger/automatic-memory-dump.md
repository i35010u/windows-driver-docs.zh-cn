---
title: 自动内存转储
description: 自动内存转储
ms.assetid: A2C71497-7865-4DC8-B760-6121B224737A
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae6b84d1c38f32e048c752f2a92d9dc1dbc31109
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354410"
---
# <a name="automatic-memory-dump"></a>自动内存转储


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


*自动内存转储*包含相同的信息[内核内存转储](kernel-memory-dump.md)。 两者之间的差异是不在转储文件本身，而 Windows 设置的系统分页文件大小的方式。

如果系统分页文件大小设置为**系统管理的大小**，和内核模式崩溃转储设置为**自动内存转储**，则 Windows 可以将页面文件的大小设置为小于 RAM 大小。 在这种情况下，Windows 设置足够大，保证内核内存转储可捕获大多数情况下页面文件的大小。

如果计算机崩溃和分页文件不是足够大，以捕获内核内存转储，Windows 会增加的大小的分页文件为至少 RAM 的大小。 在注册表中此处记录此事件的时间：

**HKLM**\\**SYSTEM**\\**CurrentControlSet**\\**Control**\\**CrashControl**\\**LastCrashTime**

增加的页面文件的大小保持在位置 4 周，然后返回到较小的大小。 如果你想要返回到较小的分页文件前 4 周，可以删除注册表项。

若要查看分页文件设置，请转到**Control Panel&gt;系统和安全&gt;系统&gt;高级系统设置**。 在“性能”下，单击“设置”。 上**高级**选项卡上，在**虚拟内存**，单击**更改**。 在虚拟内存对话框中，可以看到的页面文件设置。

![虚拟内存对话框的屏幕截图。](images/virtualmemorydialog.png)

自动内存转储文件写入到 %systemroot%\\Memory.dmp 默认情况下。

自动内存转储是推出 Windows 8 及更高版本。

**请注意**  若要自动的内存转储调试时，禁止显示缺失的页错误消息，请使用[ **.ignore\_缺少\_页**](-ignore-missing-pages--suppress-missing-page-errors-.md)命令。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[类型的内核模式转储文件](varieties-of-kernel-mode-dump-files.md)

[内核模式转储文件](kernel-mode-dump-files.md)

[正在创建内核模式转储文件](creating-a-kernel-mode-dump-file.md)

 

 






