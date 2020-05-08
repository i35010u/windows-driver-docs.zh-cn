---
title: 语言规范 1
description: 语言规范 1
ms.assetid: 7c770200-ed2a-47e0-8389-e79a5624a3dd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4334732130a0db42fa066fe1015901788bf24be2
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925624"
---
# <a name="language-specification-1"></a>语言规范 1


第一版 Srcsrv.ini 的工作原理如下所示。 （在未来的版本中，此行为可能会发生更改。）

首先，客户端调用**SrcSrvInit** ，将目标路径用作所有源文件提取的基础。 此路径存储在特殊变量 TARG 中。

当 Dbghelp.dll 加载模块的 .pdb 文件时，它将从 .pdb 文件中提取 Srcsrv.ini 流，并通过调用**SrcSrvLoadModule**将此数据块传递到 srcsrv.ini。

然后，当 Dbghelp.dll 需要获取源文件时，它将调用**SrcSrvGetFile**从版本控制中检索指定的源文件。

Srcsrv.ini 查看数据块中的所有源文件条目，以获取与请求的源规范完全匹配的条目。 此匹配项在 VAR1 中找到。

在 Srcsrv.ini 找到该条目后，它会将特殊变量（VAR1、VAR2 等）填入此源文件项的内容。 然后使用这些特殊变量解析 SRCSRVTRG 变量。

下面演示了如何使用特殊变量解析 SRCSRVTRG 变量。 假设源路径仍然为：

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3
```

每行显示一个更特殊的变量的分辨率。 解析的变量为粗体。

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

请注意，生成的目标路径是唯一的，不允许将同一文件的两个版本提取到同一位置。

Srcsrv.ini 现在查看文件是否已存在。 如果为，则 Srcsrv.ini 会将位置返回到调用方。 否则，Srcsrv.ini 将生成执行命令，以通过解析 SRCSRVCMD 提取文件。

在下面的示例中，每一行都显示了一个更特殊的变量的分辨率。 解析的变量为粗体。

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

现在 Srcsrv.ini 执行此命令。 如果此命令的结果是预期位置中的文件，则此路径将返回到调用方。

请注意，如果无法解析某个变量，则会尝试将其查找为 OS 环境变量。 如果此操作失败，则从正在处理的文本中删除变量名称。

两个连续的百分号字符被解释为单百分比符号。

### <a name="span-idsource_server_data_blocksspanspan-idsource_server_data_blocksspansource-server-data-blocks"></a><span id="source_server_data_blocks"></span><span id="SOURCE_SERVER_DATA_BLOCKS"></span>源服务器数据块

Srcsrv.ini 依赖 .pdb 文件、源文件列表和数据块中的两个数据块。

生成模块时，会自动创建源文件列表。 此列表包含用于生成模块的源文件的完全限定路径。

数据块是在源索引期间创建的。 此时，将在 .pdb 文件中添加一个名为 "srcsrv.ini" 的备用流。 插入此数据的脚本依赖于特定的生成过程和正在使用的源代码管理系统。

数据块分为三部分： ini、变量和源文件。 数据块具有以下语法。

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

所有文本都按原义解释，但包含在百分号（%）中的文本除外。 百分号中包含的文本被视为递归解析的变量名称，除非它是以下函数之一：

<span id="_fnvar___"></span><span id="_FNVAR___"></span>**%fnvar%()**  
参数文本应括在百分号中，并被视为要解析的变量。

<span id="_fnbksl___"></span><span id="_FNBKSL___"></span>**%fnbksl%()**  
应该用反斜杠（\).）替换参数文本中的所有正斜杠（/）。

<span id="_fnfile___"></span><span id="_FNFILE___"></span>**%fnfile%()**  
应去掉参数文本中的所有路径信息，只留下文件名。

数据\[块\]的 ini 部分包含用于描述要求的变量。 索引脚本可以将任意数量的变量添加到此部分。 下面是一些示例：

<span id="VERSION"></span><span id="version"></span>**版本**  
语言规范版本。 此变量是必需的。 如果基于当前语言规范开发脚本，请将此值设置为1。 Srcsrv.ini 客户端代码不会尝试执行其值大于其自身的任何脚本。 当前版本的 Srcsrv.ini 使用值2。

<span id="VERCTL"></span><span id="verctl"></span>**VERCTL**  
描述源版本控制系统的字符串。 此变量是可选的。

<span id="DATETIME"></span><span id="datetime"></span>**型**  
一个字符串，指示 .pdb 文件的处理日期和时间。 此变量是可选的。

数据\[块\]的 variables 部分包含一些变量，这些变量描述如何从源代码管理提取文件。 它还可用于将常用文本定义为变量以减小数据块的大小。

<span id="SRCSRVTRG"></span><span id="srcsrv"></span>**SRCSRVTRG**  
描述如何为提取的文件生成目标路径。 这是一个必需的变量。

<span id="SRCSRVCMD"></span><span id="srcsrvcmd"></span>**SRCSRVCMD**  
介绍如何生成命令以便从源控件中提取文件。 这包括可执行文件的名称及其命令行参数。 如果必须执行任何提取命令，则这是必需的。

<span id="SRCSRVENV"></span><span id="srcsrvenv"></span>**SRCSRVENV**  
列出要在文件提取过程中创建的环境变量。 这是一个字符串。 用 backspace 符（\\b）分隔多个条目。 这是一个可选变量。

<span id="SRCSRVVERCTRL"></span><span id="srcsrvverctrl"></span>**SRCSRVVERCTRL**  
指定正在使用的版本控制系统。 对于 Perforce，这是 Perforce。 对于 Visual SourceSafe，此为 vss。 对于 Team Foundation Server，这是 tfs。 此变量用于保存服务器错误。 这是一个可选变量。

<span id="SRCSRVVERRDESC"></span><span id="srcsrvverrdesc"></span>**SRCSRVVERRDESC**  
指定在版本控制客户端无法联系包含要提取的源文件的服务器时要显示的文本。 Srcsrv.ini 使用此值检查连接问题。 这是一个可选变量。

<span id="SRCSRVERRVAR"></span><span id="srcsrverrvar"></span>**SRCSRVERRVAR**  
指示文件项中的哪个变量对应于版本控制服务器。 Srcsrv.ini 使用它来确定不起作用的命令，具体取决于以前的失败。 文本格式为 **var * * X* ，其中*X*是所指示的变量的编号。 这是一个可选变量。

数据\[块的\] "源文件" 部分包含已为其编制索引的每个源文件的条目。 每行的内容解释为名称为 VAR1、VAR2、VAR3 等的变量，依此类推，直到 VAR10。 变量用星号隔开。 VAR1 必须指定位于 .pdb 文件中其他位置的源文件的完全限定路径。 例如：

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3 
```

