---
title: SymSrv 的高级用法
description: SymSrv 的高级用法
ms.assetid: 16d4dda0-4bcf-4450-9972-e20d71efc845
keywords:
- SymSrv，功能
- 缓存符号
- 符号服务器，缓存
- 符号，缓存
- 符号服务器，下游存储
- 下游存储（符号服务器）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 698135f29b8db0db31452578dd1d53618e7b9b86
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402300"
---
# <a name="advanced-symsrv-use"></a>SymSrv 的高级用法

SymSrv 可以传递集中符号存储区中的符号文件。 此存储可以包含任意数量的符号文件，它们对应于任意数量的程序或操作系统。 存储还可以包含二进制文件（这在调试小型转储时非常有用）。

存储区可以包含实际的符号和二进制文件，也可以只包含指向符号文件的指针。 如果存储区包含指针，SymSrv 将直接从源检索实际文件。

SymSrv 还可用于将大符号存储区分隔为适用于专用调试任务的更小的子集。

最后，SymSrv 可以使用操作系统提供的登录信息从 HTTP 或 HTTPS 源获取符号文件。 SymSrv 支持通过智能卡、证书和常规登录名和密码保护的 HTTPS 站点。 有关详细信息，请参阅[HTTP 符号存储](http-symbol-stores.md)。

### <a name="span-idsetting_the_symbol_pathspanspan-idsetting_the_symbol_pathspansetting-the-symbol-path"></a><span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>设置符号路径

若要使用此符号服务器，symsrv.dll 必须与调试器安装在同一个目录中。 可以设置符号路径，如以下代码所示：

```console
set _NT_SYMBOL_PATH = symsrv*ServerDLL*DownstreamStore*\\Server\Share

set _NT_SYMBOL_PATH = symsrv*ServerDLL*\\Server\Share

set _NT_SYMBOL_PATH = srv*DownstreamStore*\\Server\Share

set _NT_SYMBOL_PATH = srv*\\Server\Share
```

本语法的组成部分如下所述：

<span id="________symsrv"></span><span id="________SYMSRV"></span>**symsrv**  
此关键字必须始终出现在第一位。 它向调试器指示此项是符号服务器，而不只是普通符号目录。

<span id="ServerDLL"></span><span id="serverdll"></span><span id="SERVERDLL"></span>*ServerDLL*  
指定符号服务器 DLL 的名称。 如果使用的是 SymSrv 符号服务器，将始终 symsrv.dll。

<span id="srv"></span><span id="SRV"></span>**srv**  
这是**symsrv \*symsrv.dll**的简写形式。

<span id="DownstreamStore"></span><span id="downstreamstore"></span><span id="DOWNSTREAMSTORE"></span>*DownstreamStore*  
指定下游存储区。 这是将用于缓存各个符号文件的本地目录或网络共享。

可以指定多个下游存储，用星号隔开。 此页面进一步向下**层叠**了多个下游存储。

如果在通常指定下游存储的行中包括两个星号，则使用默认的下游存储。 此存储将位于主目录的符号子目录中。 主目录默认为调试器安装目录;可以通过使用[**！ homedir**](-homedir.md)扩展或通过设置 dbghelp.dll homedir 环境变量来更改此设置 \_ 。

如果*DownstreamStore*指定的目录不存在，则 SymStore 将尝试创建它。

如果省略*DownstreamStore*参数，并且不包含额外的星号（换言之，如果你使用只带有两个星号的一个星号或**symsrv** ）的**srv** ，则不会创建下游存储。 调试器将直接从服务器加载所有符号文件，而无需在本地对其进行缓存。

**注意**   如果要从 HTTP 或 HTTPS 站点访问符号，或者符号存储区使用压缩文件，则始终使用下游存储。 如果未指定下游存储，将在主目录的符号子目录中创建一个。

 

<span id="__Server_Share"></span><span id="__server_share"></span><span id="__SERVER_SHARE"></span>*\\\\服务器 \\ 共享*  
指定远程符号存储的服务器和共享。

