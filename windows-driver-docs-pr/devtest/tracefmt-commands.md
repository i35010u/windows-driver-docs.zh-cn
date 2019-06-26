---
title: Tracefmt 命令
description: 若要使用 Tracefmt，请在命令提示符窗口中键入命令。
ms.assetid: 79e56383-ce67-4716-98d6-4266b76a4b0a
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
ms.openlocfilehash: ed3beb3995e19bee9906cda44a31eb0a92d57598
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360335"
---
# <a name="tracefmt-commands"></a>Tracefmt 命令


若要使用 Tracefmt，请在命令提示符窗口中键入命令。 以下语法显示 Tracefmt 命令的元素。

若要在可读的形式显示跟踪消息，Tracefmt 必须应用于跟踪消息的跟踪消息格式文件中的格式设置说明。 您使用的语法取决于是否您拥有 TMF 文件跟踪提供程序，或是否想 Tracefmt 创建 TMF 文件。

若要提供 TMF 文件或目录的 TMF 文件路径：

```
    tracefmt [EtlFile | -rt SessionName][-tmf TMFFile | -p TMFPath ] [Options]
```

若要创建 TMF 文件：

```
    tracefmt [EtlFile | -rt SessionName]-i ImageFiles [-r SymbolPath ] [-p TmfPath ] [Options]
```

若要在命令行中显示的语法。

```
    tracefmt -h | /?
```

## <a name="span-idddktracefmtcommandstoolsspanspan-idddktracefmtcommandstoolsspanparameters"></a><span id="ddk_tracefmt_commands_tools"></span><span id="DDK_TRACEFMT_COMMANDS_TOOLS"></span>参数


<span id="_______EtlFile______"></span><span id="_______etlfile______"></span><span id="_______ETLFILE______"></span> *EtlFile*   
指定包含跟踪消息事件跟踪日志 (.etl) 文件。 输入的路径 （可选） 和文件名称。 默认值为 c:\\logfile.etl。

<span id="_______-rt________SessionName______"></span><span id="_______-rt________sessionname______"></span><span id="_______-RT________SESSIONNAME______"></span> **-rt** *SessionName*   
实际时间。 格式跟踪从指定的实时跟踪会话的消息而不是从[跟踪日志](trace-log.md)。

*会话名*跟踪会话的名称。 默认值是[NT 内核记录器](nt-kernel-logger-trace-session.md)。

<span id="_______-tmf_______TMFFile______"></span><span id="_______-tmf_______tmffile______"></span><span id="_______-TMF_______TMFFILE______"></span> **-tmf** *TMFFile*   
指定的路径 （可选） 和文件名称[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)的跟踪消息。 默认值为 Default.tmf，WDK 中包含的文件。

<span id="_______-i_______ImageFiles______"></span><span id="_______-i_______imagefiles______"></span><span id="_______-I_______IMAGEFILES______"></span> **-i** *ImageFiles*   
指示 Tracefmt 查找指定的图像文件的 PDB 符号文件和 PDB 文件中的格式设置操作说明创建 TMF 文件。

*ImageFiles*表示一个或多个二进制文件 （.exe、.dll 或.sys） 的路径和文件名的名称[跟踪提供程序](trace-provider.md)。 使用分号 （;）若要单独的图像文件名称。

<span id="_______-r_______SymbolPaths______"></span><span id="_______-r_______symbolpaths______"></span><span id="_______-R_______SYMBOLPATHS______"></span> **-r** *SymbolPaths*   
指定图像文件中指定专用的 PDB 符号文件的位置 **-i**。

*SymbolPaths*存储私有符号或符号服务器路径的目录中表示一个或多个路径。 使用分号 （;）若要分隔路径名称。 中的路径名称*SymbolPaths*可以包含通配符，例如星号 (\*) 来表示多个字符和问号 （？） 来表示单个字符。

如果包括 **-i**在命令中，但省略 **-r**，Tracepdb 搜索 PDB 文件中指定的百分比表示的路径指定的映像\_NT\_符号\_路径 %环境变量。 如果未设置环境变量，默认符号路径，以搜索 Tracepdb **srv\*\\\\\\\\符号\\\\符号**.

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span> **-p** *TMFPath*   
指定存储 TMF 文件的目录的路径。

