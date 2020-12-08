---
title: Tracefmt 命令
description: 若要使用 Tracefmt，请在命令提示符窗口中键入命令。
keywords:
- Tracefmt 命令驱动程序开发工具
topic_type:
- apiref
api_name:
- Tracefmt Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2f38f1b0b43d56caa3c54408f9d0dc631a3d857
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839661"
---
# <a name="tracefmt-commands"></a>Tracefmt 命令


若要使用 Tracefmt，请在命令提示符窗口中键入命令。 以下语法显示 Tracefmt 命令的元素。

若要以可读形式显示跟踪消息，Tracefmt 必须将跟踪消息格式文件中的格式说明应用到跟踪消息。 使用的语法取决于是否为跟踪提供程序提供了 TMF 文件，或者是否希望 Tracefmt 创建 TMF 文件。

若要提供 TMF 文件或 TMF 文件的目录的路径，请执行以下操作：

```
    tracefmt [EtlFile | -rt SessionName][-tmf TMFFile | -p TMFPath ] [Options]
```

若要创建 TMF 文件：

```
    tracefmt [EtlFile | -rt SessionName]-i ImageFiles [-r SymbolPath ] [-p TmfPath ] [Options]
```

在命令行中显示语法。

```
    tracefmt -h | /?
```

## <a name="span-idddk_tracefmt_commands_toolsspanspan-idddk_tracefmt_commands_toolsspanparameters"></a><span id="ddk_tracefmt_commands_tools"></span><span id="DDK_TRACEFMT_COMMANDS_TOOLS"></span>参数


<span id="_______EtlFile______"></span><span id="_______etlfile______"></span><span id="_______ETLFILE______"></span>*EtlFile*   
指定包含跟踪消息 ( .etl) 文件的事件跟踪日志。 输入路径 (可选) 和文件名。 默认值为 c： \\ logfile。

<span id="_______-rt________SessionName______"></span><span id="_______-rt________sessionname______"></span><span id="_______-RT________SESSIONNAME______"></span>**-rt** *SessionName*   
实时。 从指定的实时跟踪会话而不是 [跟踪日志](trace-log.md)设置跟踪消息的格式。

*SessionName* 是跟踪会话的名称。 默认值为 " [NT 内核记录器](nt-kernel-logger-trace-session.md)"。

<span id="_______-tmf_______TMFFile______"></span><span id="_______-tmf_______tmffile______"></span><span id="_______-TMF_______TMFFILE______"></span>**-tmf** *TMFFile*   
为跟踪消息指定 [跟踪消息格式 ( tmf) 文件](trace-message-format-file.md) 的路径 (可选的) 和文件名。 默认值为 tmf，这是在 WDK 中包含的文件。

<span id="_______-i_______ImageFiles______"></span><span id="_______-i_______imagefiles______"></span><span id="_______-I_______IMAGEFILES______"></span>**-i** *ImageFiles*   
指示 Tracefmt 查找指定图像文件的 PDB 符号文件，并根据 PDB 文件中的格式设置说明创建 TMF 文件。

*ImageFiles* 表示 [跟踪提供程序](trace-provider.md) ( .exe、.dll 或 .sys) 的一个或多个二进制文件的路径和文件名。 使用分号 (; ) 分隔图像文件名。

<span id="_______-r_______SymbolPaths______"></span><span id="_______-r_______symbolpaths______"></span><span id="_______-R_______SYMBOLPATHS______"></span>**-r** *SymbolPaths*   
指定 **-i** 中指定的映像文件的专用 PDB 符号文件的位置。

*SymbolPaths* 表示存储私有符号或符号服务器路径的目录的一个或多个路径。 使用分号 (; ) 分隔路径名。 *SymbolPaths* 中的路径名称可以包含通配符，如星号 (\*) 以表示多个字符， (？ ) 表示单个字符。

如果在命令中包含 **-i** ，但忽略 **-r**，则 Tracepdb 会在% \_ NT \_ 符号 \_ 路径% 环境变量指定的路径中搜索指定映像的 PDB 文件。 如果未设置环境变量，则 Tracepdb 会在默认符号路径中搜索 **srv \* \\ \\ \\ \\ 符号 \\ \\ 符号**。

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span>**-p** *TMFPath*   
指定存储 TMF 文件的目录的路径。