如果使用下游存储，则调试器将首先查找此存储中的符号文件。 如果未找到符号文件，则调试器将从指定的*服务器*中查找符号文件并*共享*，然后在下游存储中缓存此文件的副本。 文件将被复制到*DownstreamStore*下的树中的子目录，该子目录与其在* \\ \\ 服务器 \\ 共享*下的树中的位置相对应。

符号服务器不一定是符号路径中的唯一条目。 如果符号路径包含多个条目，则调试器将按顺序（从左到右）检查所需符号文件的每个条目，而不考虑符号服务器或实际目录是否已命名。

下面是一些示例。 若要将 SymSrv 用作 mybuilds mysymbols 上的符号存储区中的符号服务器 \\ \\ \\ ，请设置以下符号路径：

```console
set _NT_SYMBOL_PATH= symsrv*symsrv.dll*\\mybuilds\mysymbols
```

若要设置符号路径，以便调试器将符号文件从 mybuilds mysymbols 上的符号存储复制 \\ \\ \\ 到本地目录 c： \\ localsymbols，请使用：

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*c:\localsymbols*\\mybuilds\mysymbols
```

若要设置符号路径，以便调试器将符号文件从 HTTPS 站点复制 `https://www.company.com/manysymbols` 到本地网络目录 \\ \\ localserver \\ myshare \\ mycache，请使用：

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

最后一个示例也可以按如下方式缩短：

