---
title: 包含页面文件和内存转储的 CAB 文件
description: 内存转储文件可以与页面文件一起放置在 cabinet (CAB) 文件中。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f751cecfff77889d036cd77c9f62d3a74c34996e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828263"
---
# <a name="cab-files-that-contain-paging-files-along-with-a-memory-dump"></a>包含页面文件和内存转储的 CAB 文件


内存转储文件可以与页面文件一起放置在 cabinet (CAB) 文件中。 当 Windows 调试器分析内存转储文件时，它可以使用页面文件来显示完整的查看内存，包括创建转储文件后已分页的内存。

假设有一个名为 MyCab.cab 的 CAB 文件包含以下文件：

内存 dmp Cabmanifest.xml Pagefile.sys 也假设 Cabmanifest.xml 如下所示：

```XML
<?xml version="1.0" encoding="UTF-8"?>
<WatsonPageFileManifest>
  <Pagefiles>
    <Pagefile Name="pagefile.sys"></Pagefile>
  </Pagefiles>
</WatsonPageFileManifest>
```

可以通过输入以下命令之一来打开 CAB 文件：

-   **windbg/z MyCab.cab**
-   **kd/z MyCab.cab**

调试器读取 Cabmanifest.xml，获取要包含在调试会话中的分页文件的列表。 在此示例中，只有一个页面文件。 调试器会将页面文件转换为可在调试会话期间使用的 (.TIF) 文件的目标信息文件。 由于调试器有权访问 TIF，因此它可以显示创建转储文件时已分页的内存。

无论 CAB 文件中有多少个页面文件，调试器都只使用 Cabmanifest.xml 中列出的页面文件。 下面是列出三个页面文件的 CAB 清单文件的示例。

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

在 Cabmanifest.xml 中，必须按照 Windows 使用的相同顺序列出页面文件。 也就是说，它们必须按它们在注册表中出现的顺序列出。

放入 CAB 文件中的内存转储文件必须是完整内存转储。 可以使用 "控制面板" 将 Windows 配置为在发生崩溃时创建完整的内存转储。 例如，在 Windows 8 中，您可以切换到 **"控制面板" " &gt; 系统和安全系统" " &gt; &gt; 高级系统设置" " &gt; 启动和恢复**"。 作为使用 "控制面板" 的替代方法，可以将此注册表项的值设置为1。

**HKLM** \\**系统** \\**CurrentControlSet** \\**控件** \\**CrashControl** \\**CrashDumpEnabled**

从 Windows 8.1 开始，你可以将 Windows 配置为在 Windows 重新启动时保留页面文件的内容。

若要指定在 Windows 重新启动时要保存页面文件，请将此注册表项的值设置为1。

**HKLM** \\**系统** \\**CurrentControlSet** \\**控件** \\**CrashControl** \\**SavePageFileContents**

 

 





