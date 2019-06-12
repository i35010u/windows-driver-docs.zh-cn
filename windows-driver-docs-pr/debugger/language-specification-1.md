---
title: 语言规范 1
description: 语言规范 1
ms.assetid: 7c770200-ed2a-47e0-8389-e79a5624a3dd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55a81ac47ec93c8000e0c0c7ba8b4c36406d5d40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383517"
---
# <a name="language-specification-1"></a>语言规范 1


SrcSrv 的第一个版本的工作原理如下。 （此行为可能会更改在将来版本。）

首先，客户端调用**SrcSrvInit**与要用作基类，所有源文件提取的目标路径。 此路径存储在特殊的变量目标扩展名。

当 DbgHelp 加载模块的.pdb 文件时，它从.pdb 文件中提取 SrcSrv 数据流对该并通过调用将此数据块传递给 SrcSrv **SrcSrvLoadModule**。

然后，当 DbgHelp 需要获取源代码文件，它调用**SrcSrvGetFile**从版本控制文件中检索指定的源。

SrcSrv 评审与完全请求的源规范相匹配的条目的数据块中的所有源代码文件条目。 VAR1 中找到匹配项。

SrcSrv 找到了该项后，它与此源文件条目的内容填充 （VAR1、 VAR2 等） 的特殊变量。 然后使用这些特殊变量解析 SRCSRVTRG 变量。

下面演示了如何 SRCSRVTRG 变量是使用特殊变量解析。 我们假设源路径，仍是：

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3 
```

每行显示了一个更特殊的变量的分辨率。 已解析的变量用粗体显示。

```console
SRCSRVTRG=%sdtrg% 
SDTRG=%targ%\%var2%\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%)
c:\src\%var2%\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\%fnbksl%( sdktools/debuggers/srcsrv/shell.cpp )\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\ sdktools\debuggers\srcsrv\shell.cpp\%var4%\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\%fnfile%(%var1%)
c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\%fnfile%( c:\db\srcsrv\shell.cpp)
c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp
```

请注意如何此生成的目标路径是唯一的并且不允许两个版本的同一个文件提取到相同的位置。

SrcSrv 现在看起来有该文件已存在。 如果是，SrcSrv 位置返回给调用方。 否则，SrcSrv 生成执行命令，通过解析 SRCSRVCMD 来解压缩该文件。

在以下示例中，每行显示了一个更特殊的变量的分辨率。 已解析的变量用粗体显示。

```console
DEPOT=//depot 
WIN_SDKTOOLS= sserver.microsoft.com:4444 
SRCSRVCMD=%sdcmd% 
SDCMD=sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
sd.exe -p %fnvar%(WIN_SDKTOOLS) print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q %depot%/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q //depot/%var3%#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q //depot/ sdktools/debuggers/srcsrv/shell.cpp#%var4% 
sd.exe -p sserver.microsoft.com:4444  print -o c:\src\WIN_SDKTOOLS\sdktools\debuggers\srcsrv\shell.cpp\3\shell.cpp -q //depot/ sdktools/debuggers/srcsrv/shell.cpp#3 
```

现在 SrcSrv 执行此命令。 如果此命令的结果是预期的位置中的文件，此路径返回到调用方。

请注意，是否变量不能被解析，尝试查找它为 OS 环境变量。 如果失败，将从正在处理的文本中删除变量的名称。

两个连续的百分号字符被解释为一个百分号。

### <a name="span-idsourceserverdatablocksspanspan-idsourceserverdatablocksspansource-server-data-blocks"></a><span id="source_server_data_blocks"></span><span id="SOURCE_SERVER_DATA_BLOCKS"></span>源服务器的数据块

SrcSrv 依赖于两个.pdb 文件、 源文件列表和数据块中的数据块。

生成模块时，将自动创建源代码文件列表。 此列表包含用于生成模块的源代码文件的完全限定的路径。

源索引编制过程中创建的数据块。 在此期间，名为"srcsrv"备用流添加到.pdb 文件。 将此数据插入的脚本是依赖于特定的生成过程和源控制系统中使用。

数据块分为三个部分： ini、 变量和源文件。 数据块具有以下语法。

```console
SRCSRV: ini ------------------------------------------------ 
VERSION=1
VERCTRL=<source_control_str>
DATETIME=<date_time_str>
SRCSRV: variables ------------------------------------------ 
SRCSRVTRG=%sdtrg% 
SRCSRVCMD=%sdcmd% 
SRCSRVENV=var1=string1\bvar2=string2 
DEPOT=//depot 
SDCMD=sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%#%var4% 
SDTRG=%targ%\%var2%\%fnbksl%(%var3%)\%var4%\%fnfile%(%var1%) 
WIN_SDKTOOLS= sserver.microsoft.com:4444 
SRCSRV: source files --------------------------------------- 
<path1>*<var2>*<var3>*<var4> 
<path2>*<var2>*<var3>*<var4> 
<path3>*<var2>*<var3>*<var4> 
<path4>*<var2>*<var3>*<var4> 
SRCSRV: end ------------------------------------------------
```

所有文本是原义解释，除了文本括在百分号 （%）。 括在百分号中的文本被视为要递归式解析的变量名称，除非它是一个以下函数：

<span id="_fnvar___"></span><span id="_FNVAR___"></span> **%fnvar%()**  
参数文本框应包含在百分号并被视为变量会得到解决。

<span id="_fnbksl___"></span><span id="_FNBKSL___"></span> **%fnbksl%()**  
在参数文本框中的所有正斜杠 （/） 应替换为反斜杠 (\)。

<span id="_fnfile___"></span><span id="_FNFILE___"></span> **%fnfile%()**  
参数文本框中的所有路径信息应会都剥除，保留的文件名。

\[Ini\]的数据块部分包含介绍的要求的变量。 索引的脚本可以将任意数量的变量添加到此部分。 下面是一些示例：

<span id="VERSION"></span><span id="version"></span>**VERSION**  
语言规范版本。 此变量是必需的。 如果您要开发基于当前语言规范的脚本，将此值设置为 1。 SrcSrv 客户端代码不会尝试执行任何脚本都大于其自己的值。 当前版本的 SrcSrv 使用值为 2。

<span id="VERCTL"></span><span id="verctl"></span>**VERCTL**  
一个字符串，描述源版本控制系统。 此变量是可选的。

<span id="DATETIME"></span><span id="datetime"></span>**DATETIME**  
已处理的字符串表示日期和时间的.pdb 文件。 此变量是可选的。

\[变量\]的数据块部分包含介绍如何从源代码管理提取文件的变量。 此外可以用于定义常用的文本作为变量以减少数据块的大小。

<span id="SRCSRV"></span><span id="srcsrv"></span>**SRCSRV**  
介绍如何构建提取的文件的目标路径。 这是必需的变量。

<span id="SRCSRVCMD"></span><span id="srcsrvcmd"></span>**SRCSRVCMD**  
介绍如何生成要从源代码管理提取文件的命令。 这包括可执行文件和其命令行参数的名称。 如果必须执行任何提取命令，这是必需的。

<span id="SRCSRVENV"></span><span id="srcsrvenv"></span>**SRCSRVENV**  
列出了用于文件在提取期间创建的环境变量。 这是一个字符串。 使用退格符的字符分隔多个项 (\\b)。 这是可选的变量。

<span id="SRCSRVVERCTRL"></span><span id="srcsrvverctrl"></span>**SRCSRVVERCTRL**  
在使用指定的版本控制系统。 对于 Perforce，这是 perforce。 对于 Visual SourceSafe 中，这是 vss。 对于 Team Foundation Server，这是 tfs。 使用此变量将保留出现服务器错误。 这是可选的变量。

<span id="SRCSRVVERRDESC"></span><span id="srcsrvverrdesc"></span>**SRCSRVVERRDESC**  
指定版本控制客户端无法联系包含要提取的源文件的服务器时要显示的文本。 SrcSrv 使用此值来检查存在连接问题。 这是可选的变量。

<span id="SRCSRVERRVAR"></span><span id="srcsrverrvar"></span>**SRCSRVERRVAR**  
指示文件条目中的哪个变量对应于版本控制服务器。 SrcSrv 使用它来标识不起作用，基于以前失败的命令。 文本的格式为 **var * * * X*其中*X*是指示该变量的数目。 这是可选的变量。

\[源文件\]的数据块部分包含每个源文件编制索引的条目。 每个行的内容被解释为具有名称 VAR1，VAR2，VAR3 的变量，依此类推直到 VAR10。 由星号分隔变量。 VAR1 必须指定.pdb 文件中其他位置列出的源文件的完全限定的路径。 例如：

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3 
```