```console
set _NT_SYMBOL_PATH=srv*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

此外，符号路径可能包含多个以分号分隔的目录或符号服务器。 这允许您从多个位置（甚至多个符号服务器）查找符号。 如果某个二进制文件包含不匹配的符号文件，则调试器无法使用符号服务器找到该文件，因为它仅检查确切的参数。 但是，调试器可能会找到一个名称不匹配的符号文件，使用传统的符号路径并成功加载它。 尽管该文件在技术上不是正确的符号文件，但它可能会提供有用的信息。

### <a name="span-idcompressed_filesspanspan-idcompressed_filesspancompressed-files"></a><span id="compressed_files"></span><span id="COMPRESSED_FILES"></span>压缩文件

SymSrv 与包含压缩文件的符号存储区兼容，前提是已使用 compress.exe 工具（可从[Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=17657)获取）完成此压缩。 压缩的文件应将一个下划线作为其文件扩展名中的最后一个字符（例如，module1 \_ 或 module2 \_ ）。 有关详细信息，请参阅[SymStore](symstore.md)。

如果存储中的文件已压缩，则必须使用下游存储。 SymSrv 会在将所有文件缓存到下游存储之前对其进行解压缩。

### <a name="span-iddeleting_the_cachespanspan-iddeleting_the_cachespandeleting-the-cache"></a><span id="deleting_the_cache"></span><span id="DELETING_THE_CACHE"></span>删除缓存

如果使用*DownstreamStore*作为缓存，则可以随时删除此目录，以节省磁盘空间。

可能有一个包含许多不同程序或 Windows 版本的符号文件的大型符号存储区。 如果升级目标计算机上使用的 Windows 版本，则缓存的符号文件将全部与早期版本相匹配。 这些缓存的文件不会进一步使用，因此，这可能是删除缓存的好时机。

### <a name="span-idcascading_downstream_storesspanspan-idcascading_downstream_storesspancascading-downstream-stores"></a><span id="cascading_downstream_stores"></span><span id="CASCADING_DOWNSTREAM_STORES"></span>级联下游存储

可以指定任意数量的下游存储，用星号隔开。 这些存储称为*级联符号存储区*。

在初始**srv \\ *** 或**symsrv \\ **<strong>ServerDLL</strong> * \* * * 之后，每个后续标记表示一个符号位置。 首先检查最远的令牌。 空标记（由行中的两个星号指示）或字符串末尾的星号表示默认的下游存储区。

下面是一个符号路径示例，它使用两个下游存储来保存所访问的主符号存储区中的信息。 这可能称为 "主存储"、"中间级别存储" 和 "本地缓存"：

```console
srv*c:\localcache*\\interim\store*https://msdl.microsoft.com/download/symbols
```

在这种情况下，SymSrv 将首先查看 c： localcache 中的 \\ 符号文件。 如果找到该路径，它将返回它的路径。 如果在此处找不到它，则会在 \\ \\ 过渡 \\ 存储中查找。 如果在此处找到符号文件，则 SymSrv 会将其复制到 c： \\ localcache 并返回路径。 如果在此处找不到该文件，SymSrv 将在[Microsoft 公共符号存储区](microsoft-public-symbols.md)中查找 <https://msdl.microsoft.com/download/symbols> ; 如果在该文件中找到该文件，则 SymSrv 会将其复制到 \\ \\ 过渡 \\ 存储和 c： \\ localcache。

将使用以下路径获取类似行为：

```console
srv**\\interim\store*https://internetsite
```

在这种情况下，本地缓存是默认的下游存储，而主存储是 internet 站点。 \\ \\ \\ 已指定在另两个中间存储中使用中间存储。

当 SymSrv 处理包含级联存储区的路径时，它将跳过它无法读取或写入的任何存储。 因此，如果某个共享发生故障，它会将该文件从缺少的存储中复制到下游，而不会出现任何错误。 此错误的一个不错的副作用是，只要主存储不可写，用户就可以指定一个多个主存储流，以馈送单个下游存储流。

从主存储中检索压缩符号文件时，该文件将以压缩形式存储在任何中间级存储区中。 文件将在路径中的最底层存储中解压缩。

### <a name="span-idworking_with_http_and_smb__symbol_server_pathsspanspan-idworking_with_http_and_smb__symbol_server_pathsspanspan-idworking_with_http_and_smb__symbol_server_pathsspanworking-with-http-and-smb-symbol-server-paths"></a><span id="Working_With_HTTP_and_SMB__Symbol_Server_Paths"></span><span id="working_with_http_and_smb__symbol_server_paths"></span><span id="WORKING_WITH_HTTP_AND_SMB__SYMBOL_SERVER_PATHS"></span>使用 HTTP 和 SMB 符号服务器路径

如前文所述，链接（或级联）指的是符号路径中每个 "" 分隔符之间发生的副本 \* 。 按照从左到右的顺序搜索符号。 每个未命中时，将查询下一个（上游）符号服务器，直到找到该文件。

如果找到该文件，则会将该文件从（上游）符号服务器复制到以前的（下游）符号服务器。 这对于每个（下游）符号服务器都是重复的。 这样，使用符号服务器的所有客户端的总体工作就会填充（共享）下游符号服务器。

尽管可以在没有 SRV 前缀的情况下使用链式 UNC 路径 \* ，但建议 \* 指定 SRV 以便使用 symsrv.dll 的高级错误处理。

如果路径中包含 HTTP 符号服务器，则只能指定一个（每个链），并且它必须位于路径的末尾（因为它不能作为缓存来编写）。 如果基于 HTTP 的符号存储区位于商店列表的中间或左侧，则不能将找到的任何文件复制到该位置，并且链将断开。 此外，由于符号处理程序无法从网站打开文件，因此，基于 HTTP 的存储区不应在列表中最左端或仅存储。 如果 SymSrv 曾经出现过此符号路径，则它将尝试通过将文件复制到默认的下游存储并将其打开来进行恢复，而不管是否在符号路径中指示默认的下游存储区。

仅当使用 SRV \* 前缀（由 symsrv.dll 符号处理程序实现）时，才支持 HTTP。

**示例 HTTP 和 SMB 共享符号服务器方案**

仅限仅限 UNC 的部署涉及承载所有文件（ \\ \\ MainOffice 符号）的中央办事处 \\ ，分支机构缓存子集（ \\ \\ BranchOfficeA \\ 符号），桌面（C： \\ 符号）缓存它们引用的文件。

```console
srv*C:\Symbols*\\BranchOfficeA\Symbols*\\MainOffice\Symbols
```

如果 SMB 共享是主（上游）符号存储区，则需要读取。

```console
srv*C:\Symbols*\\MachineName\Symbols
```

如果 SMB 共享是中间（下游）符号存储区，则需要进行读取/更改。 客户端会将该文件从主符号存储区复制到 SMB 共享，然后从 SMB 共享复制到本地文件夹。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://msdl.microsoft.com/download/symbols
srv*C:\Symbols*\\MachineName\Symbols*\\MainOffice\Symbols
```

