---
title: SymProxy
description: SymProxy
keywords:
- '符号，SymProxy ( # A0) '
- 符号存储，HTTP
- '符号存储，SymProxy ( # A0) '
- SymProxy
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a0501d1cb7bf162fb6f3dee074c6d8f64c475fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813933"
---
# <a name="symproxy"></a>SymProxy


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


可以配置基于 HTTP 的符号存储，使其在客户端计算机和其他符号存储之间充当代理。 实现是通过 Internet 服务器应用程序编程接口 (ISAPI) 筛选器， ( # A0) 。 SymProxy 服务器可用作 Internet 或公司网络中其他源的网关计算机。 下图显示了一个示例 SymProxy 配置。

![示例 symproxy 配置示意图](images/symproxy-configuration.png)

在许多情况下，SymProxy 很有用。 例如：

-   在实验室环境中调试许多系统，其中的计算机未连接到公司网络，但这些符号存储在网络中，必须使用集成 Windows 身份验证 (IWA) 进行访问。

-   你的企业计算环境包括防火墙，该防火墙阻止从正在调试的计算机访问 Internet，你必须从 Internet 网站获取符号。

-   您希望为公司中的所有用户提供一个符号路径，以便他们不需要知道或关心符号所在的位置，而无需用户干预即可添加新的符号存储区。

-   你的远程站点与公司资源的剩余部分不在远处，网络访问速度较慢。 此系统可用于获取符号并将它们缓存到远程站点。

若要安装 SymProxy，你必须手动将文件复制到正确的位置、配置注册表、选择网络安全凭据，并 (IIS) 配置 Internet Information Services。 若要确保 HTTP 符号存储正确配置，请参阅 [Http 符号存储](http-symbol-stores.md)。

### <a name="span-idmultiple_symbol_server_performance_considerationsspanspan-idmultiple_symbol_server_performance_considerationsspanspan-idmultiple_symbol_server_performance_considerationsspanmultiple-symbol-server-performance-considerations"></a><span id="Multiple_Symbol_Server_Performance_Considerations"></span><span id="multiple_symbol_server_performance_considerations"></span><span id="MULTIPLE_SYMBOL_SERVER_PERFORMANCE_CONSIDERATIONS"></span>多个符号服务器性能注意事项

每个虚拟目录可以与多个 (上游) 符号存储区相关联。 每个符号存储区单独进行查询。 为了提高性能，应在 internet HTTP 服务器之前处理本地 SMB 服务器。 不同于调试器符号路径，可以在 SymProxy 符号路径中指定多个 HTTP 符号存储区。 每个虚拟目录最多支持10个条目。

### <a name="span-idsymproxy_symbol_pathspanspan-idsymproxy_symbol_pathspanspan-idsymproxy_symbol_pathspansymproxy-symbol-path"></a><span id="SymProxy_Symbol_Path"></span><span id="symproxy_symbol_path"></span><span id="SYMPROXY_SYMBOL_PATH"></span>SymProxy 符号路径

SymProxy 会将) 符号路径值中定义的 (注册表拆分为单个项，并使用每个项生成基于 SRV 的 \* 符号路径来检索文件。 它使用虚拟目录的文件夹作为每个查询中的下游存储（实际上就是将上游存储合并到单个下游符号存储区中）。

SymProxy 所使用) 符号路径生成的 (相当于：

```dbgcmd
SRV*<Virtual Directory Folder>*<SymbolPath Entry #N>
```

在此示例中，UNC 路径和两个 HTTP 路径都与一个虚拟目录相关联，以便合并来自企业符号服务器、Microsoft 和第三方 (Contoso) 的符号。 SymProxy SymbolPath 的设置如下所示：

```console
\\MainOffice\Symbols;https://msdl.microsoft.com/download/symbols;
https://symbols.contoso.com/symbols
```

首先使用) 符号路径的 (生成的主办公符号文件共享：

```dbgcmd
SRV*D:\SymStore\Symbols*\\MainOffice\Symbols
```

如果找不到符号文件，则将使用生成的 () 符号路径来查询 Microsoft 符号存储区：

```dbgcmd
SRV*D:\SymStore\Symbols*https://msdl.microsoft.com/download/symbols
```

如果仍找不到该文件，则 `(https://symbols.contoso.com/symbols)` 会使用 (生成的) 符号路径来查询 Contoso 符号存储区：

```dbgcmd
SRV*D:\SymStore\Symbols*https://symbols.contoso.com/symbols
```

本节包括：

[安装 SymProxy](installing-symproxy.md)

[配置注册表](configuring-the-registry.md)

[选择网络安全凭据](choosing-network-security-credentials.md)

[为 SymProxy 配置 IIS](configuring-iis-for-symproxy.md)

[设置排除列表](setting-up-exclusion-lists.md)

[处理不可用的符号存储](dealing-with-unavailable-symbol-stores.md)

[处理文件指针](handling-file-pointers.md)

[缓存获取的符号文件](caching-acquired-symbol-files.md)

 

 





