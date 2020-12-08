---
title: 符号存储和符号服务器
description: 符号存储和符号服务器
keywords:
- 符号服务器
- 符号服务器，概述
- 符号存储区
- 符号存储，概述
- SymSrv
- SymSrv，概述
- SymStore
- SymStore，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5a2e6416babe41afbf31a90cb041f9f55ee237b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813941"
---
# <a name="symbol-stores-and-symbol-servers"></a>符号存储和符号服务器


## <span id="ddk_using_symbol_servers_and_symbol_stores_dbg"></span><span id="DDK_USING_SYMBOL_SERVERS_AND_SYMBOL_STORES_DBG"></span>


*符号存储区* 是符号文件、索引和用于添加和删除文件的工具的集合。 符号存储还可以包含可执行的映像文件。 调试器使用 *符号服务器* 访问符号存储区中的文件。 适用于 Windows 的调试工具包括符号存储创建工具、 [SymStore](symstore.md)和符号服务器 [SymSrv](symsrv.md)。 它还包括一个工具 [SymProxy](symproxy.md)，用于在网络上设置 HTTP 符号存储，以用作调试器可能需要访问的所有符号存储区的代理。

本节包括：

[SymSrv](symsrv.md)

[使用符号服务器](using-a-symbol-server.md)

[HTTP 符号存储](http-symbol-stores.md)

[文件共享 (SMB) 符号服务器](file-share--smb--symbol-server.md)

[SymStore](symstore.md)

[SymProxy](symproxy.md)

如果未设置自己的符号存储区，而只是想要使用公共 Microsoft 符号存储区，请参阅 [Microsoft 公共符号](microsoft-public-symbols.md)。

 

 





