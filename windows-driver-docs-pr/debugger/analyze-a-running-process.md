---
title: 分析正在运行的进程
description: 使用以下命令以记录并分析正在运行的进程中的堆内存分配。 此分析重点介绍的堆栈跟踪。
ms.assetid: 65a8b510-f5f1-4622-87ff-b44d5855787d
keywords:
- 分析运行过程 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Analyze a Running Process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0abc7873df21e5fa570ddf7395257d21cf141dd3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355001"
---
# <a name="analyze-a-running-process"></a>分析正在运行的进程


使用以下命令以记录并分析正在运行的进程中的堆内存分配。 此分析重点介绍的堆栈跟踪。

```dbgcmd
umdh -p:PID [-f:LogFile] [-v[:MsgFile]] | [-g] | [-h]
```

## <a name="span-idddkanalyzearunningprocessdtoolsspanspan-idddkanalyzearunningprocessdtoolsspanparameters"></a><span id="ddk_analyze_a_running_process_dtools"></span><span id="DDK_ANALYZE_A_RUNNING_PROCESS_DTOOLS"></span>参数


<span id="_______-p_PID______"></span><span id="_______-p_pid______"></span><span id="_______-P_PID______"></span> **-p:**<em>PID</em>   
指定要分析的进程。 *PID*是进程的进程 ID。 此参数是必需的。

若要查找正在运行的进程的 PID，请使用任务管理器中，任务列表，或[TList](tlist.md)。

<span id="_______-f_LogFile______"></span><span id="_______-f_logfile______"></span><span id="_______-F_LOGFILE______"></span> **-f:**<em>LogFile</em>   
将日志内容保存在文本文件中。 默认情况下，UMDH 将日志写入到 stdout （命令窗口）。

*日志文件*指定路径 （可选） 和文件的名称。 如果指定现有的文件，UMDH 将覆盖该文件。

**请注意**  如果 UMDH 不在管理员模式下，还是尝试写入到"受保护"的路径启动的它将被拒绝访问。

 

<span id="_______-v__MsgFile_"></span><span id="_______-v__msgfile_"></span><span id="_______-V__MSGFILE_"></span> **-v\[:**<em>MsgFile</em>**\]**  
详细模式。 生成详细的信息性消息和错误消息。 默认情况下，UMDH 将这些消息写入到 stderr。

*MsgFile*指定路径 （可选） 和文本文件的名称。 当您使用此变量时，UMDH 将详细信息到指定的文件，而不是写入到 stderr。 如果指定现有的文件，UMDH 将覆盖该文件。

<span id="_______-g"></span><span id="_______-G"></span> **-g**  
记录未引用的过程 （"垃圾回收"） 的堆块。

<span id="_______-h"></span><span id="_______-H"></span> **-h**  
显示帮助。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

在 Windows 2000，如果 UMDH 报告错误查找堆栈跟踪数据库，并已启用**创建用户模式堆栈跟踪数据库**选项[GFlags](gflags.md)，则可能存在符号文件冲突。 若要解决它，将复制到同一目录中，应用程序的 DBG 和 PDB 符号文件，然后重试。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```dbgcmd
umdh -?
umdh -p:2230
umdh -p:2230  -f:dump_allocations.txt
umdh -p:2230 -f:c:\Log1.txt -v:c:\Msg1.txt
umdh -p:2230 -g -f:garbage.txt
```

 

 





