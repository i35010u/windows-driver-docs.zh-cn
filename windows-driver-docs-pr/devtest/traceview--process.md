---
title: TraceView -process
description: 使用 TraceView 命令可以在跟踪日志中或通过实时跟踪 seesion 格式化二进制跟踪消息。 TraceView 命令创建跟踪消息的文本文件和描述输入文件和输出文件的摘要文件。
keywords:
- TraceView-进程驱动程序开发工具
topic_type:
- apiref
api_name:
- TraceView -process
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 422fa1297de59913b7272dfd34955824dbd8fbd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838109"
---
# <a name="traceview--process"></a>TraceView -process


使用 **TraceView** 命令可以在 [跟踪日志](trace-log.md) 中或通过实时跟踪 seesion 格式化二进制跟踪消息。 **TraceView** 命令创建跟踪消息的文本文件和描述输入文件和输出文件的摘要文件。

```
    traceview -process [EtlFile | -rt SessionName][Parameters]
   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______EtlFile______"></span><span id="_______etlfile______"></span><span id="_______ETLFILE______"></span>*EtlFile*   
指定包含跟踪消息 ( .etl) 文件的事件跟踪日志。 输入路径 (可选) 和文件名。 默认值为 c： \\ logfile。

<span id="_______-rt_______SessionName______"></span><span id="_______-rt_______sessionname______"></span><span id="_______-RT_______SESSIONNAME______"></span>**-rt** *SessionName*   
实时。 设置来自指定实时跟踪会话的跟踪消息的格式。

*SessionName* 是跟踪会话的名称。 如果省略跟踪会话名称，Tracefmt 会从 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)中格式化消息。

<span id="_______-tmf_______TMFFile______"></span><span id="_______-tmf_______tmffile______"></span><span id="_______-TMF_______TMFFILE______"></span>**-tmf** *TMFFile*   
为跟踪消息指定 [跟踪消息格式 ( tmf) 文件](trace-message-format-file.md) 的路径 (可选的) 和文件名。

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span>**-p** *TMFPath*   
为跟踪消息指定包含 [跟踪消息格式 () 文件](trace-message-format-file.md) 的目录的路径。

<span id="_______-o_______OutputFile______"></span><span id="_______-o_______outputfile______"></span><span id="_______-O_______OUTPUTFILE______"></span>**-o** *OutputFile*   
指定输出文件的名称。 此名称应用于格式化跟踪消息的文本文件和摘要文件。

*OutputFile* 是具有 .txt 文件扩展名的路径和文件名，如 c： \\ 跟踪 \\trace.txt。 默认值为 FmfFile.txt，并 FmtSum.txt 在本地目录中。

如果将此参数与 **-displayonly** 或 **-summaryonly** 参数一起使用，则它只会影响摘要文件。

<span id="_______-csv______"></span><span id="_______-CSV______"></span>**-csv**   
将跟踪日志的格式设置为逗号分隔的可变长度 ( .csv) 文件。

<span id="_______-display______"></span><span id="_______-DISPLAY______"></span>**-display**   
除了将跟踪消息写入到输出文件，还在命令提示符窗口中显示这些跟踪消息。

<span id="_______-displayonly______"></span><span id="_______-DISPLAYONLY______"></span>**-displayonly**   
仅在命令提示符窗口中显示跟踪消息。 TraceView 不会创建跟踪消息的文本文件。

<span id="_______-nosummary______"></span><span id="_______-NOSUMMARY______"></span>**-nosummary**   
不创建 [摘要消息文件](summary-message-file.md)。

<span id="_______-summaryonly______"></span><span id="_______-SUMMARYONLY______"></span>**-summaryonly**   
仅创建 [摘要消息文件](summary-message-file.md)。 Tracefmt 不会创建 [输出文件](tracefmt-output-file.md)。

<span id="_______-noprefix______"></span><span id="_______-NOPREFIX______"></span>**-noprefix**   
省略 [跟踪消息前缀](trace-message-prefix.md)。 此参数影响输出文件和 Tracefmt 显示中的跟踪消息。

<span id="_______-ods______"></span><span id="_______-ODS______"></span>**-ods**   
将格式化跟踪消息发送到调试器以显示。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
“详细”： 在 "命令提示符" 窗口中显示详细信息，因为 Tracefmt 处理跟踪消息的每个块或缓冲区。 如果怀疑文件损坏或不一致，请使用此参数。

<span id="_______-h_____"></span><span id="_______-H_____"></span>**-h**  | **/?**  
显示帮助。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

```
traceview -process
traceview -process mytrace.etl -p c:\tracing -o mytrace.txt
traceview mytrace.etl -tmf c:\tracing\37753236-c81f-505e-d40a-128d3bb2b5ff.tmf
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt -display
```

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

若要设置跟踪消息的格式，必须为跟踪消息指定跟踪消息格式文件。 可用的方法按优先级顺序列出：

-   **-Tmf** 参数。

-   **-P** 参数。

-   % TRACE \_ 格式 \_ 搜索 \_ 路径% 环境变量。 将变量的值设置为 TMF 文件所在的目录。

如果 TMF 文件名不是 [消息 GUID](message-guid.md)，请使用 **-TMF** 参数，并输入文件的完全限定路径。 否则，TraceView 将找不到 TMF 文件。

如果 TraceView 找不到 TMF 文件，或 TMF 文件未包含跟踪消息的格式设置信息，则 TraceView 无法设置消息格式。 相反，TraceView 写入消息文本： "未找到格式信息"。

如果 TraceView 无法格式化跟踪消息，则会引发异常并显示一条消息，如下所示：

```
*****FormatMessage Header(Header) of EventTrace, parameter 23 raised an exception*****
```
