---
title: SymProxy
description: SymProxy
ms.assetid: c0b122fe-4996-4659-a3f1-95831605c0b3
keywords:
- 符号，SymProxy (symproxy.dll)
- 符号存储区 HTTP
- 符号存储区，SymProxy (symproxy.dll)
- SymProxy
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca844e346e047ff43cc5bf4b79e28357a0bc933
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567179"
---
# <a name="symproxy"></a>SymProxy


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


你可以配置你的基于 HTTP 的符号存储区，使其作为客户端计算机和其他符号存储区之间的代理。 实现是通过名为 SymProxy (Symproxy.dll) Internet 服务器应用程序编程接口 (ISAPI) 筛选器。 SymProxy 服务器可以用作到 Internet 或公司网络中的其他源的网关计算机。 下图显示了一个示例 SymProxy 配置。

![示例 symproxy 配置示意图](images/symproxy-configuration.png)

SymProxy 是在许多情况下很有用。 例如：

-   在调试中的计算机未附加到公司网络中，在实验室环境中的许多系统，但符号存储在网络中，必须使用集成 Windows 身份验证 (IWA) 进行访问。

-   企业计算环境包括一个从正在调试的计算机将禁止对 Internet 访问的防火墙，您必须从 internet 网站获取的符号。

-   你想要在你的公司提供单一符号路径为所有用户，以便它们不需要知道或在意符号的位置，并可以添加新符号存储区，而无需用户干预。

-   您有远的公司资源，其余部分在物理上是一个远程站点和网络访问速度较慢。 此系统可用于获取符号和缓存到远程站点。

若要安装 SymProxy，您必须手动将文件复制到正确的位置、 配置注册表、 选择网络安全凭据和配置 Internet 信息服务 (IIS)。 若要确保已正确配置 HTTP 符号存储区，请参阅[HTTP 符号存储区](http-symbol-stores.md)。

### <a name="span-idmultiplesymbolserverperformanceconsiderationsspanspan-idmultiplesymbolserverperformanceconsiderationsspanspan-idmultiplesymbolserverperformanceconsiderationsspanmultiple-symbol-server-performance-considerations"></a><span id="Multiple_Symbol_Server_Performance_Considerations"></span><span id="multiple_symbol_server_performance_considerations"></span><span id="MULTIPLE_SYMBOL_SERVER_PERFORMANCE_CONSIDERATIONS"></span>多个符号服务器性能注意事项

每个虚拟目录可与多个 （上游） 符号存储区相关联。 单独查询每个符号存储区。 为性能，应在 internet HTTP 服务器之前处理本地 SMB 服务器。 与不同的调试器符号路径，可以 SymProxy 符号路径中指定多个 HTTP 符号存储区。 每个虚拟目录支持最多 10 个条目。

### <a name="span-idsymproxysymbolpathspanspan-idsymproxysymbolpathspanspan-idsymproxysymbolpathspansymproxy-symbol-path"></a><span id="SymProxy_Symbol_Path"></span><span id="symproxy_symbol_path"></span><span id="SYMPROXY_SYMBOL_PATH"></span>SymProxy 符号路径

SymProxy 拆分 （注册表中定义） 符号路径值中对各项，并使用每个条目生成 SRV\*基于符号路径检索文件。 它使用合并到单个下游符号存储区中的上游存储在每个查询的 – 实际上，下游存储的虚拟目录的文件夹。

（生成） 的符号路径由 SymProxy 等效于此：

```dbgcmd
SRV*<Virtual Directory Folder>*<SymbolPath Entry #N>
```

在此示例中，UNC 路径和两个 HTTP 路径是虚拟目录以合并来自公司的符号服务器、 Microsoft 和第三方 (Contoso) 的符号与相关联。 SymProxy SymbolPath 将设置如下：

```console
\\MainOffice\Symbols;https://msdl.microsoft.com/download/symbols;
https://symbols.contoso.com/symbols
```

第一种使用 （生成） 的符号路径的查询 Main Office 符号文件共享：

```dbgcmd
SRV*D:\SymStore\Symbols*\\MainOffice\Symbols
```

如果未找到符号文件，使用 （生成） 的符号路径的查询 Microsoft 符号存储区：

```dbgcmd
SRV*D:\SymStore\Symbols*https://msdl.microsoft.com/download/symbols
```

如果该文件仍未找到，Contoso 符号存储区 (https://symbols.contoso.com/symbols)使用 （生成） 的符号路径的查询：

```dbgcmd
SRV*D:\SymStore\Symbols*https://symbols.contoso.com/symbols
```

本部分包括：

[安装 SymProxy](installing-symproxy.md)

[配置注册表](configuring-the-registry.md)

[选择网络安全凭据](choosing-network-security-credentials.md)

[为 SymProxy 配置 IIS](configuring-iis-for-symproxy.md)

[设置排除列表](setting-up-exclusion-lists.md)

[处理不可用的符号存储区](dealing-with-unavailable-symbol-stores.md)

[处理文件指针](handling-file-pointers.md)

[缓存获取的符号文件](caching-acquired-symbol-files.md)

 

 





