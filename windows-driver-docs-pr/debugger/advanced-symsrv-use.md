---
title: SymSrv 的高级用法
description: SymSrv 的高级用法
ms.assetid: 16d4dda0-4bcf-4450-9972-e20d71efc845
keywords:
- SymSrv 功能
- 缓存符号
- 符号服务器缓存
- 符号缓存
- 符号服务器，下游应用商店
- 下游应用商店 （符号服务器）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566163bd79334c22c2b094ab08975af1b03b439c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327367"
---
# <a name="advanced-symsrv-use"></a>SymSrv 的高级用法


SymSrv 可以提供集中式的符号存储区中的符号文件。 此存储区可以包含任意数量的符号文件，对应于任意数量的程序或操作系统。 在存储区还可以包含二进制文件 （这是有用的小型转储调试时）。

在存储区可以包含的实际符号和二进制文件，也可以只需包含符号文件的指针。 如果在存储区包含的指针，SymSrv 将直接从其源检索的实际文件。

SymSrv 还用于大型符号存储区划分为一个较小子集适用于专门的调试任务。

最后，SymSrv 可以从使用由操作系统提供的登录信息的 HTTP 或 HTTPS 源获取的符号文件。 SymSrv 支持 HTTPS 站点受智能卡、 证书和正则登录名和密码。 有关详细信息，请参阅[HTTP 符号存储区](http-symbol-stores.md)。

### <a name="span-idsettingthesymbolpathspanspan-idsettingthesymbolpathspansetting-the-symbol-path"></a><span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>设置符号路径

若要使用此符号服务器，必须在调试器所在的同一目录中安装 symsrv.dll。 可以设置符号路径，如下所示：

```console
set _NT_SYMBOL_PATH = symsrv*ServerDLL*DownstreamStore*\\Server\Share 

set _NT_SYMBOL_PATH = symsrv*ServerDLL*\\Server\Share 

set _NT_SYMBOL_PATH = srv*DownstreamStore*\\Server\Share 

set _NT_SYMBOL_PATH = srv*\\Server\Share 
```

此语法的各个部分介绍了，如下所示：

<span id="________symsrv"></span><span id="________SYMSRV"></span> **symsrv**  
此关键字始终显示第一个。 它指示调试器，此项是符号服务器，而不仅仅是一个普通符号目录。

<span id="ServerDLL"></span><span id="serverdll"></span><span id="SERVERDLL"></span>*ServerDLL*  
指定符号服务器 DLL 的名称。 如果使用 SymSrv 符号服务器，此属性始终为 symsrv.dll。

<span id="srv"></span><span id="SRV"></span>**srv**  
这是速记**symsrv\*symsrv.dll**。

<span id="DownstreamStore"></span><span id="downstreamstore"></span><span id="DOWNSTREAMSTORE"></span>*DownstreamStore*  
指定下游存储区。 这是将用于缓存单独的符号文件的本地目录或网络共享。

您可以指定多个下游存储区，分隔星号。 中介绍了多个下游存储**级联 Downstream 存储**进一步在此页上。

如果在其中将通常指定下游存储区的行中包含两个星号，则使用默认的下游存储。 此存储区将位于主目录的符号子目录中。 主目录将默认为调试器安装目录;这可以通过更改[ **！ homedir** ](-homedir.md)扩展或通过设置 DBGHELP\_主目录环境变量。

如果*DownstreamStore*指定的目录不存在，SymStore 将尝试创建它。

如果*DownstreamStore*省略参数且不额外星号包含-换而言之，如果您使用**srv**有一个星号或**symsrv**使用正好两个将创建星号-然后下游的存储。 调试器将直接在服务器上，而无需本地缓存加载所有符号文件。

**请注意**  如果要从 HTTP 或 HTTPS 站点，访问符号或符号存储区使用压缩的文件，如果始终使用下游应用商店。 如果不指定任何下游存储，则将主目录的符号子目录中创建一个。

 

<span id="__Server_Share"></span><span id="__server_share"></span><span id="__SERVER_SHARE"></span>*\\\\服务器\\共享*  
指定的服务器和共享的远程符号存储区。

