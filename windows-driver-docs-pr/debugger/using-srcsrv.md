---
title: 使用 SrcSrv
description: 使用 SrcSrv
ms.assetid: 2696e5e9-343f-49a2-bdab-23a54f8c9e5c
keywords:
- '源服务器，Srcsrv.ini ( # A0) '
- Srcsrv.ini，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6db71c431d8b8ce513a42dc0a1e431ba153885fb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207329"
---
# <a name="using-srcsrv"></a>使用 SrcSrv


若要将 [srcsrv.ini](srcsrv.md) 与 WINDBG、KD、NTSD 或 CDB 一起使用，请验证是否已安装最新版本的 [适用于 Windows 的调试工具](./index.md) (版本6.3 或更高版本) 。 然后，将源路径中的文本包含在 `srv*` 源路径中的所有目录中，以分号分隔。

例如：

```dbgcmd
.srcpath srv*;c:\someSourceCode
```

如果按前面的示例中所示设置了源路径，则调试器将首先使用 [srcsrv.ini](srcsrv.md) 从目标模块的符号文件中指定的位置检索源文件。 如果 Srcsrv.ini 无法检索源文件，则调试器将尝试从 c： someSourceCode 检索该文件 \\ 。 无论 srv \* 是路径中的第一个元素还是稍后显示，调试器始终使用 SymSrv，然后再搜索路径中列出的任何其他目录。

如果 [srcsrv.ini](srcsrv.md)检索到源文件，则在调试会话结束后，该文件将保留在硬盘上。 源文件以本地方式存储在主目录的 src 子目录中 (不同于符号服务器，源服务器未在 `srv*` 语法自身) 指定本地缓存。 主目录默认为适用于 Windows 的调试工具安装目录;可以通过使用 [**！ homedir**](-homedir.md) 扩展或通过设置 dbghelp.dll \_ homedir 环境变量来更改它。 如果主目录的 src 子目录尚不存在，则创建它。

### <a name="span-iddebugging_srcsrvspanspan-iddebugging_srcsrvspandebugging-srcsrv"></a><span id="debugging_srcsrv"></span><span id="DEBUGGING_SRCSRV"></span>调试 Srcsrv.ini

如果从调试器提取源文件时遇到任何问题，请用-n 命令行参数启动调试器，以查看实际的源提取命令以及这些命令的输出。 ！符号干扰命令会执行相同的操作，但你可能已经丢失了上一次提取尝试中的重要信息。 这是因为，调试器会尝试从看起来无法访问的版本控制存储库访问源。

### <a name="span-idretrieving_source_filesspanspan-idretrieving_source_filesspanretrieving-source-files"></a><span id="retrieving_source_files"></span><span id="RETRIEVING_SOURCE_FILES"></span>检索源文件

如果使用 " [**打开 (打开源文件") **](-open--open-source-file-.md) 命令，通过 [srcsrv.ini](srcsrv.md)打开一个新的源文件，则必须包含-m Address 参数。

为了便于使用之前所列调试器之外的工具中的 [srcsrv.ini](srcsrv.md) ，dbghelp.dll API 通过 **SymGetSourceFile** 函数提供对 srcsrv.ini 功能的访问权限。 若要检索要检索的源文件的名称，请调用 **SymEnumSourceFiles** 或 **SymGetLineFromAddr64** 函数。 有关 Dbghelp.dll API 的更多详细信息，请参阅 dbghelp.dll 文档，该文档可在适用于 Windows 的调试工具安装目录的 sdk/help 子目录中找到，或参阅 [调试帮助库](/windows/win32/debug/debug-help-library)。

### <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

调试会话结束后， [srcsrv.ini](srcsrv.md) 下载的任何源文件都将保留在硬盘上。 若要控制源缓存的大小，可使用 AgeStore 工具删除早于指定日期的缓存文件或将缓存内容减小到指定的大小。 有关详细信息，请参阅 [AgeStore](agestore.md)。

 

