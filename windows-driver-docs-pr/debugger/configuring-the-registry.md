---
title: 配置注册表
description: 配置注册表
ms.assetid: 69a1dd39-c4aa-491d-9e28-fd1661ec9a7a
keywords:
- SymProxy，注册表
- ProxyCfg 和 SymProxy
- Netsh 和 SymProxy
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5453a38b46b66b1654375ccf69079e32d79f9d3e
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557768"
---
# <a name="configuring-the-registry"></a>配置注册表


SymProxy 将其设置存储在此注册表项中。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

此注册表项控制要从中查找要在网站中存储的符号的位置、日志记录级别以及 SymProxy 是否使用到网络的直接连接进行操作。 可以通过运行随 Windows 调试工具提供的 SymProxy 注册工具（Symproxy）来创建此密钥。 在命令提示符处键入**symproxy** ，或在 Windows 资源管理器中双击它。

这会为将以 "x" 为前缀的设置添加一些条目，以使其处于禁用状态。 若要启用设置，请删除所需设置前面的 "x"。

```reg
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy]
"Available Settings"="Remove the 'x' prefix to use the setting"
"xMissAgeTimeout"=dword:00015180
"xMissAgeCheck"=dword:00000e10
"xMissTimeout"=dword:00000e10
"xNoCache"=dword:00000001
"xNoFilePointers"=dword:00000001
"xNoInternetProxy"=dword:00000001
"xNoLongerIndexedAuthoritive"=dword:00000001
"xNoUncompress"=dword:00000001
"xRequestTimeout"=dword:0000019
"xRetryAppHang"=dword:0000002
"xUriFilter"=dword:00000FF
"xUriTiers"=dword:0000001
```

Symproxy 注册表文件使用符号的虚拟目录名称，并将符号路径配置为使用 Microsoft 公共符号服务器。

```reg
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories]

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories\Symbols]
"SymbolPath"="https://msdl.microsoft.com/download/symbols"
```

在本主题的 "事件日志" 部分中介绍了 symproxy 中的事件日志记录条目。

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

本主题中讨论了 symproxy 中的 web 目录条目。

### <a name="span-idweb_directoriesspanspan-idweb_directoriesspanweb-directories"></a><span id="web_directories"></span><span id="WEB_DIRECTORIES"></span>Web 目录

对于在 IIS 中生成的、用作符号存储区的每个虚拟目录，你必须在以下注册表项的**Web 目录**子项下面设置一个注册表项。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

**编辑符号存储区虚拟目录的注册表项**

-   编辑**SymbolPath**的内容，使其包含 SymProxy 符号存储区使用的所有符号存储区。 如果正在使用多个符号存储区，请使用分号分隔它们。 每个值最多支持10个存储区。 HTTP 路径必须包含**https://前缀**，并且 UNC 路径必须包含 **\\\\** 前缀。

例如，如果其中一个虚拟目录称为符号，并且它访问的符号存储位于 UNC 存储区 \\ \\ 符号 \\ 符号和 HTTP 存储区 https://msdl.microsoft.com/download/symbols 中，请创建以下注册表项。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy/Web Directories/Symbols
```

创建此密钥后，请将其**SymbolPath**编辑为 \\ \\ 符号 \\ 符号; <https://msdl.microsoft.com/download/symbols> 。 可在注册表编辑器的以下屏幕截图中查看。

![显示已修改 symbolpath 的注册表编辑器的屏幕截图](images/symproxy-registry.png)

在此示例中，SymProxy 首先搜索符号符号中的符号 \\ \\ \\ 。 如果在此处找不到文件，将使用 Microsoft 符号存储区。

-   在与虚拟目录名称匹配的 Web 目录下的每个项中， \_ 需要创建一个名为 SymbolPath 的 REG SZ。 值包含将用于填充 SymProxy 符号存储区的所有上游符号存储区。

-   最多支持10个条目。

-   用分号分隔条目。

-   UNC 路径需要包括 " \\ \\ " 前缀

-   HTTP 路径需要包含 "https://" 前缀

-   将值从最小成本到最昂贵。

    - 你将需要在计算中平衡使用情况性能目标与服务器和数据通信成本。

    - 通常，在 internet HTTP 服务器之前放置本地 SMB/HTTP 服务器。

### <a name="span-idsymproxy_performance_countersspanspan-idsymproxy_performance_countersspanspan-idsymproxy_performance_countersspansymproxy-performance-counters"></a><span id="SymProxy_Performance_Counters"></span><span id="symproxy_performance_counters"></span><span id="SYMPROXY_PERFORMANCE_COUNTERS"></span>SymProxy 性能计数器

SymProxy 可以通过名为 SymProxy 的访问接口发出性能计数器。

若要启用性能计数器支持，请在管理员命令窗口中注册 symproxy 清单文件：

```console
C:\> lodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