如果使用的下游存储，则此存储区中的符号文件将首先查找调试器。 如果未找到符号文件，调试器将查找从指定符号文件*服务器*并*共享*，然后缓存下游存储区中此文件的副本。 该文件将复制到下的树中的子目录*DownstreamStore*到树中的下其位置对应 *\\ \\Server\\共享*。

符号服务器没有为符号路径中的唯一项。 如果符号路径由多个条目，调试器会检查所需的符号文件，按顺序 （从左到右），而不考虑符号服务器或实际目录是否为每个条目。

下面是一些示例。 用于 SymSrv 与符号存储区使用符号服务器上\\ \\mybuilds\\mysymbols，设置以下的符号路径：

```console
set _NT_SYMBOL_PATH= symsrv*symsrv.dll*\\mybuilds\mysymbols
```

若要设置符号路径，以便调试器会将符号从符号存储区的文件复制上\\ \\mybuilds\\到本地目录 c: mysymbols\\localsymbols，使用：

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*c:\localsymbols*\\mybuilds\mysymbols
```

若要设置符号路径，以便调试器将符号文件从 HTTP 站点 www.company.com/manysymbols 复制到本地网络目录\\\\本地服务器\\myshare\\mycache，使用：

```console
set _NT_SYMBOL_PATH=symsrv*symsrv.dll*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

此外可以这种情况下缩短此最后一个示例：

```console
set _NT_SYMBOL_PATH=srv*\\localserver\myshare\mycache*https://www.company.com/manysymbols
```

此外，符号路径可以包含多个目录或符号服务器，之间用分号分隔。 这样即可找到多个位置 （或甚至多个符号服务器） 中的符号。 如果二进制文件具有不匹配的符号文件，调试器无法找到它使用符号服务器，因为它只检查确切的参数。 但是，调试器可能会找到具有正确名称的不匹配的符号文件使用传统的符号路径，并成功加载。 即使将文件从技术上讲不是正确的符号文件，它可能提供有用的信息。

### <a name="span-idcompressedfilesspanspan-idcompressedfilesspancompressed-files"></a><span id="compressed_files"></span><span id="COMPRESSED_FILES"></span>压缩的文件

