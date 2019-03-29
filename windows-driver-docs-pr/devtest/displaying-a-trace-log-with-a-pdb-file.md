---
title: 使用 PDB 文件显示跟踪日志
description: 使用 PDB 文件显示跟踪日志
ms.assetid: 267a5d34-6fd0-43b6-aa07-5154bdb2b9a7
keywords:
- 程序数据库符号文件 WDK
- WDK 的 PDB 符号文件
- 符号文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dc70de6eefd456a9c04fb313d5bba7e1057834e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567171"
---
# <a name="displaying-a-trace-log-with-a-pdb-file"></a>使用 PDB 文件显示跟踪日志


## <span id="ddk_using_a_pdb_file_tools"></span><span id="DDK_USING_A_PDB_FILE_TOOLS"></span>


若要显示的跟踪日志，您必须告诉 TraceView 如何设置存储在日志中的跟踪消息的格式。 此格式设置信息包含在[PDB 符号文件](pdb-symbol-files.md)提供程序。

如果你有提供程序的 PDB 符号文件，使用以下过程显示跟踪日志。 如果还没有 PDB 符号文件，请参阅[显示与 TMF 文件跟踪日志](displaying-a-trace-log-with-a-tmf-file.md)。

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  上**文件**菜单上，单击**打开现有日志文件**。

3.  在中**日志文件名称**框中，键入路径和事件跟踪日志文件 (.etl) 的名称。 或者，单击省略号按钮 (**...**) 并导航到该文件。

4.  在中**日志文件选择**对话框中，您还可以设置选择选项，以生成其他输出日志文件中的文件。 此步骤可选。 有关详细信息，请参阅[设置跟踪日志选项](setting-trace-log-options.md)...

5.  单击 **“确定”**。

6.  单击**PDB （调试信息） 文件**并键入的路径[PDB 符号文件](pdb-symbol-files.md)跟踪提供程序。 或者，单击省略号按钮 (**...**) 并导航到该文件。

7.  单击 **“确定”**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

当显示日志的内容文件中的期望值**状态**跟踪会话列表的列是**现有**。 跟踪消息来自一个日志，此值指示没有正在运行的跟踪会话。

 

 