若要禁用性能计数器支持，请注销清单：

```console
C:\> unlodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-idsymproxy_event_tracing_for_windowsspanspan-idsymproxy_event_tracing_for_windowsspanspan-idsymproxy_event_tracing_for_windowsspansymproxy-event-tracing-for-windows"></a><span id="SymProxy_Event_Tracing_for_Windows"></span><span id="symproxy_event_tracing_for_windows"></span><span id="SYMPROXY_EVENT_TRACING_FOR_WINDOWS"></span>Windows 的 SymProxy 事件跟踪

SymProxy 可以通过名为 SymProxy 的提供程序创建 ETW 事件。

```console
C:\> logman query providers | findstr SymProxy
Microsoft-Windows-SymProxy {0876099C-A903-47FF-AF14-52035BB479EF}
```

若要启用 ETW 支持，请注册清单文件：

```console
C:\> wevtutil.exe install-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

若要禁用 ETW 支持，请注销清单文件：

```console
C:\> wevtutil.exe uninstall-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-idevent_logspanspan-idevent_logspanspan-idevent_logspanevent-log"></a><span id="Event_Log"></span><span id="event_log"></span><span id="EVENT_LOG"></span>事件日志

如果配置了 ETW，事件会作为事件记录在事件日志*Operational and Analytic*中的 "*应用程序和服务日志" \\ \\ \\ *下的 "运行" 和 "分析" 通道中。

若要正确查看事件日志条目的消息，需要将 symproxy 文件的 "事件日志" 区域添加到注册表中：

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

### <a name="span-idsymproxy_eventsspanspan-idsymproxy_eventsspanspan-idsymproxy_eventsspansymproxy-events"></a><span id="SymProxy_Events"></span><span id="symproxy_events"></span><span id="SYMPROXY_EVENTS"></span>SymProxy 事件

SymProxy 记录以下事件：

| **事件 ID** | **说明**                   | **频道** |
|--------------|-----------------------------------|-------------|
| 1            | ISAPI 筛选器的开头         | 管理员       |
| 2            | 停止 ISAPI 筛选器          | 管理员       |
| 3            | ISAPI 筛选器的配置 | 管理员       |
| 4            | 丢失缓存统计信息             | 管理员       |
| 10           | URL 请求-本地缓存命中     | 可运行 |
| 11           | URL 请求-本地缓存未命中    | 可运行 |
| 20           | 通过 SymSrv 下载符号        | 可运行 |
| 30           | 缺少关键符号           | 管理员       |
| 31           | 缺少关键映像            | 管理员       |
| 40           | SymSrv-找不到路径           | 管理员       |
| 41           | SymSrv-找不到文件           | 管理员       |
| 42           | SymSrv-访问被拒绝            | 管理员       |
| 43           | SymSrv –路径太长            | 管理员       |
| 49           | SymSrv –错误代码               | 管理员       |
| 90           | 锁争用                   | 可运行 |
| 100          | 一般关键消息          | 分析    |
| 101          | 常规错误消息             | 分析    |
| 102          | 一般警告消息           | 分析    |
| 103          | 常规信息性消息     | 分析    |
| 104          | 常规分析消息          | 分析    |
| 105          | 常规调试消息             | 调试       |



### <a name="span-idsymbol_server_proxy_configurationspanspan-idsymbol_server_proxy_configurationspanspan-idsymbol_server_proxy_configurationspansymbol-server-proxy-configuration"></a><span id="Symbol_Server_Proxy_Configuration"></span><span id="symbol_server_proxy_configuration"></span><span id="SYMBOL_SERVER_PROXY_CONFIGURATION"></span>符号服务器代理配置

SymProxy 将其配置设置存储在以下注册表项区域中：

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

SymProxy 从该位置获取其全局设置和上游符号存储区的符号路径。

可以通过在自定义的 symproxy 文件中合并，如前文所述，创建此密钥。

### <a name="span-idsymbol_server_proxy__keyspanspan-idsymbol_server_proxy__keyspanspan-idsymbol_server_proxy__keyspansymbol-server-proxy-key"></a><span id="Symbol_Server_Proxy__key"></span><span id="symbol_server_proxy__key"></span><span id="SYMBOL_SERVER_PROXY__KEY"></span>符号服务器代理密钥

符号服务器代理注册表项支持以下全局设置（所有 REG \_ DWORD）。 可以通过回收应用程序池实时应用设置。 将创建一个新的 w3wp.exe 进程，并且它将读取新的值。 完成对旧 w3wp.exe 进程的所有挂起的请求后，旧的 w3wp.exe 进程将结束。 IIS 默认回收每1740分钟（29小时） w3wp.exe 处理。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">REG_DWORD</td>
<td align="left">说明</td>
</tr>
<tr class="odd">
<td align="left">NoInternetProxy</td>
<td align="left"><p>作为服务运行时，SymSrv.dll 使用 WinHTTP 而不是 WinInet 发出 HTTP 请求。 因此，你可能需要设置 HTTP 代理设置，以便该服务可以访问外部网络资源。 可以使用 netsh 程序执行此操作。 键入 "netsh.exe winhttp-？" 有关说明。</p>
<p>默认情况下，SymProxy 使用指定的 HTTP 代理。 如果未配置 HTTP 代理，SymProxy 将使用虚拟代理。 这样就可以安全地访问 intranet 内的 HTTP 站点。 作为副作用，这会阻止 SymProxy 直接连接到不安全站点。</p>
<p>创建 REG_DWORD： "NoInternetProxy" 值会将 SymProxy 配置为在没有代理的情况下运行，从而允许直接连接。</p></td>
</tr>
<tr class="even">
<td align="left">NoFilePointers</td>
<td align="left"><p>默认情况下，对于不存在的符号，SymProxy 将在请求的文件（在本地缓存中）旁查找文件 ptr 文件。 如果找到，它将返回由文件 ptr 文件指定的位置。 仅当 SymStore.exe 填充本地缓存时，此功能才是必需的。</p>
<p>创建 REG_DWORD： "NoFilePointers" 值以跳过查找。</p></td>
</tr>
<tr class="odd">
<td align="left">NoUncompress</td>
<td align="left"><p>默认情况下，SymProxy 将在将文件返回到调用方之前，解压缩下载的符号。 这会减少客户端的 CPU，但会增加 i/o。</p>
<p>创建 REG_DWORD： "NoUncompress" 值以跳过解压缩。</p></td>
</tr>
<tr class="even">
<td align="left">NoCache</td>
<td align="left"><p>默认情况下，SymProxy 会将下载的符号缓存到本地文件系统，该文件由虚拟目录的路径定义。</p>
<p>创建 REG_DWORD： "NoCache" 值以跳过下载并改为向客户端提供文件的远程路径。</p></td>
</tr>
<tr class="odd">
<td align="left">MissTimeout</td>
<td align="left"><p>缺少符号被报告为缺少的超时时间段（以秒为单位），无需重新查询上游符号服务器。</p>
<p>未命中与基于 UTC 的时间相关联。 对该文件的后续请求会被立即拒绝 N 秒。</p>
<p>第一次在 N 秒后对文件进行请求会导致重新查询上游符号存储。</p>
<p>成功后，将返回符号文件并删除未命中。</p>
<p>发生故障时，未命中会向前移动到当前时间（UTC），以启动新的超时时间。</p>
<p>使用 "未命中 <em> 的缓存" 计数器来监视未命中的情况。</p>
<p><ul>
    <li>未指定-（默认值）300秒/5 分钟</li>
    <li>0–功能已禁用</li>
    <li>N –超时持续时间为 N 秒</li>
   </ul>
</td>
</tr>
<tr class="even">
<td align="left">MissAgeCheck</td>
<td align="left"><p>两次未命中期限检查。 将扫描未命中的缓存并删除早于 MissAgeTimeout 秒的记录。</p>
<p>使用事件 ID 4 将当前统计信息保存到事件日志。</p>
<p><ul>
    <li>未指定-（默认值）3600秒/1 小时</li>
    <li>0–功能已禁用</li>
    <li>N –在 N 秒内的两次检查之间</li>
   </ul>
</td>
</tr>
<tr class="odd">
<td align="left"><p>FailureTimeout</p>
<p>FailureCount</p>
<p>FailurePeriod</p>
<p>FailureBlackout</p></td>
<td align="left"><p>使用掉电功能 termporarly 禁用无响应的上游符号存储。 掉电功能使用4个 REG_DWORD 值来定义行为。 默认情况下，该功能处于禁用状态。</p>
<p>对于在符号路径中定义的每个上游符号存储区，会单独记录失败。 如果请求所用时间超过 FailureTimeout （msec），则失败计数将增加。</p>
<p>在 FailurePeriod 秒后，符号路径标记为 "FailureCount"。 此时，所有请求都将被忽略，直到超过 FailureBlackout 秒。 超时后的第一个调用方测试上游符号存储区。 如果成功，将删除超时并允许请求。 如果失败，时间设置为现在 + FailureBlackout 秒。 在此之后，将再次测试上游符号存储区。</p></td>
</tr>
<tr class="even">
<td align="left">MissAgeTimeout</td>
<td align="left"><p>说明待定</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">RequestTimeout</td>
<td align="left"><p>说明待定</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">RetryAppHang</td>
<td align="left"><p>说明待定</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">NoLongerIndexedAuthoritive</td>
<td align="left"><p>说明待定</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">UriFilter</td>
<td align="left"><p>说明待定</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">UriTiers</td>
<td align="left"><p>说明待定</p>
<p></p></td>
</tr>
</tbody>
</table>



### <a name="span-idaccessing_outside_network_resourcesspanspan-idaccessing_outside_network_resourcesspanaccessing-outside-network-resources"></a><span id="accessing_outside_network_resources"></span><span id="ACCESSING_OUTSIDE_NETWORK_RESOURCES"></span>访问外部网络资源

当 SymSrv 与 SymProxy 一起使用时，它作为一项服务运行，并使用 WinHTTP API 通过 HTTP 连接访问符号。 这不同于其通常使用 WinInet 来实现此目的的行为。

因此，你可能需要设置 HTTP 代理设置，以便该服务可以访问外部网络资源。 使用以下方法之一来配置这些设置：

-   使用 Netsh 工具（netsh.exe）。 有关说明，请在命令提示符窗口中键入以下内容：

    ```console
    netsh winhttp -? 
    ```

SymProxy 的默认行为是使用 ProxyCfg 或 Netsh 指定的任何 HTTP 代理。 如果未配置 HTTP 代理，SymProxy 将使用虚拟代理来允许访问 intranet 内的安全 HTTP 站点。 作为副作用，此方法阻止 SymProxy 使用到外部 Internet 的直接连接。 如果希望允许 SymProxy 使用直接连接到 Internet，请 \_ 在注册表的**符号服务器代理**密钥中创建一个名为**NoInternetProxy**的 "REG DWORD" 值。 将**NoInternetProxy**的值设置为1，并验证是否没有 ProxyCfg 指示的 HTTP 代理。

