---
title: DBH 命令行选项
description: DBH 命令行使用以下语法。
ms.assetid: fd333c2d-1f07-4a47-8653-e10cf58417a5
keywords:
- DBH 命令行选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DBH Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 482138a444fcc8780381ba7f8dee4a4f652398da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373381"
---
# <a name="dbh-command-line-options"></a>DBH 命令行选项


DBH 命令行使用以下语法。

```console
dbh [Options] -p:PID [Command] 

dbh [Options] ExecutableName [Command] 

dbh [Options] SymbolFileName [Command] 

dbh -? 

dbh -??  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="-p_PID"></span><span id="-p_pid"></span><span id="-P_PID"></span>**-p:**<em>PID</em>  
指定要加载其符号的进程的进程 ID。

<span id="_______ExecutableName______"></span><span id="_______executablename______"></span><span id="_______EXECUTABLENAME______"></span> *ExecutableName*   
指定的可执行文件的符号加载，其中包括文件扩展名 （通常是.exe 或.sys）。 应包含相对或绝对目录路径;如果包括任何路径，不则，假定当前工作目录。 如果在此位置找不到指定的文件，也可以使用搜索 DBH **SymLoadModuleEx**。

<span id="_______SymbolFileName______"></span><span id="_______symbolfilename______"></span><span id="_______SYMBOLFILENAME______"></span> *SymbolFileName*   
指定要加载其符号的符号文件包括文件扩展名 （.pdb 或.dbg）。 应包含相对或绝对目录路径;如果包括任何路径，不则，假定当前工作目录。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下选项的任意组合。

<span id="-d"></span><span id="-D"></span>**-d**  
原因修饰名，用于显示符号和搜索符号。 使用此选项时， [SYMOPT\_PUBLICS\_仅](symbol-options.md#symopt-publics-only)处于打开状态，并且这两个 SYMOPT\_UNDNAME 和 SYMOPT\_自动\_PUBLICS 处于关闭状态。 这是发出命令 symopt +4000 运行 DBH 后跟 symopt-10002 等效。

<span id="-s_Path"></span><span id="-s_path"></span><span id="-S_PATH"></span>**-s:**<em>路径</em>  
设置为指定的符号路径*路径*值。

<span id="-n_"></span><span id="-N_"></span>**-n**   
开启*干扰符号加载*。 有关搜索符号显示其他信息。 加载时显示每个符号文件的名称。 如果调试器无法加载符号文件，它会显示一条错误消息。 在文本中显示的.pdb 文件的错误消息。 .Dbg 文件的错误消息是在 winerror.h 文件中所述的错误代码的形式。 并非所有这些消息都很有用，但其中一些可能会有所帮助分析为什么无法找到或匹配的符号文件。 如果加载的图像文件只是为了恢复符号标头信息，这是也显示。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*   
原因 DBH 若要运行，执行指定*命令*，然后退出。 有关可用命令的列表，请参阅[DBH 命令](dbh-commands.md)。

<span id="_______-_______"></span> **-?**   
显示帮助文本 DBH 命令行。

<span id="_______-________"></span> **-??**   
显示帮助文本 DBH 命令行中，并显示所有 DBH 命令的列表。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 DBH 工具的详细信息，请参阅[使用 DBH](using-dbh.md)。

 

 