解释如下：

```console
VAR1=c:\proj\src\file.cpp
VAR2=TOOLS_PRJ
VAR3=tools/mytool/src/file.cpp
VAR4=3
```

在此示例中，VAR4 是修订号。 但是，大多数源代码管理系统都支持对文件进行标记，以便可以还原给定生成的源状态。 因此，可以改为使用该生成的标签。 可以修改示例数据块，使其包含如下所示的变量：

```console
LABEL=BUILD47 
```

然后，(假设源代码管理系统使用 at 符号（@）指示标签，可以按如下所示修改 SRCSRVCMD 变量：

```console
sd.exe -p %fnvar%(%var2%) print -o %srcsrvtrg% -q %depot%/%var3%@%label%
```

### <a name="span-idhandling_server_errorsspanspan-idhandling_server_errorsspanhandling-server-errors"></a><span id="handling_server_errors"></span><span id="HANDLING_SERVER_ERRORS"></span>处理服务器错误

有时，客户端无法从单个版本控制服务器提取所有文件。 这可能是因为服务器关闭并关闭了网络，或者因为用户没有适当的权限访问源。 但是，尝试获取此源所使用的时间可能会显著降低。 在这种情况下，最好禁用从已证实不可用的源中提取任何尝试。

只要 Srcsrv.ini 无法提取文件，它就会检查该命令生成的输出文本。 如果此命令的任何部分包含 SRCSRVERRDESC 内容的完全匹配项，则将跳过对同一版本控制服务器的所有未来命令。 请注意，可以通过将数字或任意文本添加到 SRCSRVERRDESC 变量名称的末尾来定义多个错误字符串。 以下是示例：

```console
SRCSRVERRDESC=lime: server not found
SRCSRVERRDESC_2=pineapple: network error
```

服务器的标识是从 SRCSRVERRVAR 获取的。 因此，如果 SRCSRVERRVAR 包含 "var2"，.pdb 文件中的文件条目如下所示：

```console
c:\proj\src\file.cpp*TOOLS_PRJ*tools/mytool/src/file.cpp*3
```

所有将来尝试使用在变量2中包含 "工具\_扩展名为 .prj" 的文件项获取源都将被绕过。

还可以通过编辑[srcsrv.ini](the-srcsrv-ini-file.md)在调试器客户端上添加错误指示器。 有关详细信息，请参阅包含的 srcsrv.ini 示例版本。

 

 





