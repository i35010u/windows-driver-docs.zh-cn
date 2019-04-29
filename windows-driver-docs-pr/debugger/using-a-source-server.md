---
title: 使用源服务器
description: 使用源服务器
ms.assetid: b3467f26-1ce3-42cb-a8c8-a7d10efc5079
keywords:
- 源服务器 (srcsrv.dll)
- 源服务器 (srcsrv.dll) 概述
- SrcSrv (srcsrv.dll)
- SrcSrv (srcsrv.dll) 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e2cf4d155227156e6f98ead371ffe6df53acb32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367963"
---
# <a name="using-a-source-server"></a>使用源服务器


源服务器使调试器能够自动检索与当前目标匹配的源文件。 若要使用的源服务器，必须调试二进制文件的源编制索引在生成时，并为其源文件位置嵌入 PDB 文件中。

调试工具的 Windows 包括源服务器[SrcSrv](srcsrv.md) (Srcsrv.exe)。

### <a name="span-idusingsrcsrvwithadebuggerspanspan-idusingsrcsrvwithadebuggerspanusing-srcsrv-with-a-debugger"></a><span id="using_srcsrv_with_a_debugger"></span><span id="USING_SRCSRV_WITH_A_DEBUGGER"></span>SrcSrv 使用调试程序

[SrcSrv](srcsrv.md)可与 WinDbg、 KD、 NTSD 或 CDB。

若要使用[SrcSrv](srcsrv.md)调试器中，输入以下命令以将源路径设置为 srv\*。

```dbgcmd
.srcfix
```

可以通过输入以下命令来获取相同的结果。

```dbgcmd
.srcpath srv*
```

将源路径设置为 srv\*告知调试器，应从目标模块的符号文件中指定的位置检索源文件。

如果你想要使用[SrcSrv](srcsrv.md)并且还包括在你的源路径的目录列表中，使用分号分隔`srv*`从路径中的任何目录。

例如：

```dbgcmd
.srcpath srv*;c:\someSourceCode 
```

如果在前面的示例所示设置的源路径，则首先使用调试器[SrcSrv](srcsrv.md)来从目标模块的符号文件中指定的位置检索源文件。 如果无法检索源文件 SrcSrv，调试器会尝试检索从 c:\\someSourceCode。 无论是否 srv\*路径中的第一个元素或更高版本，显示调试器始终使用 SymSrv 之前它将搜索路径中列出的任何其他目录。

此外可以使用[ **.srcfix +** ](-srcfix---lsrcfix--use-source-server-.md)追加`srv*`到现有的源路径，如下面的示例中所示。

```dbgcmd
3: kd> .srcpath c:\mySource
Source search path is: c:\mySource
3: kd> .srcfix+
Source search path is: c:\mySource;SRV*
```

如果源文件由源服务器检索，它将保留在您的硬盘中，调试会话结束后。 源文件存储在本地中的主目录的子目录 (与不同的符号服务器中，源服务器未指定本地缓存中的`srv*`语法本身)。 主目录将默认为调试器安装目录;可以通过更改[ **！ homedir** ](-homedir.md)扩展或通过设置 DBGHELP\_主目录环境变量。 如果尚不存在此子目录，将创建它。

如果您使用[ **（打开源文件） 打开**](-open--open-source-file-.md)命令，以打开新的源文件，并通过[SrcSrv](srcsrv.md)，你必须包括-m 地址参数。

了解如何以编制索引源，或如果您计划创建你自己源控件提供程序的模块，请参阅[SrcSrv](srcsrv.md)。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

任何源下载文件[SrcSrv](srcsrv.md)调试会话结束后将保留在您的硬盘上。 若要控制源缓存的大小，可以删除早于指定日期的缓存的文件，或减少指定的大小如下缓存的内容中使用 AgeStore 工具。 有关详细信息，请参阅[AgeStore](agestore.md)。

 

 