当 SMB 共享是 SymProxy 部署中的中间（下游）符号存储时，只需要读取。 SymProxy ISAPI 筛选器将执行写入，而不是客户端。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://SymProxyName/Symbols
```

**多个 HTTP 和 SMB 共享符号服务器缓存方案**

可以指定多个符号服务器和缓存位置的链，并用分号 ";" 分隔。 如果符号位于第一个链中，则不遍历第二个链。 如果符号不位于第一个链中，则将遍历第二个链，并且如果符号位于第二个链中，则它们将缓存在指定位置。 如果在第一个链中指定的主符号服务器上不提供符号，则使用此方法通常可以使用只使用辅助服务器的主要符号服务器。

```console
srv*C:\Symbols*\\Machine1\Symbols*https://SymProxyName/Symbols;srv*C:\WebSymbols* https://msdl.microsoft.com/download/symbols
```

### <a name="span-idcache_localsymbolcachespanspan-idcache_localsymbolcachespancachelocalsymbolcache"></a><span id="cache_localsymbolcache"></span><span id="CACHE_LOCALSYMBOLCACHE"></span>缓存 \* *localsymbolcache*

创建符号的本地缓存的另一种方法是使用符号路径中的** \\ cache**<em>* localsymbolcache</em>字符串。 这不是符号服务器元素的一部分，而是符号路径中单独的元素。 调试器将使用指定的目录*localsymbolcache*来存储从显示在此字符串右侧符号路径中的任何元素加载的任何符号。 这使你可以对从任何位置下载的符号（而不仅仅是符号服务器下载的符号）使用本地缓存。

例如，以下符号路径将不缓存从* \\ \\ someshare*获取的符号。 它将使用 c： \\ mysymbols 缓存从* \\ \\ anothershare*中获取的符号，因为以* \\ \\ anothershare*开头的元素出现在**cache \* c： \\ mysymbols**元素的右侧。 它还将使用 c： \\ mysymbols 缓存来自 Microsoft 公共符号存储区的符号，因为符号服务器使用的是常用语法（具有两个或多个星号的**srv** ）。 此外，如果你随后使用[**. sympath +**](-sympath--set-symbol-path-.md)命令将其他位置添加到此路径，则还将缓存这些新元素，因为它们将追加到路径的右侧。

```console
_NT_SYMBOL_PATH=\\someshare\that\cachestar\ignores;srv*c:\mysymbols*https://msdl.microsoft.com/download/symbols;cache*c:\mysymbols;\\anothershare\that\gets\cached
```

### <a name="span-idhow_symsrv_locates_filesspanspan-idhow_symsrv_locates_filesspanhow-symsrv-locates-files"></a><span id="how_symsrv_locates_files"></span><span id="HOW_SYMSRV_LOCATES_FILES"></span>SymSrv 如何查找文件

SymSrv 创建所需符号文件的完全限定的 UNC 路径。 此路径以指向在 \_ NT \_ 符号 \_ 路径环境变量中记录的符号存储区的路径开头。 然后， **SymbolServer**例程用于标识所需文件的名称;此名称作为目录名称附加到路径。 然后追加另一个目录名称，其中包括*id*的串联、*两个*和*三*个传递给**SymbolServer**的参数。 如果其中任何一个值为零，则忽略它们。

将在生成的目录中搜索符号文件或符号存储指针文件。

如果此搜索成功， **SymbolServer**会将路径传递给调用方并返回**TRUE**。 如果找不到该文件， **SymbolServer**将返回**FALSE**。

### <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

AgeStore 工具可用于删除早于指定日期的缓存文件，或将缓存的内容减小到指定的大小。 如果下游存储太大，这可能很有用。 有关详细信息，请参阅[AgeStore](agestore.md)。

 

 