时 **-p**使用不带 **-i**，在指定的路径中搜索 Tracefmt **-p**对于现有 TMF 文件。 如果 **-p** TMF 文件 %跟踪的值中省略 Tracefmt 看起来\_格式\_搜索\_PATH %环境变量，如果将其设置。 否则，Tracefmt 尝试应用 Default.tmf 文件中的格式设置说明。

当 **-p**用于 **-i**，Tracefmt 将放置在指定的目录中创建的 TMF 文件 **-p**。 如果 **-p**是省略，Tracefmt 置于 TMF 文件 %跟踪的值指定的目录\_格式\_搜索\_PATH %环境变量，如果将其设置。 否则，Tracefmt 将文件放在本地目录中。

<span id="_______-h_____"></span><span id="_______-H_____"></span> **-h** |  **/?**  
显示帮助。

<span id="_______-o_______OutputFile______"></span><span id="_______-o_______outputfile______"></span><span id="_______-O_______OUTPUTFILE______"></span> **-o** *OutputFile*   
指定的替代名称[Tracefmt 输出文件](tracefmt-output-file.md)并[Tracefmt 条摘要消息文件](summary-message-file.md)。 默认值为 FmfFile.txt （适用于输出文件中） 和 FmtSum.txt.sum （适用于摘要文件） 中的本地目录。

*OutputFile*是与.txt 文件扩展名，例如 c: 路径和文件名\\跟踪\\trace.txt。

如果使用此参数与 **-displayonly**或 **-summaryonly**选项，它会影响仅条摘要消息文件。

<span id="_______-csv______"></span><span id="_______-CSV______"></span> **-csv**   
格式化[Tracefmt 输出文件](tracefmt-output-file.md)作为以逗号分隔、 可变长度 (.csv) 文件。 此格式详细的结构化将前缀添加到每条消息，除了标准[跟踪消息前缀](trace-message-prefix.md)。

此选项会影响输出文件和显示的跟踪消息，在命令提示符窗口中，如果有的话。

<span id="_______-csvheader______"></span><span id="_______-CSVHEADER______"></span> **-csvheader**   
将描述性列标题的行添加到 CSV 文件。 此标头是用于解释 Tracefmt 将添加到 CSV 文件的结构化的前缀特别有用。 默认情况下，Tracefmt CSV 文件没有列标题。

<span id="_______-csvquote______"></span><span id="_______-CSVQUOTE______"></span> **-csvquote**   
两倍，CSV 文件中的所有引号 （"）。 此功能适用于显示引号引起来，仅当它们括在引号内的应用程序。

<span id="_______-display______"></span><span id="_______-DISPLAY______"></span> **-display**   
在命令提示符窗口中，除了写入到输出文件中显示的跟踪消息。

<span id="_______-displayonly______"></span><span id="_______-DISPLAYONLY______"></span> **-displayonly**   
仅在命令提示符窗口中显示跟踪消息并不会创建一个输出文件。

<span id="_______-nosummary______"></span><span id="_______-NOSUMMARY______"></span> **-nosummary**   
不会创建[条摘要消息文件](summary-message-file.md)。

<span id="_______-summaryonly______"></span><span id="_______-SUMMARYONLY______"></span> **-summaryonly**   
创建仅[条摘要消息文件](summary-message-file.md)。 不会创建 Tracefmt[输出文件](tracefmt-output-file.md)。

<span id="_______-noprefix______"></span><span id="_______-NOPREFIX______"></span> **-noprefix**   
省略[跟踪消息前缀](trace-message-prefix.md)。 此选项会影响输出文件和 Tracefmt 显示中的跟踪消息。

<span id="_______-hires______"></span><span id="_______-HIRES______"></span> **-hires**   
高分辨率。 显示跟踪消息时间戳中的微秒和纳秒为单位的数量。 默认情况下，显示仅毫秒为单位。

使用此选项，当性能计数器的时钟值用于跟踪消息的时间戳，而不是系统计时器，例如何时**Tracelog UsePerfCounter**使用参数。 有关跟踪日志命令的信息，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)。

<span id="_______-seq______"></span><span id="_______-SEQ______"></span> **-seq**   
显示中的本地或全局序列号[跟踪消息前缀](trace-message-prefix.md)。 如果消息中未记录序列号，该字段未初始化，或填充零或"f"s。

