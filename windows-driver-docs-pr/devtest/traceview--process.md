---
title: TraceView -process
description: 使用 TraceView-处理命令以设置在跟踪日志中或从实时跟踪 seesion 的二进制跟踪消息的格式。 TraceView-处理命令创建文本文件的跟踪消息和摘要文件，用于描述输入和输出文件。
ms.assetid: a0da5004-7a9f-4229-92c1-6264fcbf9b0d
keywords:
- TraceView-处理驱动程序开发工具
topic_type:
- apiref
api_name:
- TraceView -process
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57d39635eb39d4dbe05ac74f01e1cbd127e439ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369612"
---
# <a name="traceview--process"></a>TraceView -process


使用**TraceView-进程**命令来设置格式的二进制跟踪中的消息[跟踪日志](trace-log.md)或从实时跟踪 seesion。 **TraceView-进程**命令会创建文本文件的跟踪消息和摘要文件，用于描述输入和输出文件。

```
    traceview -process [EtlFile | -rt SessionName][Parameters]
   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="_______EtlFile______"></span><span id="_______etlfile______"></span><span id="_______ETLFILE______"></span> *EtlFile*   
指定包含跟踪消息事件跟踪日志 (.etl) 文件。 输入的路径 （可选） 和文件名称。 默认值为 c:\\logfile.etl。

<span id="_______-rt_______SessionName______"></span><span id="_______-rt_______sessionname______"></span><span id="_______-RT_______SESSIONNAME______"></span> **-rt** *SessionName*   
实际时间。 格式跟踪来自指定的实时跟踪会话的消息。

*会话名*跟踪会话的名称。 如果省略跟踪会话名称，Tracefmt 格式从消息[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

<span id="_______-tmf_______TMFFile______"></span><span id="_______-tmf_______tmffile______"></span><span id="_______-TMF_______TMFFILE______"></span> **-tmf** *TMFFile*   
指定的路径 （可选） 和文件名称[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)的跟踪消息。

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span> **-p** *TMFPath*   
指定包含的目录的路径[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)的跟踪消息。

<span id="_______-o_______OutputFile______"></span><span id="_______-o_______outputfile______"></span><span id="_______-O_______OUTPUTFILE______"></span> **-o** *OutputFile*   
指定输出文件的名称。 此名称适用于文本文件的格式化的跟踪消息和摘要文件。

*OutputFile*是与.txt 文件扩展名，例如 c: 路径和文件名\\跟踪\\trace.txt。 默认值为 FmfFile.txt 和 FmtSum.txt 本地目录中。

如果使用此参数与 **-displayonly**或 **-summaryonly**参数，它会影响仅摘要文件。

<span id="_______-csv______"></span><span id="_______-CSV______"></span> **-csv**   
格式设置为一个以逗号分隔、 可变长度 (.csv) 文件跟踪日志。

<span id="_______-display______"></span><span id="_______-DISPLAY______"></span> **-display**   
在命令提示符窗口中，除了写入到输出文件中显示的跟踪消息。

<span id="_______-displayonly______"></span><span id="_______-DISPLAYONLY______"></span> **-displayonly**   
仅在命令提示符窗口中显示的跟踪消息。 TraceView 不会创建跟踪消息的文本文件。

<span id="_______-nosummary______"></span><span id="_______-NOSUMMARY______"></span> **-nosummary**   
不会创建[条摘要消息文件](summary-message-file.md)。

<span id="_______-summaryonly______"></span><span id="_______-SUMMARYONLY______"></span> **-summaryonly**   
创建仅[条摘要消息文件](summary-message-file.md)。 不会创建 Tracefmt[输出文件](tracefmt-output-file.md)。

<span id="_______-noprefix______"></span><span id="_______-NOPREFIX______"></span> **-noprefix**   
省略[跟踪消息前缀](trace-message-prefix.md)。 此参数会影响输出文件和 Tracefmt 显示中的跟踪消息。

<span id="_______-ods______"></span><span id="_______-ODS______"></span> **-ods**   
将格式化的跟踪消息发送到调试程序，以便显示。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
详细。 显示的详细信息命令提示符窗口中的 Tracefmt 处理每个块或跟踪消息的缓冲区。 如果您担心发生文件损坏或不一致，请使用此参数。

<span id="_______-h_____"></span><span id="_______-H_____"></span> **-h** | **/?**  
显示帮助。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

```
traceview -process
traceview -process mytrace.etl -p c:\tracing -o mytrace.txt
traceview mytrace.etl -tmf c:\tracing\37753236-c81f-505e-d40a-128d3bb2b5ff.tmf
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt -display
```

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

若要格式化跟踪消息，必须指定跟踪消息的跟踪消息格式文件。 按优先级顺序列出可用的方法：

-   **-Tmf**参数。

-   **-P**参数。

-   %跟踪\_格式\_搜索\_PATH %环境变量。 将变量的值设置为 TMF 文件所在的目录。

如果 TMF 文件名称不是[消息 GUID](message-guid.md)，使用 **-tmf**参数和输入文件的完全限定的路径。 否则，TraceView 将找到 TMF 文件。

如果 TraceView 找不到 TMF 文件，或者 TMF 文件不包含格式化跟踪消息的信息，TraceView 无法格式化消息。 相反，消息文本，代替 TraceView 写入："未找到格式信息。"

如果 TraceView 不能设置格式的跟踪消息，它会引发异常并显示一条消息，如：

```
*****FormatMessage Header(Header) of EventTrace, parameter 23 raised an exception*****
```
