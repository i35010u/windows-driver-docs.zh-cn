---
title: 分析正在运行的进程
description: 使用以下命令来记录和分析正在运行的进程中的堆内存分配。 此分析侧重于堆栈跟踪。
keywords:
- 分析正在运行的进程 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Analyze a Running Process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5a76390e7e33bb0f4443ef3d305def98260c056
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783569"
---
# <a name="analyze-a-running-process"></a>分析正在运行的进程


使用以下命令来记录和分析正在运行的进程中的堆内存分配。 此分析侧重于堆栈跟踪。

```dbgcmd
umdh -p:PID [-f:LogFile] [-v[:MsgFile]] | [-g] | [-h]
```

## <a name="span-idddk_analyze_a_running_process_dtoolsspanspan-idddk_analyze_a_running_process_dtoolsspanparameters"></a><span id="ddk_analyze_a_running_process_dtools"></span><span id="DDK_ANALYZE_A_RUNNING_PROCESS_DTOOLS"></span>参数


<span id="_______-p_PID______"></span><span id="_______-p_pid______"></span><span id="_______-P_PID______"></span>**-p：**<em>PID</em>   
指定要分析的进程。 *PID* 是进程的进程 ID。 此参数是必需的。

若要查找正在运行的进程的 PID，请使用任务管理器、Tasklist 或 [tlist.exe](tlist.md)。

<span id="_______-f_LogFile______"></span><span id="_______-f_logfile______"></span><span id="_______-F_LOGFILE______"></span>**-f：**<em>LogFile</em>   
将日志内容保存在文本文件中。 默认情况下，UMDH 会将日志写入 stdout (命令窗口) 。

*LogFile* 指定 (可选的路径) 和文件的名称。 如果指定了现有文件，UMDH 将覆盖该文件。

**注意**   如果 UMDH 未在管理员模式下启动，或者尝试写入 "protected" 路径，则会拒绝访问。

 

<span id="_______-v__MsgFile_"></span><span id="_______-v__msgfile_"></span><span id="_______-V__MSGFILE_"></span>**-v \[ ：**<em>MsgFile</em>**\]**  
详细模式。 生成详细的信息性消息和错误消息。 默认情况下，UMDH 会将这些消息写入 stderr。

*MsgFile* 指定 (可选的路径) 和文本文件的名称。 使用此变量时，UMDH 会将详细消息写入指定的文件，而不是写入 stderr。 如果指定了现有文件，UMDH 将覆盖该文件。

<span id="_______-g"></span><span id="_______-G"></span>**-g**  
记录进程未引用的堆块 ( "垃圾回收" ) 。

<span id="_______-h"></span><span id="_______-H"></span>**-h**  
显示帮助。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

在 Windows 2000 上，如果 UMDH 报告查找堆栈跟踪数据库时出错，并且已在 [GFlags](gflags.md)中启用了 "**创建用户模式堆栈跟踪数据库**" 选项，则可能存在符号文件冲突。 若要解决此问题，请将应用程序的 DBG 和 PDB 符号文件复制到相同的目录，然后重试。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```dbgcmd
umdh -?
umdh -p:2230
umdh -p:2230  -f:dump_allocations.txt
umdh -p:2230 -f:c:\Log1.txt -v:c:\Msg1.txt
umdh -p:2230 -g -f:garbage.txt
```

 

 





