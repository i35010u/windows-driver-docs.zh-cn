---
title: 使用 PDB 文件显示跟踪日志
description: 使用 PDB 文件显示跟踪日志
keywords:
- 程序数据库符号文件 WDK
- PDB 符号文件 WDK
- 符号文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 945072f34199b5f4a6ce01c805a3e0ad48a20228
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839021"
---
# <a name="displaying-a-trace-log-with-a-pdb-file"></a>使用 PDB 文件显示跟踪日志


## <span id="ddk_using_a_pdb_file_tools"></span><span id="DDK_USING_A_PDB_FILE_TOOLS"></span>


若要显示跟踪日志，您必须告诉 TraceView 如何格式化日志中存储的跟踪消息。 此格式设置信息包含在提供程序的 [PDB 符号文件](pdb-symbol-files.md) 中。

如果有提供程序的 PDB 符号文件，请使用以下过程来显示跟踪日志。 如果你没有 PDB 符号文件，请参阅 [使用 TMF 文件显示跟踪日志](displaying-a-trace-log-with-a-tmf-file.md)。

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  在 " **文件** " 菜单上，单击 " **打开现有日志文件**"。

3.  在 " **日志文件名称** " 框中，键入 ( .etl) 的事件跟踪日志文件的路径和名称。 或者，单击省略号 **按钮 ()** 并导航到该文件。

4.  在 " **日志文件选择** " 对话框中，您还可以设置 "选择选项" 以从日志文件生成其他输出文件。 此步骤是可选的。 有关详细信息，请参阅 [设置跟踪日志选项](setting-trace-log-options.md)。

5.  单击 **“确定”** 。

6.  单击 " **PDB (调试信息") 文件** "，然后键入跟踪提供程序的 [PDB 符号文件](pdb-symbol-files.md) 的路径。 或者，单击省略号 **按钮 ()** 并导航到该文件。

7.  单击 **“确定”** 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

显示日志文件的内容时，"跟踪会话" 列表的 " **状态** " 列中的预期值为 "已 **存在**"。 此值指示跟踪消息来自日志，而不是正在运行的跟踪会话。

 

 