SymSrv 是包括压缩的文件的符号存储区与兼容，只要此压缩已完成，但 compress.exe 工具，可用它[此处](https://go.microsoft.com/fwlink/p/?linkid=239917)。 压缩的文件应具有其文件扩展名中的最后一个字符与下划线 (例如，module1.pd\_或 module2.db\_)。 有关详细信息，请参阅[SymStore](symstore.md)。

如果在存储上的文件被压缩，则必须使用下游应用商店。 SymSrv 将解压缩之前缓存在下游应用商店上的所有文件。

### <a name="span-iddeletingthecachespanspan-iddeletingthecachespandeleting-the-cache"></a><span id="deleting_the_cache"></span><span id="DELETING_THE_CACHE"></span>删除缓存

如果使用的*DownstreamStore*为缓存，您可以在任何时间以节省磁盘空间删除此目录。

很可能有大量符号存储区，其中包含适用于许多不同的程序或 Windows 版本的符号文件。 如果您的目标计算机上使用的 Windows 版本升级时，缓存的符号文件将所有的早期版本匹配。 这些缓存的文件不会的任何进一步使用，因此这可能会删除缓存的好时机。

### <a name="span-idcascadingdownstreamstoresspanspan-idcascadingdownstreamstoresspancascading-downstream-stores"></a><span id="cascading_downstream_stores"></span><span id="CASCADING_DOWNSTREAM_STORES"></span>级联下游存储

可以指定任意数量的下游存储，分隔星号。 这些存储区被称为*级联符号存储区*。

首字母后**srv\\*** 或**symsrv\\**<strong>ServerDLL</strong>*\** *、 每个后续令牌表示符号位置。 首先检查最大程度地保留的令牌。 -通过在行中，两个星号或字符串末尾的星号指示-的空令牌表示默认下游存储区。

下面是使用两个下游存储来保存从主符号存储区正在访问的信息的符号路径的示例。 主存储、 中等级别存储事件和本地缓存可以进行调用：

```console
srv*c:\localcache*\\interim\store*https://msdl.microsoft.com/download/symbols
```

在此方案中，SymSrv，将首先查找 c： 驱动器中\\localcache 符号文件。 如果它找到存在，则它将返回到它的路径。 如果它找到不存在，它将查找\\\\临时\\存储。 如果在其中找到符号文件，SymSrv 会将其复制到 c:\\localcache 和返回的路径。 如果它找到不存在，将查看 SymSrv [Microsoft 公共符号存储区](microsoft-public-symbols.md)处<https://msdl.microsoft.com/download/symbols>; 如果找到该文件存在，SymSrv 会将其复制到这两\\\\临时\\应用商店和 c:\\localcache。

通过使用以下路径将获得类似的行为：

```console
srv**\\interim\store*https://internetsite
```

在这种情况下，本地缓存是默认下游存储以及主存储是 internet 站点。 中等级别的存储区\\\\临时\\之间另外两个用于指定应用商店。

当 SymSrv 处理包含级联存储的路径时，它将跳过它无法读取或写入任何存储。 因此如果一个共享位置出现故障，它将文件复制到下游的存储从缺少存储未出现任何错误。 此错误的一个很好的副作用是用户可以指定多个馈送的下游存储单个流，只要主存储不是可写的主存储。

当从主存储中检索压缩的符号文件时，它将存储在任何中等级别存储区中的压缩形式。 在路径中的最底层存储中，将未压缩文件。

### <a name="span-idworkingwithhttpandsmbsymbolserverpathsspanspan-idworkingwithhttpandsmbsymbolserverpathsspanspan-idworkingwithhttpandsmbsymbolserverpathsspanworking-with-http-and-smb-symbol-server-paths"></a><span id="Working_With_HTTP_and_SMB__Symbol_Server_Paths"></span><span id="working_with_http_and_smb__symbol_server_paths"></span><span id="WORKING_WITH_HTTP_AND_SMB__SYMBOL_SERVER_PATHS"></span>使用 HTTP 和 SMB 符号服务器路径

如先前所论述的链接 （），或级联是指发生之间每个副本"\*"符号路径中的分隔符。 按从左到右顺序中搜索符号。 每个未命中，在下一步 （上游） 符号服务器将查询，直到找到该文件。

如果找到，该文件从 （上游） 符号服务器复制到以前的 （下游） 符号服务器。 对于每个 （下游） 符号服务器都会重复此操作。 这种方式，（共享） 的下游符号服务器中填充了所有客户端使用的符号服务器的集体努力。

即使链接的 UNC 路径可以使用没有 SRV\*前缀，我们建议该 SRV\*指定，以便使用 symsrv.dll 高级的错误处理。

只有一个时的路径中包括 HTTP 符号服务器，可以指定 （每个链），且必须在路径的末尾 （因为它无法写入缓存作为）。 如果基于 HTTP 的符号存储区位于中间或左侧的存储列表中，它就不可能将找到的任何文件复制到它，并链可能会遭到破坏。 此外，因为符号处理程序无法从网站上打开文件，基于 HTTP 的应用商店不应最左侧或列表上只存储。 如果 SymSrv 会不断看到此符号路径，它将尝试通过将文件复制到默认下游存储恢复并从那里，而不考虑默认下游存储是否示符号路径打开它。

使用 SRV 时仅支持 HTTP\*前缀 （由 symsrv.dll 符号处理程序实现）。

**示例 HTTP 和 SMB 共享符号服务器方案**

常见的仅限 UNC 的部署涉及到中央办公室承载的所有文件 (\\\\MainOffice\\符号)、 分支机构缓存子集 (\\\\BranchOfficeA\\符号)，和桌面 (c:\\符号) 缓存它们引用的文件。

```console
srv*C:\Symbols*\\BranchOfficeA\Symbols*\\MainOffice\Symbols
```

当 SMB 共享主 （上游） 符号存储区时，读取是必需的。

```console
srv*C:\Symbols*\\MachineName\Symbols
```

当 SMB 共享的中间 （下游） 符号存储区时，读取/更改是必需的。 客户端会将文件复制到 SMB 共享中，主符号存储区中，然后从本地文件夹的 SMB 共享。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://msdl.microsoft.com/download/symbols
srv*C:\Symbols*\\MachineName\Symbols*\\MainOffice\Symbols
```

当 SMB 共享中 SymProxy 部署中间 （下游） 符号存储区时，仅读取是必需的。 SymProxy ISAPI 筛选器将执行的写入，而不是客户端。

```console
srv*C:\Symbols*\\MachineName\Symbols*https://SymProxyName/Symbols
```

**多个 HTTP 和 SMB 共享符号服务器缓存方案**

可以指定多个链的符号服务器和缓存位置，由一个分号分隔";"。 如果符号位于第一个链中，第二个链不按照顺序遍历。 如果符号不位于第一个链，将遍历的第二个链，并且如果符号位于第二个链中，它们将缓存在指定的位置。 此方法将允许主符号服务器可正常情况下，与辅助服务器仅使用，如果符号不能指定第一个链中的主符号服务器上。

```console
srv*C:\Symbols*\\Machine1\Symbols*https://SymProxyName/Symbols;srv*C:\WebSymbols* https://msdl.microsoft.com/download/symbols
```

### <a name="span-idcachelocalsymbolcachespanspan-idcachelocalsymbolcachespancachelocalsymbolcache"></a><span id="cache_localsymbolcache"></span><span id="CACHE_LOCALSYMBOLCACHE"></span>cache\**localsymbolcache*

若要创建符号的本地缓存的另一种方法是使用**缓存\\**<em>* localsymbolcache</em>符号路径中的字符串。 这不是符号服务器元素，但符号路径中的单独元素的一部分。 调试器将使用指定的目录*localsymbolcache*存储在符号路径中此字符串的右侧会显示任何元素中加载任何符号。 这样，您可以从任何位置下载的符号，而不仅仅是那些由符号服务器下载使用本地缓存。

例如，以下的符号路径不会缓存符号摘自 *\\ \\someshare*。 它将使用 c:\\取自下缓存符号的 mysymbols  *\\ \\anothershare*，因为元素开头 *\\ \\anothershare*出现的右侧**缓存\*c:\\mysymbols**元素。 它还将使用 c:\\mysymbols 到来自 Microsoft 公共符号存储区，由于使用符号服务器的常规语法下缓存符号 (**srv**带两个或多个星号)。 此外，如果您随后使用[ **.sympath +** ](-sympath--set-symbol-path-.md)命令向此路径添加其他位置，这些新元素还将缓存，因为它们将追加到路径的右侧。

```console
_NT_SYMBOL_PATH=\\someshare\that\cachestar\ignores;srv*c:\mysymbols*https://msdl.microsoft.com/download/symbols;cache*c:\mysymbols;\\anothershare\that\gets\cached
```

### <a name="span-idhowsymsrvlocatesfilesspanspan-idhowsymsrvlocatesfilesspanhow-symsrv-locates-files"></a><span id="how_symsrv_locates_files"></span><span id="HOW_SYMSRV_LOCATES_FILES"></span>如何 SymSrv 查找文件

SymSrv 创建所需的符号文件的完全限定的 UNC 路径。 此路径开头的记录在符号存储区路径\_NT\_符号\_PATH 环境变量。 **SymbolServer**例程然后用于标识所需的文件的名称; 此名称追加到作为目录名称的路径。 另一个目录名称，包含的串联*id*，*两个*，并*三个*参数传递给**SymbolServer**，是然后，将追加。 如果任何这些值为零，将省略它们。

生成目录中搜索的符号文件或符号存储区的指针文件。

如果成功，此搜索**SymbolServer**将路径传递给调用方，并返回**TRUE**。 如果找不到该文件， **SymbolServer**返回**FALSE**。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

若要删除早于指定日期的缓存的文件或减少指定的大小如下缓存的内容，可以使用 AgeStore 工具。 这很有用，如果你的下游存储太大。 有关详细信息，请参阅[AgeStore](agestore.md)。

 

 





