---
title: 使用符号服务器
description: 使用符号服务器
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: efe1ffffd1c17adf26c891450f6f2b91d8876a4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803195"
---
# <a name="using-a-symbol-server"></a>使用符号服务器


符号服务器使调试器能够自动从符号存储中检索正确的符号文件-符号文件的索引集合-无需用户知道产品名称、版本或生成号。 用于 Windows 的调试工具包包含符号 server [SymSrv](symsrv.md) ( # A0) 。

### <a name="span-idusing_symsrv_with_a_debuggerspanspan-idusing_symsrv_with_a_debuggerspanusing-symsrv-with-a-debugger"></a><span id="using_symsrv_with_a_debugger"></span><span id="USING_SYMSRV_WITH_A_DEBUGGER"></span>结合使用 SymSrv 和调试器

SymSrv 可以与 WinDbg、KD、NTSD 或 CDB 一起使用。

若要将此符号服务器用于调试器，只需在符号路径中包含文本 **srv \\** _ 即可。 例如：

```console
set _NT_SYMBOL_PATH = srv_DownstreamStore*SymbolStoreLocation
```

其中， *DownstreamStore* 指定将用于缓存各个符号文件的本地目录或网络共享，而 *SymbolStoreLocation* 是符号存储区的位置，格式为 *\\ \\ 服务器 \\ 共享* 或 internet 地址。 有关更多语法选项，请参阅 [Advanced SymSrv Use](advanced-symsrv-use.md)。

Microsoft 拥有一个使 Windows 符号公开可用的网站。 可以通过以下方式直接在符号路径中引用此站点：

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

其中， *DownstreamStore* 指定将用于缓存各个符号文件的本地目录或网络共享。 有关详细信息，请参阅 [Microsoft 公共符号](microsoft-public-symbols.md)。

如果计划创建符号存储区、为 web (HTTP) access 配置符号存储区，或者编写自己的符号服务器或符号存储区，请参阅 [符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。

### <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

调试会话结束后，SymSrv 下载的所有符号文件都将保留在硬盘上。 若要控制符号缓存的大小，可使用 AgeStore 工具删除早于指定日期的缓存文件，或将缓存的内容减小到指定的大小。 有关详细信息，请参阅 [AgeStore](agestore.md)。

 

 