解释，如下所示：

```console
VAR1=c:\proj\src\file.cpp
VAR2=TOOLS_PRJ
VAR3=tools/mytool/src/file.cpp
VAR4=3
```

在此示例中，VAR4 是修订号。 但是，大多数源控制系统支持标记的方式可以还原给定生成的源状态的文件。 因此，您可以改用标签进行生成。 可以修改示例数据块包含一个变量，如下所示：

```console
LABEL=BUILD47 
```

然后，假设源控制系统使用 at 符号 (@) 若要指示一个标签，可以修改 SRCSRVCMD 变量，如下所示：

```console
sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%@%label%
```

### <a name="span-idhandlingservererrorsspanspan-idhandlingservererrorsspanhandling-server-errors"></a><span id="handling_server_errors"></span><span id="HANDLING_SERVER_ERRORS"></span>处理服务器错误

有时客户端不能从一个版本控制服务器根本提取的任何文件。 这可能是由于服务器与网络断开和向下或者用户不具有访问源的相应权限。 但是，尝试获取此源使用的时间可以使操作慢下来显著。 在此情况下，最好禁用从已被证实不可用的源中提取的任何尝试。

每当 SrcSrv 无法提取文件，它将检查该命令生成的输出文本。 如果此命令的任何部分包含的 SRCSRVERRDESC 内容的完全匹配项，将跳过所有后续命令到相同的版本控制服务器。 请注意，您可以通过 SRCSRVERRDESC 变量名称的末尾添加数字或任意文本来定义多个错误字符串。 下面是一个示例：

```console
SRCSRVERRDESC=lime: server not found
SRCSRVERRDESC_2=pineapple: network error
```

从 SRCSRVERRVAR 获取服务器的标识。 因此如果 SRCSRVERRVAR 包含"var2"和.pdb 文件中的文件条目如下所示：

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3
```

所有未来都尝试获取使用包含的文件条目的源，"工具\_PRJ"在变量 2 会绕过。

您还可以添加错误指示符调试器客户端上通过编辑[Srcsrv.ini](the-srcsrv-ini-file.md)。 请参阅有关详细信息的 srcsrv.ini 的随附的示例版本。

 

 





