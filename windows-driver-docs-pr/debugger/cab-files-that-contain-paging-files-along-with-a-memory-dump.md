---
title: 包含分页文件以及内存转储的 CAB 文件
description: 内存转储文件可放在 cabinet (CAB) 文件和分页文件。
ms.assetid: 89B54522-1B21-4E4E-9AF3-1F637E3BA50F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a16260eaa2a95de7a60d7374f7ecba009376aaf1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524060"
---
# <a name="cab-files-that-contain-paging-files-along-with-a-memory-dump"></a>包含分页文件以及内存转储的 CAB 文件


内存转储文件可放在 cabinet (CAB) 文件和分页文件。 当 Windows 调试器分析内存转储文件时，它可以使用分页文件提供完整视图内存，包括创建转储文件时换出的内存。

假定一个名为 MyCab.cab 的 CAB 文件包含这些文件：

Memory.dmp Cabmanifest.xml Pagefile.sys 还假设 Cabmanifest.xml 如下所示：

```XML
<?xml version="1.0" encoding="UTF-8"?>
<WatsonPageFileManifest>
  <Pagefiles>
    <Pagefile Name="pagefile.sys"></Pagefile>
  </Pagefiles>
</WatsonPageFileManifest>
```

可以通过输入以下命令之一来打开 CAB 文件：

-   **windbg /z MyCab.cab**
-   **kd /z MyCab.cab**

调试器读取 Cabmanifest.xml 都将包括在调试会话中的分页文件的列表。 在此示例中，没有一个分页文件。 调试器将分页文件转换到的目标信息文件 (TIF) 文件，它可以在调试会话期间使用。 调试器有权访问 TIF，因为它可以显示在创建转储文件的时间已调出的内存。

无论多少分页文件是 CAB 文件中，调试器使用 Cabmanifest.xml 中列出的分页文件。 下面是 CAB 清单文件，其中列出了三个分页文件的示例。

```XML
<?xml version="1.0" encoding="UTF-8"?>
<WatsonPageFileManifest>
  <Pagefiles>
    <Pagefile Name="pagefile1.sys"></Pagefile>
    <Pagefile Name="pagefile2.sys"></Pagefile>
    <Pagefile Name="swapfile.sys"></Pagefile>
  </Pagefiles>
</WatsonPageFileManifest>
```

Cabmanifest.xml，在分页文件必须与 Windows 使用这些相同的顺序列出。 也就是说，它们必须出现在注册表的顺序列出。

CAB 文件中放置的内存转储文件必须是完全内存转储。 可以使用控制面板配置 Windows 崩溃时创建完全内存转储。 例如，在 Windows 8 中你可以转到**Control Panel&gt;系统和安全&gt;系统&gt;高级系统设置&gt;启动和恢复**。 作为使用控制面板的替代方法，可以将此注册表项的值设置为 1。

**HKLM**\\**SYSTEM**\\**CurrentControlSet**\\**Control**\\**CrashControl**\\**CrashDumpEnabled**

从 Windows 8.1，您可以配置 Windows 以在 Windows 重新启动时保留分页文件的内容。

若要指定你想要保存 Windows 重新启动时的分页文件，设置此注册表项的值为 1。

**HKLM**\\**SYSTEM**\\**CurrentControlSet**\\**Control**\\**CrashControl**\\**SavePageFileContents**

 

 