如果使用 **-p** 而不使用 **-i**，Tracefmt 将在 **-p** 指定的路径中搜索现有的 TMF 文件。 如果省略 **-p** ，Tracefmt 将在% TRACE \_ 格式搜索路径% 环境变量的值中查找 TMF 文件 \_ \_ （如果已设置）。 否则，Tracefmt 会尝试在 tmf 文件中应用格式说明。

将 **-p** 与 **-i** 一起使用时，Tracefmt 会将它创建的 TMF 文件放在 **-p** 指定的目录中。 如果省略 **-p** ，则 Tracefmt 会将 TMF 文件放在% TRACE 格式搜索路径% 环境变量的值所指定的目录中 \_ \_ \_ （如果已设置）。 否则，Tracefmt 会将文件放在本地目录中。

<span id="_______-h_____"></span><span id="_______-H_____"></span>**-h**  | **/?**  
显示帮助。

<span id="_______-o_______OutputFile______"></span><span id="_______-o_______outputfile______"></span><span id="_______-O_______OUTPUTFILE______"></span>**-o** *OutputFile*   
指定 [Tracefmt 输出文件](tracefmt-output-file.md) 和 [Tracefmt 摘要消息文件](summary-message-file.md)的替换名称。 默认值为输出文件的默认值 FmtSum.txt) 为本地目录中的摘要文件 ( (FmfFile.txt。

*OutputFile* 是具有 .txt 文件扩展名的路径和文件名，如 c： \\ 跟踪 \\trace.txt。

如果将此参数与 **-displayonly** 或 **-summaryonly** 选项一起使用，则它只会影响摘要消息文件。

<span id="_______-csv______"></span><span id="_______-CSV______"></span>**-csv**   
将 [Tracefmt 输出文件](tracefmt-output-file.md) 的格式设置为逗号分隔的可变长度 ( .csv) 文件。 此格式向每条消息添加了一个详细的结构化前缀，还添加了标准 [跟踪消息前缀](trace-message-prefix.md)。

此选项会影响输出文件和跟踪消息在命令提示符窗口中的显示方式（如果有）。

<span id="_______-csvheader______"></span><span id="_______-CSVHEADER______"></span>**-csvheader**   
向 CSV 文件添加一行描述性列标题。 此标头对于解释 Tracefmt 添加到 CSV 文件的结构化前缀特别有用。 默认情况下，Tracefmt CSV 文件没有列标题。

<span id="_______-csvquote______"></span><span id="_______-CSVQUOTE______"></span>**-csvquote**   
在 CSV 文件中将所有引号标记 ( ") 加倍。 此功能适用于仅在用引号引起引号时才显示引号的应用程序。

<span id="_______-display______"></span><span id="_______-DISPLAY______"></span>**-display**   
除了将跟踪消息写入到输出文件，还在命令提示符窗口中显示这些跟踪消息。

<span id="_______-displayonly______"></span><span id="_______-DISPLAYONLY______"></span>**-displayonly**   
仅在命令提示符窗口中显示跟踪消息，不会创建输出文件。

<span id="_______-nosummary______"></span><span id="_______-NOSUMMARY______"></span>**-nosummary**   
不创建 [摘要消息文件](summary-message-file.md)。

<span id="_______-summaryonly______"></span><span id="_______-SUMMARYONLY______"></span>**-summaryonly**   
仅创建 [摘要消息文件](summary-message-file.md)。 Tracefmt 不会创建 [输出文件](tracefmt-output-file.md)。

<span id="_______-noprefix______"></span><span id="_______-NOPREFIX______"></span>**-noprefix**   
省略 [跟踪消息前缀](trace-message-prefix.md)。 此选项会影响输出文件和 Tracefmt 显示中的跟踪消息。

<span id="_______-hires______"></span><span id="_______-HIRES______"></span>**-招聘**   
高分辨率。 显示跟踪消息时间戳的微秒和纳秒数。 默认情况下，仅显示毫秒。

当性能计数器时钟值用于跟踪消息时间戳而不是系统计时器（如使用 **Tracelog-UsePerfCounter** 参数时）时，请使用此选项。 有关 Tracelog 命令的信息，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md)。

<span id="_______-seq______"></span><span id="_______-SEQ______"></span>**-seq**   
显示 [跟踪消息前缀](trace-message-prefix.md)中的本地序列号或全局序列号。 如果未在消息中记录序列号，则字段未初始化或用零或 "f" 填充。

<span id="_______-ods______"></span><span id="_______-ODS______"></span>**-ods**   
将格式化跟踪消息发送到调试器以显示。

<span id="_______-gmt______"></span><span id="_______-GMT______"></span>**-gmt**   
在格林尼治标准时间 (GMT) 中显示每个跟踪消息的时间戳。

此选项仅影响 Tracefmt 输出文件。 它不会将事件跟踪日志中的时间戳转换 ( .etl) 文件中。 提交 Tracefmt 命令时，将显示跟踪日志的时区。

<span id="_______-utc______"></span><span id="_______-UTC______"></span>**-utc**   
以协调世界时 (UTC) 显示每个跟踪消息上的时间戳。 UTC 与 GMT 几乎完全相同，但它表示午夜为零。

此选项仅影响 Tracefmt 输出文件。 它不会将事件跟踪日志中的时间戳转换 ( .etl) 文件中。 提交 Tracefmt 命令时，将显示跟踪日志文件的时区。

<span id="_______-trace______"></span><span id="_______-TRACE______"></span>**-trace**   
显示 Tracefmt 操作。 当格式不正确或 Tracefmt 报告错误或异常时，此信息很有用。

跟踪显示范围可能会很大。 考虑将 Tracefmt 输出重定向到一个文本文件，以便以后检查。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
“详细”： 在 "命令提示符" 窗口中显示详细信息，因为 Tracefmt 处理跟踪消息的每个块或缓冲区。 如果怀疑文件损坏或不一致，请使用此选项。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**查找 TMF 文件**

如果省略 **-i** 参数，Tracefmt 将使用以下方法来查找 TMF 文件。 按 Tracefmt 使用这些方法的顺序列出这些方法。

-   **-Tmf** 参数。

-   **-P** 参数。

-   % TRACE \_ 格式 \_ 搜索 \_ 路径% 环境变量。

-   Tmf，它是一种包含在 WDK 中的文件。

如果 Tracefmt 找不到 TMF 文件，或 TMF 文件未包含跟踪消息的格式设置信息，则 Tracefmt 无法显示这些消息。 相反，它会编写以下错误消息来代替跟踪消息

```
No Format Information found.
```

**引发了异常**

如果 Tracefmt 无法设置跟踪消息参数的格式，则会引发异常并显示一条消息，如下所示：

```
*****FormatMessage Header(Header) of EventTrace, parameter 23 raised an exception*****
```

如果看到类似的异常，请在源代码中查看消息定义，并特别注意任何用户指定的变量类型。 有关详细信息，请参阅 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))。

