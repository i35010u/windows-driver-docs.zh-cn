---
title: 使用 PDB 文件创建跟踪会话
description: 使用 PDB 文件创建跟踪会话
keywords:
- 程序数据库符号文件 WDK
- PDB 符号文件 WDK
- 符号文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecc9a764755d31035865140877b888aa1155d1e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792367"
---
# <a name="creating-a-trace-session-with-a-pdb-file"></a>使用 PDB 文件创建跟踪会话


## <span id="ddk_create_a_trace_session_with_a_pdb_file_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_WITH_A_PDB_FILE_TOOLS"></span>


指定跟踪提供程序的最简单方法是为包含跟踪提供程序的源代码查找 [PDB 符号文件](pdb-symbol-files.md) 。 TraceView 可以从 PDB 文件中提取跟踪会话所需的所有信息。

### <a name="span-idto_create_a_trace_session_with_a_pdb_filespanspan-idto_create_a_trace_session_with_a_pdb_filespanto-create-a-trace-session-with-a-pdb-file"></a><span id="to_create_a_trace_session_with_a_pdb_file"></span><span id="TO_CREATE_A_TRACE_SESSION_WITH_A_PDB_FILE"></span>使用 PDB 文件创建跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

3.  单击 **“添加提供程序”**。

4.  单击 " **PDB (调试信息") 文件**"，然后键入跟踪提供程序的 [PDB 符号文件](pdb-symbol-files.md) 的路径;或者，单击省略号 **按钮 ()** 并导航到该文件。

5.  若要添加其他提供程序，请单击 " **添加提供程序**"。 此步骤是可选的。

6.  单击 **“下一步”** 。

7.  如果需要，请[选择 "标志" 和 "级别](selecting-flags-and-levels.md)"。

8.  如果需要，请[设置基本跟踪会话选项](setting-basic-trace-session-options.md)。

9.  如果需要，请[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

10. 单击“完成”。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

如果指定的 PDB 文件不包括所需的跟踪元素，TraceView 将显示 "找不到 PDB 文件" 错误消息。

如果使用 TraceView 在运行 Windows Server 2003 的计算机上打开 PDB 文件，则 TraceView 会自动退出。

 





