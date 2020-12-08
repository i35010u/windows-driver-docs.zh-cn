---
title: DBH 命令行选项
description: THIS->DBH 命令行使用以下语法。
keywords:
- THIS->DBH Command-Line 选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DBH Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 503facb3c54c00e3d3aff2f610a177aa31739a6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833189"
---
# <a name="dbh-command-line-options"></a>DBH 命令行选项


THIS->DBH 命令行使用以下语法。

```console
dbh [Options] -p:PID [Command] 

dbh [Options] ExecutableName [Command] 

dbh [Options] SymbolFileName [Command] 

dbh -? 

dbh -??  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="-p_PID"></span><span id="-p_pid"></span><span id="-P_PID"></span>**-p：**<em>PID</em>  
指定要加载其符号的进程的进程 ID。

<span id="_______ExecutableName______"></span><span id="_______executablename______"></span><span id="_______EXECUTABLENAME______"></span>*ExecutableName*   
指定要加载其符号的可执行文件，包括文件扩展名 (通常是 .exe 或 .sys) 。 应包含相对或绝对目录路径;如果未包含路径，则假定为当前工作目录。 如果在此位置找不到指定的文件，THIS->DBH 将使用 **SymLoadModuleEx** 搜索该文件。

<span id="_______SymbolFileName______"></span><span id="_______symbolfilename______"></span><span id="_______SYMBOLFILENAME______"></span>*SymbolFileName*   
指定要加载其符号的符号文件，包括文件扩展名 ( .pdb 或 dbg) 。 应包含相对或绝对目录路径;如果未包含路径，则假定为当前工作目录。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下选项的任意组合。

<span id="-d"></span><span id="-D"></span>**-d.ddd...e**  
导致在显示符号和搜索符号时使用修饰名。 使用此选项时，将 [ \_ \_ 仅打开 SYMOPT PUBLICS](symbol-options.md#symopt-publics-only) ，同时禁用 SYMOPT \_ UNDNAME 和 SYMOPT \_ AUTO \_ PUBLICS。 这等效于在运行 THIS->DBH 后发出命令 symopt + 4000 后跟 symopt-10002。

<span id="-s_Path"></span><span id="-s_path"></span><span id="-S_PATH"></span>**-s：**<em>路径</em>  
将符号路径设置为指定的 *路径* 值。

<span id="-n_"></span><span id="-N_"></span>**-n**   
打开 *干扰符号加载*。 将显示有关搜索符号的其他信息。 每个符号文件的名称将在加载时显示。 如果调试器无法加载符号文件，则将显示一条错误消息。 .Pdb 文件的错误消息以文本显示。 Dbg 文件的错误消息以错误代码的形式出现，如 winerror.h 文件中所述。 并非所有这些消息都有用，但其中一些消息可能有助于分析找不到或不匹配符号文件的原因。 如果加载图像文件只是为了恢复符号标头信息，则也会显示此信息。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span>*命令*   
使 THIS->DBH 运行，执行指定的 *命令*，然后退出。 有关可能的命令的列表，请参阅 [This->dbh 命令](dbh-commands.md)。

<span id="_______-_______"></span> **-?**   
显示 THIS->DBH 命令行的帮助文本。

<span id="_______-________"></span> **-??**   
显示 THIS->DBH 命令行的帮助文本，并显示所有 THIS->DBH 命令的列表。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 THIS->DBH 工具的详细信息，请参阅 [使用 this->dbh](using-dbh.md)。

 

 





