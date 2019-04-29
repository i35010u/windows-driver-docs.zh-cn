---
title: 使用 PDB 文件创建跟踪会话
description: 使用 PDB 文件创建跟踪会话
ms.assetid: dae78674-3563-4fd5-869b-abd4c13aa202
keywords:
- 程序数据库符号文件 WDK
- WDK 的 PDB 符号文件
- 符号文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d08ac7b33e8fcc72ee185f9ff7ad9d96e40d481
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381012"
---
# <a name="creating-a-trace-session-with-a-pdb-file"></a>使用 PDB 文件创建跟踪会话


## <span id="ddk_create_a_trace_session_with_a_pdb_file_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_WITH_A_PDB_FILE_TOOLS"></span>


指定跟踪提供程序的最简单方法是查找[PDB 符号文件](pdb-symbol-files.md)包括跟踪提供程序的源代码。 TraceView 可以提取所有 PDB 文件中需要用于跟踪会话的信息。

### <a name="span-idtocreateatracesessionwithapdbfilespanspan-idtocreateatracesessionwithapdbfilespanto-create-a-trace-session-with-a-pdb-file"></a><span id="to_create_a_trace_session_with_a_pdb_file"></span><span id="TO_CREATE_A_TRACE_SESSION_WITH_A_PDB_FILE"></span>若要使用的 PDB 文件创建跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  上**文件**菜单上，单击**新建日志会话**。

3.  单击**添加提供程序**。

4.  单击**PDB （调试信息） 文件**，然后键入的路径[PDB 符号文件](pdb-symbol-files.md)跟踪提供程序; 或单击省略号按钮 (**...**) 并导航到该文件。

5.  若要添加其他提供程序，请单击**添加提供程序**。 此步骤可选。

6.  单击“下一步” 。

7.  [选择标志和级别](selecting-flags-and-levels.md)，如果所需的。

8.  [设置会话选项的基本跟踪](setting-basic-trace-session-options.md)，如果所需的。

9.  [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)，如果所需的。

10. 单击 **“完成”**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果您指定的 PDB 文件不包括所需的跟踪元素，TraceView 将显示"找不到 PDB 文件"错误消息。

如果您使用 TraceView 打开 PDB 文件运行 Windows Server 2003 的计算机上，TraceView 将自动退出。

 





