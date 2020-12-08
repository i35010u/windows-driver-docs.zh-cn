---
title: 使用源服务器
description: 使用源服务器
keywords:
- '源服务器 ( # A0) '
- '源服务器 ( # A0) ，概述'
- 'Srcsrv.ini ( # A0) '
- 'Srcsrv.ini ( # A0) ，概述'
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1944f8ec5aa230a82d9cf7194a541a9a651aedd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803199"
---
# <a name="using-a-source-server"></a>使用源服务器


源服务器使调试器能够自动检索与当前目标匹配的源文件。 若要使用源服务器，必须在生成时调试已经过源索引的二进制文件，并将其源文件位置嵌入到 PDB 文件中。

适用于 Windows 的调试工具包含源服务器 [srcsrv.ini](srcsrv.md) ( # A0) 。

### <a name="span-idusing_srcsrv_with_a_debuggerspanspan-idusing_srcsrv_with_a_debuggerspanusing-srcsrv-with-a-debugger"></a><span id="using_srcsrv_with_a_debugger"></span><span id="USING_SRCSRV_WITH_A_DEBUGGER"></span>结合使用 Srcsrv.ini 和调试器

[Srcsrv.ini](srcsrv.md) 可以与 WINDBG、KD、NTSD 或 CDB 一起使用。

若要将 [srcsrv.ini](srcsrv.md) 与调试器一起使用，请输入以下命令，将源路径设置为 srv \* 。

```dbgcmd
.srcfix
```

可以通过输入以下命令获得相同的结果。

```dbgcmd
.srcpath srv*
```

将源路径设置为 srv 会 \* 告诉调试器，它应从目标模块的符号文件中指定的位置检索源文件。

如果要使用 [srcsrv.ini](srcsrv.md) 并在源路径中包含目录列表，请使用分号来分隔路径中的 `srv*` 所有目录。

例如：

```dbgcmd
.srcpath srv*;c:\someSourceCode 
```

如果按前面的示例中所示设置了源路径，则调试器将首先使用 [srcsrv.ini](srcsrv.md) 从目标模块的符号文件中指定的位置检索源文件。 如果 Srcsrv.ini 无法检索源文件，则调试器将尝试从 c： someSourceCode 检索该文件 \\ 。 无论 srv \* 是路径中的第一个元素还是稍后显示，调试器始终使用 SymSrv，然后再搜索路径中列出的任何其他目录。

你还可以使用 [**. srcfix +**](-srcfix---lsrcfix--use-source-server-.md) 向 `srv*` 现有源路径追加，如以下示例中所示。

```dbgcmd
3: kd> .srcpath c:\mySource
Source search path is: c:\mySource
3: kd> .srcfix+
Source search path is: c:\mySource;SRV*
```

如果源服务器检索到源文件，则在调试会话结束后，它将保留在您的硬盘上。 源文件以本地方式存储在主目录的 src 子目录中 (不同于符号服务器，源服务器未在 `srv*` 语法自身) 指定本地缓存。 主目录默认为调试器安装目录;可以通过使用 [**！ homedir**](-homedir.md) 扩展或通过设置 dbghelp.dll \_ homedir 环境变量来更改它。 如果此子目录尚不存在，则将创建它。

如果使用 " [**打开 (打开源文件")**](-open--open-source-file-.md) 命令，通过 [srcsrv.ini](srcsrv.md)打开一个新的源文件，则必须包含-m Address 参数。

有关如何为源编制索引的信息，或者，如果计划创建自己的源代码管理提供程序模块，请参阅 [srcsrv.ini](srcsrv.md)。

### <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

调试会话结束后， [srcsrv.ini](srcsrv.md) 下载的任何源文件都将保留在硬盘上。 若要控制源缓存的大小，可使用 AgeStore 工具删除早于指定日期的缓存文件，或将缓存的内容减小到指定的大小。 有关详细信息，请参阅 [AgeStore](agestore.md)。

 

 





