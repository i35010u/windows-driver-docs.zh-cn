---
title: 使用 SrcSrv
description: 使用 SrcSrv
ms.assetid: 2696e5e9-343f-49a2-bdab-23a54f8c9e5c
keywords:
- SrcSrv (srcsrv.dll) 的源服务器
- SrcSrv 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 650872e6dfb0ef7d1f7ac0c1d27050ec985255a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353097"
---
# <a name="using-srcsrv"></a>使用 SrcSrv


若要使用[SrcSrv](srcsrv.md)与 WinDbg、 KD、 NTSD 或 CDB，验证是否已安装最新版本[对于 Windows 调试工具](https://docs.microsoft.com/windows-hardware/drivers/debugger/)包 （版本 6.3 或更高版本）。 然后，包括文本`srv*`在源路径中，用分号分隔从还源路径中的任何目录。

例如：

```dbgcmd
.srcpath srv*;c:\someSourceCode
```

如果在前面的示例所示设置的源路径，则首先使用调试器[SrcSrv](srcsrv.md)来从目标模块的符号文件中指定的位置检索源文件。 如果无法检索源文件 SrcSrv，调试器会尝试检索从 c:\\someSourceCode。 无论是否 srv\*路径中的第一个元素或更高版本，显示调试器始终使用 SymSrv 之前它将搜索路径中列出的任何其他目录。

如果检索源文件[SrcSrv](srcsrv.md)，调试会话结束后将其保留在您的硬盘。 源文件存储在本地中的主目录的子目录 (与不同的符号服务器中，源服务器未指定本地缓存中的`srv*`语法本身)。 主目录将默认为用于 Windows 调试工具安装目录;可以通过更改[ **！ homedir** ](-homedir.md)扩展或通过设置 DBGHELP\_主目录环境变量。 如果尚不存在的主目录的子目录，则创建它。

### <a name="span-iddebuggingsrcsrvspanspan-iddebuggingsrcsrvspandebugging-srcsrv"></a><span id="debugging_srcsrv"></span><span id="DEBUGGING_SRCSRV"></span>调试 SrcSrv

如果遇到从调试器中提取的源文件时出现问题，请使用-n 若要查看实际的源提取命令以及这些命令的输出的命令行参数启动调试器。 ！ 符号干扰性命令执行同样的操作，但可能已丢失了从以前的提取尝试的重要信息。 这是因为调试器放弃尝试访问源似乎是无法访问的版本控制存储库中。

### <a name="span-idretrievingsourcefilesspanspan-idretrievingsourcefilesspanretrieving-source-files"></a><span id="retrieving_source_files"></span><span id="RETRIEVING_SOURCE_FILES"></span>检索源文件

如果您使用[ **（打开源文件） 打开**](-open--open-source-file-.md)命令，以打开新的源文件，并通过[SrcSrv](srcsrv.md)，你必须包括-m 地址参数。

为方便使用的[SrcSrv](srcsrv.md)从最前面列出的调试以外的工具，DbgHelp API 提供了对通过 SrcSrv 功能的访问**SymGetSourceFile**函数。 若要检索要检索的源文件的名称，请调用**SymEnumSourceFiles**或**SymGetLineFromAddr64**函数。 DbgHelp API 的更多详细信息，请参阅 dbghelp.chm 文档，其中可以找到有关 Windows 调试工具安装目录中，在 sdk/帮助子目录中，或请参阅[调试帮助库](https://go.microsoft.com/fwlink/p/?linkid=125231)。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

任何源下载文件[SrcSrv](srcsrv.md)调试会话结束后保留在您的硬盘上。 若要控制源缓存的大小，可以删除早于指定日期的缓存的文件，或减少指定的大小如下缓存的内容中使用 AgeStore 工具。 有关详细信息，请参阅[AgeStore](agestore.md)。

 

 





