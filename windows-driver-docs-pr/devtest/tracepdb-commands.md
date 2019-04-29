---
title: Tracepdb 命令
description: 若要使用 Tracepdb，请在命令提示符窗口中键入命令。 以下语法显示 Tracepdb 命令的元素。
ms.assetid: c6502f26-d50e-48dc-85b4-978a83abff33
keywords:
- Tracepdb 命令驱动程序开发工具
topic_type:
- apiref
api_name:
- Tracepdb Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cbe1a056df14579548d49e3aacbc2c5d1f9d5e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369687"
---
# <a name="tracepdb-commands"></a>Tracepdb 命令


若要使用 Tracepdb，请在命令提示符窗口中键入命令。 以下语法显示 Tracepdb 命令的元素。

使用以下参数来指定 PDB 文件的位置。

```
    tracepdb [-f PDBFiles] [-s] [-p TMFDirectory] [-v] [-c]
```

使用以下参数来指定的图像文件[跟踪提供程序](trace-provider.md)。

```
    tracepdb -i ImageFiles [-r SymbolPaths] [-p TMFDiretory]  [-v]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-f_______PDBfiles______"></span><span id="_______-f_______pdbfiles______"></span><span id="_______-F_______PDBFILES______"></span> **-f** *PDBfiles*   
指定是为 Tracepdb 输入 PDB 符号文件的位置。 默认值是\*.pdb 中的本地目录。

*PDBFiles*是一个或多个 PDB 文件的路径和文件名称。 文件名称可以包含通配符，例如星号 (\*) 来表示多个字符和问号 （？） 来表示单个字符。 使用分号 （;）若要单独的文件的名称。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
以递归方式搜索。 创建文件的值匹配的所有 PDB 文件，TMF **-f**目录和指定的路径的所有子目录中的参数 **-f**参数。 如果 **-f**省略，则 **-s** TMF 文件的所有 PDB 文件创建本地目录及其子目录中。

<span id="_______-p_______TMFDirectory______"></span><span id="_______-p_______tmfdirectory______"></span><span id="_______-P_______TMFDIRECTORY______"></span> **-p** *TMFDirectory*   
指定创建 Tracepdb TMF 文件的位置。 默认值为本地目录。

TMF 文件是 Tracepdb 输出文件。 不能指定 TMF 文件的名称。 文件名称是[消息 GUID](message-guid.md)的[跟踪提供程序](trace-provider.md)。

<span id="_______-i_______ImageFiles______"></span><span id="_______-i_______imagefiles______"></span><span id="_______-I_______IMAGEFILES______"></span> **-i** *ImageFiles*   
指定的图像文件的位置[跟踪提供程序](trace-provider.md)本地计算机上。 当你使用 **-i**参数，Tracepdb 使用的名称和图像文件的版本来查找其 PDB 符号文件。

*ImageFiles*是路径和文件名的一个或多个二进制文件 （.exe、.dll、.sys） 的跟踪提供程序。 该文件中的名称*ImageFiles*可以包括通配符，例如\*（来表示多个字符） 和？ （若要表示单个字符）。 使用分号 (**;**) 来分隔图像文件名。

<span id="_______-r_______SymbolPaths______"></span><span id="_______-r_______symbolpaths______"></span><span id="_______-R_______SYMBOLPATHS______"></span> **-r** *SymbolPaths*   
指定的 PDB 符号文件的位置。

*SymbolPaths*表示一个或多个路径，对存储私有符号的目录或符号服务器上的目录。 中的路径名称*SymbolPaths*可以包括通配符，例如\*（来表示多个字符） 和？ （若要表示单个字符）。

如果包括 **-i**参数，但省略 **-r**，Tracepdb 搜索 PDB 文件中指定的百分比表示的路径指定的映像\_NT\_符号\_路径 %环境变量。 如果未设置环境变量，默认符号路径，以搜索 Tracepdb **srv\*\\\\\\\\符号\\\\符号**.

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
显示详细输出。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
将生成[TMC](trace-message-control-file.md)文件。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

```
tracepdb -v
tracepdb -f tracedrv.pdb
tracepdb -f c:\tracing\ndis*.pdb -s
tracepdb -f d:\tools\trace*.pdb -p d:\tracing
tracepdb -i d:\winddk\7060\src\general\tracing\tracedrv\objfre_wnet_x86_vh\tracedrv.sys -r 
tracepdb -i trace*.exe;flpy*.dll -p d:\tracing
tracepdb -i tracedrv.exe -r srv*\\\\symbolstore\\symbols\\new
```

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

TMF 文件的名称是[消息 GUID](message-guid.md)的源文件。 消息 GUID 表示源代码文件和文件中的跟踪条目。 Windows 使用消息的 GUID 与包含的消息的格式说明该 TMF 文件关联的跟踪消息。

如果提交不包括跟踪格式说明的 PDB 符号文件，Tracepdb 显示的信息性消息，并不会创建任何文件。

如果 Tracefmt 找不到任何 PDB 文件中指定的路径，它将返回到命令提示符下，不加说明。 若要获取处理详细信息，重新提交该命令与 **-v**参数。









