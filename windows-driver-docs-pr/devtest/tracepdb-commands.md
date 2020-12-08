---
title: Tracepdb 命令
description: 若要使用 Tracepdb，请在命令提示符窗口中键入命令。 以下语法显示 Tracepdb 命令的元素。
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
ms.openlocfilehash: fd89e5eb26c13a3d484d1966cfa1f079fc3a20dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838117"
---
# <a name="tracepdb-commands"></a>Tracepdb 命令


若要使用 Tracepdb，请在命令提示符窗口中键入命令。 以下语法显示 Tracepdb 命令的元素。

使用以下参数指定 PDB 文件的位置。

```
    tracepdb [-f PDBFiles] [-s] [-p TMFDirectory] [-v] [-c]
```

使用以下参数为 [跟踪提供程序](trace-provider.md)指定映像文件。

```
    tracepdb -i ImageFiles [-r SymbolPaths] [-p TMFDiretory]  [-v]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-f_______PDBfiles______"></span><span id="_______-f_______pdbfiles______"></span><span id="_______-F_______PDBFILES______"></span>**-f** *PDBfiles*   
指定作为 Tracepdb 输入的 PDB 符号文件的位置。 默认情况下， \* 本地目录中为 .pdb。

*PDBFiles* 是一个或多个 PDB 文件的路径和文件名。 文件名可以包含通配符，如星号 (\*) ，以表示多个字符， (？ ) 表示单个字符。 使用分号 (; ) 分隔文件名。

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
以递归方式搜索。 为所有 PDB 文件创建 TMF 文件，该文件与目录中 **-f** 参数的值以及 **-f** 参数指定的路径的所有子目录匹配。 如果省略 **-f** ，则 **-s** 为本地目录及其子目录中的所有 PDB 文件创建 TMF 文件。

<span id="_______-p_______TMFDirectory______"></span><span id="_______-p_______tmfdirectory______"></span><span id="_______-P_______TMFDIRECTORY______"></span>**-p** *TMFDirectory*   
指定 Tracepdb 创建的 TMF 文件的位置。 默认值为本地目录。

TMF 文件是 Tracepdb 输出文件。 不能指定 TMF 文件的名称。 文件名为[跟踪提供程序](trace-provider.md)的[消息 GUID](message-guid.md) 。

<span id="_______-i_______ImageFiles______"></span><span id="_______-i_______imagefiles______"></span><span id="_______-I_______IMAGEFILES______"></span>**-i** *ImageFiles*   
指定本地计算机上 [跟踪提供程序](trace-provider.md) 的图像文件的位置。 使用 **-i** 参数时，Tracepdb 将使用图像文件的名称和版本来查找其 PDB 符号文件。

*ImageFiles* 是跟踪提供程序 ( .exe、.dll、.sys) 的一个或多个二进制文件的路径和文件名。 *ImageFiles* 中的文件名可以包含通配符，如 \* (表示多个字符) 和？  (表示单个字符) 。 使用分号 (**;**) 分隔图像文件名。

<span id="_______-r_______SymbolPaths______"></span><span id="_______-r_______symbolpaths______"></span><span id="_______-R_______SYMBOLPATHS______"></span>**-r** *SymbolPaths*   
指定 PDB 符号文件的位置。

*SymbolPaths* 表示一个或多个目录路径，这些路径存储私有符号或指向符号服务器上的目录。 *SymbolPaths* 中的路径名称可以包含通配符，如 \* (表示多个字符) 和？  (表示单个字符) 。

如果包括 **-i** 参数，但忽略 **-r**，则 Tracepdb 会在% \_ NT \_ 符号 \_ 路径% 环境变量指定的路径中搜索指定映像的 PDB 文件。 如果未设置环境变量，则 Tracepdb 会在默认符号路径中搜索 **srv \* \\ \\ \\ \\ 符号 \\ \\ 符号**。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
显示详细输出。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
生成 [TMC](trace-message-control-file.md) 文件。

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

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

TMF 文件的名称是源文件的 [消息 GUID](message-guid.md) 。 消息 GUID 表示文件中的源文件和跟踪条目。 Windows 使用消息 GUID 将跟踪消息与包含消息格式说明的 TMF 文件相关联。

如果提交的 PDB 符号文件不包括跟踪格式设置说明，Tracepdb 将显示信息消息，并且不会创建任何文件。

如果 Tracefmt 在指定的路径中找不到任何 PDB 文件，它将返回到命令提示符而不进行注释。 若要获取处理详细信息，请重新提交带有 **-v** 参数的命令。









