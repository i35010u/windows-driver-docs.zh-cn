---
title: 符号存储和符号服务器
description: 符号存储和符号服务器
ms.assetid: de35abe7-93ad-4ca0-94d4-bed1230e057b
keywords:
- 符号服务器
- 符号服务器概述
- 符号存储区
- 符号存储区概述
- SymSrv
- SymSrv 概述
- SymStore
- SymStore 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0943ddd04f7befbaf3ff99b3af284d0e5a2d10e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368063"
---
# <a name="symbol-stores-and-symbol-servers"></a>符号存储和符号服务器


## <span id="ddk_using_symbol_servers_and_symbol_stores_dbg"></span><span id="DDK_USING_SYMBOL_SERVERS_AND_SYMBOL_STORES_DBG"></span>


一个*符号存储区*是符号文件、 索引和工具，用于添加和删除文件的集合。 符号存储区也可能包含可执行文件的图像文件。 调试器使用访问符号存储区中的文件*符号服务器*。 调试工具的 Windows 包含这两个符号存储区创建工具、 [SymStore](symstore.md)，和符号服务器[SymSrv](symsrv.md)。 它还包括一个工具[SymProxy](symproxy.md)，设置以充当代理的所有符号的调试器可能需要访问存储在网络上 HTTP 符号存储区。

本部分包括：

[SymSrv](symsrv.md)

[使用符号服务器](using-a-symbol-server.md)

[HTTP 符号存储区](http-symbol-stores.md)

[文件共享 (SMB) 符号服务器](file-share--smb--symbol-server.md)

[SymStore](symstore.md)

[SymProxy](symproxy.md)

如果不设置自己符号存储区中，但只是想要使用公共 Microsoft 符号存储区，请参阅[Microsoft 公共符号](microsoft-public-symbols.md)。

 

 