**具有非 GUID 文件名的 TMF 文件**

如果 TMF 文件名不是 [消息 GUID](message-guid.md)，则必须使用-TMF 参数来标识文件，并输入文件的完全限定路径。

**格式化 NT 内核记录器跟踪消息**

若要从 " [NT 内核记录器" 跟踪会话](nt-kernel-logger-trace-session.md) 或 [全局记录器跟踪会话](global-logger-trace-session.md)设置消息的格式，请使用-tmf 参数来指定 tmf 文件，这是在 WDK 中包含的 [跟踪消息格式文件](trace-message-format-file.md) 。

**从实时跟踪会话设置跟踪消息的格式**

使用 **-rt** (实时) 参数时，Tracefmt 将显示一条消息，确认它处于实时模式，然后等待来自指定跟踪提供程序的跟踪消息。 它不会返回到命令提示符，直到跟踪会话停止。

**设置 QPC 时间戳的格式**

Tracefmt **) 正确** 设置系统性能计数器时钟 (的值的格式。 如果使用的是高分辨率时间，请使用 Tracerpt （Windows XP 及更高版本的 Windows 中包含的工具）来格式化跟踪消息。 有关详细信息，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md)中 **-UsePerfCounter** 参数的描述。

**不顺序跟踪消息**

如果在运行 Windows XP 的计算机上查看跟踪消息文件，则显示的跟踪消息可能不按顺序显示。 若要更正此问题，可以在启动跟踪会话时使用序列号选项，并使用 Tracefmt 查看跟踪。 然后，可以根据序列号查看具有 Traceview 和排序的跟踪。 你还可以在运行 Windows Server 2003 或更高版本的 Windows 的计算机上查看跟踪。
