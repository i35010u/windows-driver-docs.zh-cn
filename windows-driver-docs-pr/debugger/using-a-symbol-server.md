---
title: 使用符号服务器
description: 使用符号服务器
ms.assetid: 6c1687c7-7b9d-45f7-8778-c7284c4a8222
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ab2d732ed51664ffa7065968f79821ad7cd1990
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368161"
---
# <a name="using-a-symbol-server"></a>使用符号服务器


符号服务器还允许调试器符号从自动检索正确的符号文件存储的符号文件的索引的集合的而用户无需知道产品名称，不释放，或生成号。 有关 Windows 调试工具软件包包括符号服务器[SymSrv](symsrv.md) (symsrv.exe)。

### <a name="span-idusingsymsrvwithadebuggerspanspan-idusingsymsrvwithadebuggerspanusing-symsrv-with-a-debugger"></a><span id="using_symsrv_with_a_debugger"></span><span id="USING_SYMSRV_WITH_A_DEBUGGER"></span>在调试器使用 SymSrv

可使用 WinDbg、 KD、 NTSD 或 CDB SymSrv。

若要使用调试器使用此符号服务器，只需包含该文本**srv\\*** 符号路径中。 例如：

```console
set _NT_SYMBOL_PATH = srv*DownstreamStore*SymbolStoreLocation
```

其中*DownstreamStore*指定的本地目录或网络共享，将用于缓存单独的符号文件，并*SymbolStoreLocation*下列任意形式是符号存储区的位置 *\\\\服务器\\共享*或 internet 地址。 有关更多语法选项，请参阅[高级 SymSrv 使用](advanced-symsrv-use.md)。

Microsoft 已使 Windows 符号公开可用的网站。 也可以按以下方式于符号路径中引用直接访问此站点：

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

其中，再次*DownstreamStore*指定将用于缓存单独的符号文件的本地目录或网络共享。 有关详细信息，请参阅[Microsoft 公共符号](microsoft-public-symbols.md)。

如果你打算创建符号存储区，配置的 web (HTTP) 访问的符号存储区或编写你自己的符号服务器或符号存储区，请参阅[符号存储区和符号服务器](symbol-stores-and-symbol-servers.md)。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

调试会话结束后，由 SymSrv 下载的所有符号文件将都保留在您的硬盘上。 若要控制符号缓存的大小，可以删除早于指定日期的缓存的文件，或减少指定的大小如下缓存的内容中使用 AgeStore 工具。 有关详细信息，请参阅[AgeStore](agestore.md)。

 

 





