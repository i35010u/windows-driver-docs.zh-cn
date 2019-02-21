---
title: VSSDump 工具
description: VSSDump 工具
ms.assetid: b213c949-3433-4686-8323-5af83a6ee5b1
keywords:
- SrcSrv，VSSDump 工具
- VSSDump 工具
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76c003ba7304593bea2007bcadadbfa4dfe2bfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521702"
---
# <a name="the-vssdump-tool"></a>VSSDump 工具


为 Microsoft Visual SourceSafe，VSSDump (Vssdump.exe) 工具可供索引脚本。 它会收集源文件要编制索引的列表。 此程序也是有价值的命令行实用工具，可用于检查的索引的脚本可能处理过的文件。

若要准备源索引，请编辑 Srcsrv.ini，使其包含在版本控制服务器的条目。 这是必须一次执行的操作。 在示例版本 Srcsrv.ini 中列出了详细信息。 可以使用环境变量，也可以切换到索引的脚本来表示此文件的位置。 但是，最好将其放入与脚本相同的目录，因为此文件的内容用于跨企业或开发系统中的所有项目是全局的。 此文件可用于唯一地标识不同的版本控制服务器。 请注意，您可以提供此文件的不同版本到调试器以便查看版本控制服务器，这可能有帮助，如果你想要减少服务器上的流量的复制副本。

为源索引特定生成，请确保没有源文件签出在生成计算机上。 如果任何文件是签出和编辑，这些更改将不会反映在编制索引的最终源.pdb 文件。 此外，如果您的生成过程包括从其他文件生成源代码文件预编译传递，你必须签入到版本控制作为预编译的一部分这些生成的文件。

在生成完成，设置要作为根的所有源文件和生成的.pdb 文件的当前工作目录。 然后，运行 SSIndex。 必须指定作为参数使用何种版本控制系统。 例如：

**ssindex.cmd -server=vss**

SSIndex 接受允许您从任何位置运行该脚本还可以单独指定源文件和.pdb 文件的位置的参数。 这会十分有用，如果源保存在从.pdb 文件输出的另一个位置。 例如：

**ssindex.cmd -server=vss -source=c:\\**<em>source</em> **-symbols=c:\\**<em>outputdir</em>

此外可以使用环境变量来指定这些目录。 使用？ 或-?? 有关详细信息的命令行选项。

下面是此脚本生成的输出示例：

```console
## C:\ >ssindex.cmd -system=vss -?

SSIndex.cmd [/option=<value> [...]] [ModuleOptions] [/Debug]
General SrcSrv settings:
     NAME              SWITCH      ENV. VAR        Default
  -----------------------------------------------------------------------------
  1) srcsrv.ini        Ini         SRCSRV_INI      .\srcsrv.ini
  2) Source root       Source      SRCSRV_SOURCE   .
  3) Symbols root      Symbols     SRCSRV_SYMBOLS  .
  4) Control system    System      SRCSRV_SYSTEM   <N/A>
  5) Save File (opt.)  Save        SRCSRV_SAVE     <N/A>
  6) Load File (opt.)  Load        SRCSRV_LOAD     <N/A>
Visual Source Safe specific settings:
     NAME            SWITCH      ENV. VAR        Default
  -----------------------------------------------------------------------------
  A) VSS Server      Server      SSDIR            <N/A>
  B) VSS Client      Client      SSROOT           <Current directory>
  C) VSS Project     Project     SSPROJECT        <N/A>
  D) VSS Label       Label       SSLABEL          <N/A>
Precedence is: Default, environment, cmdline switch. (ie. env overrides default,
switch overrides env).
Using '/debug' will turn on verbose output.
Use "SSIndex.cmd -??" for verbose help information.
## See SrcSrv documentation for more information.
```

此外可以使用提供的包装器脚本 (Vssindex.cmd) 之一来避免指定版本控制系统。 脚本源索引所有.pdb 文件在当前目录中找到和以下版本控制信息，若要查找所有源文件找到在当前目录及更低。 可以使用环境变量和命令行开关来指定这些文件的不同位置。

完成后的源索引，可以通过运行 SrcTool.pdb 文件在测试输出。 此程序显示指示.pdb 文件为源编制索引的数据。 它还显示每个源文件的特定信息。 最后，它显示多个索引的源和找到没有索引的信息的源的数目。 如果文件不是源编制索引，它设置为-1 %ERRORLEVEL%。 否则，它设置为索引的源文件数 %ERRORLEVEL%。

VSSDump 还可独立诊断源索引期间遇到的问题。 语法是按如下所示：

**vssdump.exe** *Options*

*选项*可以是下列选项中的任意组合。

<span id="-a"></span><span id="-A"></span>**-a**  
将导致所有项目，以进行搜索，而不是限制到当前项目。 此选项不能使用与 **-p**选项。

<span id="-p_ProjectName"></span><span id="-p_projectname"></span><span id="-P_PROJECTNAME"></span>**-p** *ProjectName*  
将导致*VSSDump*以将其搜索限制到指定的项目*ProjectName*。 如果此选项不存在，则使用当前项目。 此选项不能使用与 **-a**选项。

<span id="-d_RootDirectory"></span><span id="-d_rootdirectory"></span><span id="-D_ROOTDIRECTORY"></span>**-d** *RootDirectory*  
将导致*VSSDump*以将其搜索限制为指定的根目录*RootDirectory*。 如果没有此选项，则使用当前目录。

<span id="-l_Label"></span><span id="-l_label"></span><span id="-L_LABEL"></span>**-l** *Label*  
将导致*VSSDump*若要列出带有标签与匹配指定的那些文件*标签*。

<span id="VSSDump-v_SharePath"></span><span id="vssdump-v_sharepath"></span><span id="VSSDUMP-V_SHAREPATH"></span>*VSSDump***-v** *SharePath*  
指定虚拟 SourceSafe 数据库的位置位于*SharePath*。 此选项可重写 SSDIR 环境变量中指定的路径。

<span id="-r"></span><span id="-R"></span>**-r**  
将导致*VSSDump*搜索子目录以递归方式。

<span id="-f"></span><span id="-F"></span>**-f**  
将导致*VSSDump*到列表而不列出文件本身包含源文件的目录。

<span id="-i"></span><span id="-I"></span>**-i**  
将导致*VSSDump*以忽略当前目录，并列出整个项目。 此选项不能使用与 **-r**。

<span id="-s"></span><span id="-S"></span>**-s**  
将导致*VSSDump*输出格式设置为用于脚本文件。

<span id="-c"></span><span id="-C"></span>**-c**  
将导致*VSSDump*以显示虚拟 SourceSafe 配置信息。