<span id="_______-ods______"></span><span id="_______-ODS______"></span> **-ods**   
将格式化的跟踪消息发送到调试程序，以便显示。

<span id="_______-gmt______"></span><span id="_______-GMT______"></span> **-gmt**   
每条跟踪消息以格林威治标准时间 (GMT) 上显示的时间戳。

此选项会影响 Tracefmt 输出文件。 它不转换的时间戳在事件跟踪日志 (.etl) 文件。 提交 Tracefmt 命令时，将显示的跟踪日志的时区。

<span id="_______-utc______"></span><span id="_______-UTC______"></span> **-utc**   
每条跟踪消息以协调世界时 (UTC) 上显示的时间戳。 UTC 几乎与格林威治标准时间，但它表示午夜为零。

此选项会影响 Tracefmt 输出文件。 它不转换的时间戳在事件跟踪日志 (.etl) 文件。 提交 Tracefmt 命令时，将显示的跟踪日志文件的时区。

<span id="_______-trace______"></span><span id="_______-TRACE______"></span> **-trace**   
显示 Tracefmt 操作发生时。 格式不正确或 Tracefmt 时报告错误或异常，此信息很有用。

显示在跟踪可能非常大。 请考虑将 Tracefmt 输出重定向到文本文件以供日后检查。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
详细。 显示的详细信息命令提示符窗口中的 Tracefmt 处理每个块或跟踪消息的缓冲区。 如果您怀疑发生文件损坏或不一致，请使用此选项。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**查找 TMF 文件**

如果省略 **-i**参数，Tracefmt 使用以下方法查找 TMF 文件。 为了让 Tracefmt 使用它们在列出方法。

-   **-Tmf**参数。

-   **-P**参数。

-   %跟踪\_格式\_搜索\_PATH %环境变量。

-   Default.tmf，WDK 中包含的文件。

如果 Tracefmt 找不到 TMF 文件，或 TMF 文件不包含格式化跟踪消息的信息，Tracefmt 无法显示的消息。 相反，它将写入以下错误消息来代替跟踪消息

```
No Format Information found.
```

**引发异常**

如果 Tracefmt 无法设置跟踪消息参数的格式，它会引发异常并显示一条消息，如：

```
*****FormatMessage Header(Header) of EventTrace, parameter 23 raised an exception*****
```

如果看到一个类似的异常，请查看源代码，特别要注意到任何用户指定的变量类型中的消息定义。 有关详细信息，请参阅[ **DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))。

**与非 GUID 文件名 TMF 文件**

如果 TMF 文件名称不是[消息 GUID](message-guid.md)，必须使用-tmf 参数标识的文件和输入文件的完全限定的路径。

**格式设置 NT 内核记录器跟踪消息**

从格式消息[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)或[全局记录器跟踪会话](global-logger-trace-session.md)，使用-tmf 参数来指定 system.tmf 文件[跟踪消息格式文件](trace-message-format-file.md) WDK 中包含...

**设置从实时跟踪会话的跟踪消息格式**

当你使用 **-rt** （实时） 参数，则 Tracefmt 显示一条消息，确认它在实时模式下，然后等待指定的跟踪提供程序中的跟踪消息。 它不会不返回到命令提示符，直到停止跟踪会话。

**格式设置 QPC 时间戳**

Tracefmt 不会格式化的系统性能计数器时钟的值 (**QueryPerformanceCounter**) 正确。 如果使用此高分辨率时，使用 Tracerpt，Windows XP 和更高版本的 Windows 中, 包含的工具来设置格式的跟踪消息。 有关详细信息，请参阅的说明 **-UsePerfCounter**中的参数[ **Tracelog 命令语法**](tracelog-command-syntax.md)。

**乱序跟踪消息**

如果您查看运行 Windows XP 的计算机上的跟踪消息文件，显示可能会显示跟踪消息的顺序。 若要更正此问题，可以启动跟踪会话并查看使用 Tracefmt 跟踪时使用的序列号选项。 然后可以查看跟踪与 Traceview 和根据序列号排序。 此外可以在运行 Windows Server 2003 或更高版本的 Windows 的计算机上查看的跟踪。









