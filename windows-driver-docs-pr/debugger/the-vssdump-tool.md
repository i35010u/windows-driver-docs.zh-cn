---
title: VSSDump 工具
description: VSSDump 工具
keywords:
- Srcsrv.ini，VSSDump 工具
- VSSDump 工具
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0fdae546e350fea17ed9f8dcc77af994fb3ad66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787773"
---
# <a name="the-vssdump-tool"></a>VSSDump 工具


用于 Microsoft Visual SourceSafe 的索引编制脚本使用 VSSDump ( # A0) 工具。 它会收集要建立索引的源文件的列表。 此程序也是一个重要的命令行实用程序，你可以使用它来检查索引脚本可以处理的文件。

若要准备源索引，请编辑 Srcsrv.ini，使其包含版本控制服务器的条目。 此操作必须执行一次。 Srcsrv.ini 示例中列出了详细信息。 您可以使用环境变量或切换到索引脚本来表示此文件的位置。 不过，最好将它放在脚本所在的同一目录中，因为此文件的内容应在业务或开发系统中的所有项目中是全局的。 此文件用于唯一标识不同版本控制服务器。 请注意，你可以向调试器提供此文件的其他版本，以便它们查看版本控制服务器的复制副本，如果你想要降低服务器上的流量，这可能很有用。

若要为特定生成编制源索引，请确保在生成计算机上未签出任何源文件。 如果签出和编辑了任何文件，则这些更改不会反映在最终的源索引 .pdb 文件中。 此外，如果您的生成过程包含从其他文件生成源文件的预编译传递，则您必须将这些生成的文件作为预编译的一部分签入到版本控制中。

完成生成后，将当前工作目录设置为所有源文件和生成的 .pdb 文件的根。 然后运行 Ssindex.cmd。 您必须指定要用作参数的版本控制系统。 例如：

**ssindex.cmd = vss**

Ssindex.cmd 接受一些参数，这些参数允许你从任何位置运行脚本并单独指定源文件和 .pdb 文件的位置。 如果源保存在输出 .pdb 文件的另一个位置，则此方法最有用。 例如：

**ssindex.cmd = vss-source = c： \\**<em>source</em> **-符号 = c： \\**<em>outputdir</em>

还可以用环境变量指定这些目录。 使用-？ 或-?? 有关详细信息的命令行选项。

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

你还可以使用提供的包装脚本 (Vssindex) ，以避免指定版本控制系统。 脚本源-为在当前目录和下面找到的所有 .pdb 文件编制索引，并提供版本控制信息，以查找在当前目录和下面找到的所有源文件。 您可以使用环境变量和命令行开关为这些文件指定不同的位置。

完成源索引后，可以通过在 .pdb 文件上运行 Srctool.exe 来测试输出。 此程序显示的数据指示 .pdb 文件是否是源索引。 它还显示每个源文件的特定信息。 最后，它会显示已建立索引的源的数目，以及未找到其索引信息的源的数目。 如果文件不是源索引文件，则它会将% ERRORLEVEL% 设置为-1。 否则，它会将% ERRORLEVEL% 设置为索引源文件数。

还可以单独使用 VSSDump 在源索引时诊断问题。 语法如下：

**vssdump.exe** *选项*

*选项* 可以是下列选项的任意组合。

<span id="-a"></span><span id="-A"></span>**-a**  
导致搜索所有项目，而不是限制到当前项目。 此选项不能与 **-p** 选项一起使用。

<span id="-p_ProjectName"></span><span id="-p_projectname"></span><span id="-P_PROJECTNAME"></span>**-p** *项目名称*  
使 *VSSDump* 将其搜索限制为项目 *名称* 指定的项目。 如果此选项不存在，则使用当前项目。 此选项不能与 **-a** 选项一起使用。

<span id="-d_RootDirectory"></span><span id="-d_rootdirectory"></span><span id="-D_ROOTDIRECTORY"></span>**-d** *RootDirectory*  
使 *VSSDump* 将其搜索限制为 *RootDirectory* 指定的根目录。 如果此选项不存在，则使用当前目录。

<span id="-l_Label"></span><span id="-l_label"></span><span id="-L_LABEL"></span>**-l** *标签*  
使 *VSSDump* 仅列出标签与指定 *的标签相* 匹配的文件。

<span id="VSSDump-v_SharePath"></span><span id="vssdump-v_sharepath"></span><span id="VSSDUMP-V_SHAREPATH"></span>*VSSDump * * *-v* * *SharePath*  
指定虚拟 SourceSafe 数据库的位置是在 *SharePath* 中。 此选项将覆盖在 SSDIR 环境变量中指定的路径。

<span id="-r"></span><span id="-R"></span>**-r**  
使 *VSSDump* 以递归方式搜索子目录。

<span id="-f"></span><span id="-F"></span>**-f**  
使 *VSSDump* 列出包含源文件的目录，而不列出文件本身。

<span id="-i"></span><span id="-I"></span>**-i**  
使 *VSSDump* 忽略当前目录，并列出整个项目。 此选项不能与 **-r** 一起使用。

<span id="-s"></span><span id="-S"></span>**-s**  
导致 *VSSDump* 设置输出的格式，以便与脚本文件一起使用。

<span id="-c"></span><span id="-C"></span>**-c**  
使 *VSSDump* 只显示虚拟 SourceSafe 配置信息。









