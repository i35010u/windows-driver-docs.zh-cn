---
title: 配置注册表
description: 配置注册表
ms.assetid: 69a1dd39-c4aa-491d-9e28-fd1661ec9a7a
keywords:
- SymProxy、 注册表
- ProxyCfg 和 SymProxy
- Netsh 和 SymProxy
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: e47fd16f420e3464a6cc1420aab93b94f8e8534a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375583"
---
# <a name="configuring-the-registry"></a>配置注册表


SymProxy 将其设置存储在此注册表项。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

若要查找的位置符号在 Web 站点、 日志记录级别和 SymProxy 操作具有直接连接到网络中存储此注册表密钥控制。 要创建此密钥，您可以通过运行 SymProxy 注册工具 (Symproxy.reg) 提供有关 Windows 调试工具。 类型**symproxy.reg**在命令提示符下或从 Windows 资源管理器中双击它。

这将添加条目，以便禁用它们将带有"x"前缀的设置。 若要启用的设置，删除前面所需的设置的"x"。

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

Symproxy.reg 注册表文件假定虚拟目录名称的符号，并配置要使用 Microsoft 公共符号服务器的符号路径。

```reg
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories]

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories\Symbols]
"SymbolPath"="https://msdl.microsoft.com/download/symbols"
```

Symproxy.reg 中的事件日志记录条目的本主题的事件日志部分中介绍后一种。

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

本主题中讨论了 symproxy.reg 中的 web 目录条目。

### <a name="span-idwebdirectoriesspanspan-idwebdirectoriesspanweb-directories"></a><span id="web_directories"></span><span id="WEB_DIRECTORIES"></span>Web 目录

每个虚拟目录在 IIS 将用作符号存储区中生成，你必须设置以下注册表项**Web 目录**以下注册表项的子项。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

**若要编辑符号存储区的虚拟目录的注册表项**

-   编辑的内容**SymbolPath**将包含所有 SymProxy 符号存储区使用的符号存储。 如果正在使用的多个符号存储区，请用分号分隔它们。 最多 10 个存储支持的每个值。 HTTP 路径必须包括**https:// 前缀**，并且必须包含 UNC 路径**\\ \\**前缀。

例如，如果其中一个虚拟目录称为符号，它访问符号存储区位于 UNC 应用商店\\\\符号\\符号和 HTTP 存储区 https://msdl.microsoft.com/download/symbols，创建以下注册表键。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy/Web Directories/Symbols
```

创建此密钥后，编辑其**SymbolPath**要\\\\符号\\符号;<https://msdl.microsoft.com/download/symbols>。 这可以看到以下屏幕截图在注册表编辑器中。

![修改后的 symbolpath，注册表编辑器的屏幕截图](images/symproxy-registry.png)

在此示例中，SymProxy 首先搜索中的符号\\\\符号\\符号。 如果那里未找到文件，将使用 Microsoft 符号存储区。

-   在每个匹配的虚拟目录名称，注册的 Web 目录下的项\_SZ 调用 SymbolPath 需要创建。 将用于填充 SymProxy 符号存储区的所有上游符号存储区包含的值。

-   支持最多 10 个条目。

-   用分号分隔的单独条目。

-   UNC 路径需要包括"\\\\"前缀

-   HTTP 路径需要包括"https://"前缀

-   从最便宜到最高的值进行排序。

    - 需要进行权衡与服务器以及在计算中使用的数据通信成本的使用情况性能目标。

    - 一般情况下，将之前的 internet HTTP 服务器的本地 SMB/HTTP 服务器。

### <a name="span-idsymproxyperformancecountersspanspan-idsymproxyperformancecountersspanspan-idsymproxyperformancecountersspansymproxy-performance-counters"></a><span id="SymProxy_Performance_Counters"></span><span id="symproxy_performance_counters"></span><span id="SYMPROXY_PERFORMANCE_COUNTERS"></span>SymProxy 性能计数器

SymProxy 可以发出通过名为 SymProxy 的提供程序的性能计数器。

若要启用性能计数器支持，请在管理员命令窗口中注册 symproxy 清单文件：

```console
C:\> lodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

若要禁用性能计数器支持，取消注册清单：

```console
C:\> unlodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-idsymproxyeventtracingforwindowsspanspan-idsymproxyeventtracingforwindowsspanspan-idsymproxyeventtracingforwindowsspansymproxy-event-tracing-for-windows"></a><span id="SymProxy_Event_Tracing_for_Windows"></span><span id="symproxy_event_tracing_for_windows"></span><span id="SYMPROXY_EVENT_TRACING_FOR_WINDOWS"></span>Windows SymProxy 事件跟踪

SymProxy 可以创建通过名为 Microsoft Windows SymProxy 的提供程序的 ETW 事件。

```console
C:\> logman query providers | findstr SymProxy
Microsoft-Windows-SymProxy {0876099C-A903-47FF-AF14-52035BB479EF}
```

若要启用 ETW 支持，请注册清单的文件：

```console
C:\> wevtutil.exe install-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

若要禁用 ETW 支持，取消注册清单的文件：

```console
C:\> wevtutil.exe uninstall-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-ideventlogspanspan-ideventlogspanspan-ideventlogspanevent-log"></a><span id="Event_Log"></span><span id="event_log"></span><span id="EVENT_LOG"></span>事件日志

如果配置 ETW，作为事件中记录的事件*操作和分析*通道下*应用程序和服务日志\\Microsoft\\Windows\\SymProxy*事件日志中。

若要正确查看事件日志条目的消息，symproxy.reg 文件的事件日志区域必须添加到注册表：

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

### <a name="span-idsymproxyeventsspanspan-idsymproxyeventsspanspan-idsymproxyeventsspansymproxy-events"></a><span id="SymProxy_Events"></span><span id="symproxy_events"></span><span id="SYMPROXY_EVENTS"></span>SymProxy 事件

SymProxy 记录以下事件：

|              |                                   |             |
|--------------|-----------------------------------|-------------|
| **事件 ID** | **说明**                   | **Channel** |
| 1            | ISAPI 筛选器的开头         | 管理员       |
| 2            | ISAPI 筛选器，停止          | 管理员       |
| 3            | ISAPI 筛选器的配置 | 管理员       |
| 4            | 未命中缓存的统计信息             | 管理员       |
| 10           | URL 请求的本地缓存命中     | 操作 |
| 11           | URL 请求的本地缓存未命中    | 操作 |
| 20           | 通过 SymSrv 符号下载        | 操作 |
| 30           | 缺少关键的符号           | 管理员       |
| 31           | 缺少关键的图像            | 管理员       |
| 40           | SymSrv – 找不到路径           | 管理员       |
| 41           | SymSrv – 找不到文件           | 管理员       |
| 42           | SymSrv – 访问被拒绝            | 管理员       |
| 43           | SymSrv – 路径太长            | 管理员       |
| 49           | SymSrv – 错误代码               | 管理员       |
| 90           | 锁争用                   | 操作 |
| 100          | 常规的关键消息          | 分析    |
| 101          | 常规错误消息             | 分析    |
| 102          | 常规警告消息           | 分析    |
| 103          | 常规条信息性消息     | 分析    |
| 104          | 常规分析消息          | 分析    |
| 105          | 常规调试消息             | 调试       |



### <a name="span-idsymbolserverproxyconfigurationspanspan-idsymbolserverproxyconfigurationspanspan-idsymbolserverproxyconfigurationspansymbol-server-proxy-configuration"></a><span id="Symbol_Server_Proxy_Configuration"></span><span id="symbol_server_proxy_configuration"></span><span id="SYMBOL_SERVER_PROXY_CONFIGURATION"></span>符号服务器代理配置

SymProxy 将其配置设置存储在以下注册表关键领域：

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

从该位置，SymProxy 获取其全局设置和上游符号存储区的符号路径。

要创建此密钥，您可以通过合并在 symproxy.reg 文件中自定义前面所述。

### <a name="span-idsymbolserverproxykeyspanspan-idsymbolserverproxykeyspanspan-idsymbolserverproxykeyspansymbol-server-proxy-key"></a><span id="Symbol_Server_Proxy__key"></span><span id="symbol_server_proxy__key"></span><span id="SYMBOL_SERVER_PROXY__KEY"></span>符号服务器代理密钥

符号服务器代理注册表项支持以下全局设置 (所有 REG\_DWORD)。 通过回收应用程序池，可以实时应用设置。 将创建一个新的 w3wp.exe 进程，它会显示新值。 完成到旧的 w3wp.exe 进程的所有挂起的请求后，旧的 w3wp.exe 进程将结束。 默认情况下 IIS 回收 w3wp.exe 进程每隔 1,740 分钟 （29 小时）。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">REG_DWORD</td>
<td align="left">描述</td>
</tr>
<tr class="odd">
<td align="left">NoInternetProxy</td>
<td align="left"><p>作为服务运行时，SymSrv.dll 使用 WinHTTP 而不是 WinInet 发出 HTTP 请求。 因此，您可能需要设置 HTTP 代理设置，以便服务可以访问外部网络资源。 您可以执行此操作使用 netsh 程序。 键入"netsh.exe winhttp-？" 有关说明。</p>
<p>默认情况下，SymProxy 使用指定的 HTTP 代理。 如果没有 HTTP 代理配置，SymProxy 将使用虚拟代理。 这允许对 HTTP 站点在 intranet 中的安全访问。 产生了负面影响，这可以防止 SymProxy 直接连接到不安全站点。</p>
<p>创建 REG_DWORD:"NoInternetProxy"值配置 SymProxy 操作不使用代理，从而允许直接连接。</p></td>
</tr>
<tr class="even">
<td align="left">NoFilePointers</td>
<td align="left"><p>默认情况下，不存在的符号 SymProxy 将查找请求文件 （在本地缓存） 旁边的 file.ptr 文件。 如果找到，它将返回指定 file.ptr 文件的位置。 这种功能是仅由 SymStore.exe 填充本地缓存时所需。</p>
<p>创建 REG_DWORD:"NoFilePointers"要跳过查找的值。</p></td>
</tr>
<tr class="odd">
<td align="left">NoUncompress</td>
<td align="left"><p>默认情况下，SymProxy 将文件返回到调用方之前解压缩下载的符号。 这可在客户端，减少 CPU，但会增加 I/O。</p>
<p>创建 REG_DWORD： 要跳过解压缩的"NoUncompress"值。</p></td>
</tr>
<tr class="even">
<td align="left">NoCache</td>
<td align="left"><p>默认情况下，SymProxy 将缓存下载到本地文件系统，由虚拟目录的路径定义的符号。</p>
<p>创建 REG_DWORD:"NoCache"值以跳过下载并改为提供给客户端的远程文件的路径。</p></td>
</tr>
<tr class="odd">
<td align="left">MissTimeout</td>
<td align="left"><p>超时时间，以秒为单位，为其缺少符号报告为丢失而无需重新查询上游符号服务器。</p>
<p>未命中是与基于 UTC 时间关联。 为 N 秒立即拒绝的文件的后续请求。</p>
<p>后 N 秒使上游符号文件的第一个请求将存储为重新查询。</p>
<p>如果成功，返回的符号文件，并删除未命中。</p>
<p>在失败时，未命中向前移动到当前时间 （采用 UTC) 以启动新的超时时间。</p>
<p>使用"未命中缓存<em>"用于监视未命中数的计数器。</p>
<p>• 未指定-（默认值） 300 秒/5 分钟</p>
<p>• 0 – 功能已禁用</p>
<p>• N – 超时持续时间 N 秒</p></td>
</tr>
<tr class="even">
<td align="left">MissAgeCheck</td>
<td align="left"><p>未命中年龄检查之间的时间段。 扫描未命中缓存并删除早于 MissAgeTimeout 秒的记录。</p>
<p>当前统计信息将保存到事件日志使用事件 ID 4。</p>
<p>• 未指定-（默认值） 3600 秒/1 小时</p>
<p>• 0 – 功能已禁用</p>
<p>• N – 检查在 N 秒之间的段</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FailureTimeout</p>
<p>FailureCount</p>
<p>FailurePeriod</p>
<p>FailureBlackout</p></td>
<td align="left"><p>中断功能使用到 termporarly 禁用上游符号存储没有响应。 中断功能使用 4 个 REG_DWORD 值来定义行为。 默认情况下，禁用该功能。</p>
<p>为每个符号路径中定义的上游符号存储区，分别记录失败。 如果请求花费的时间比 FailureTimeout （毫秒），失败计数将递增。</p>
<p>符号路径 FailurePeriod 秒 FailureCount 失败后标记为不活动。 在此时间之前经过 FailureBlackout 秒后，将忽略所有请求。 超时之后第一个调用方测试上游符号存储区。 如果成功，删除超时和允许的请求。 在失败时，时间设置为现在 + FailureBlackout 秒。 该时间后上游符号存储区重新测试。</p></td>
</tr>
<tr class="even">
<td align="left">MissAgeTimeout</td>
<td align="left"><p>挂起的说明</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">RequestTimeout</td>
<td align="left"><p>挂起的说明</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">RetryAppHang</td>
<td align="left"><p>挂起的说明</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">NoLongerIndexedAuthoritive</td>
<td align="left"><p>挂起的说明</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">UriFilter</td>
<td align="left"><p>挂起的说明</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">UriTiers</td>
<td align="left"><p>挂起的说明</p>
<p></p></td>
</tr>
</tbody>
</table>



### <a name="span-idaccessingoutsidenetworkresourcesspanspan-idaccessingoutsidenetworkresourcesspanaccessing-outside-network-resources"></a><span id="accessing_outside_network_resources"></span><span id="ACCESSING_OUTSIDE_NETWORK_RESOURCES"></span>访问外部网络资源

SymSrv SymProxy 结合使用时，它作为服务运行，并使用 WinHTTP API 通过 HTTP 连接访问的符号。 这不同于其常规行为的 WinInet 将用于此目的。

因此，您可能需要设置 HTTP 代理设置，使此服务可以访问外部网络资源。 使用以下方法之一来配置这些设置：

-   使用 Netsh 工具 (netsh.exe)。 有关说明，在命令提示符窗口中键入以下：

    ```console
    netsh winhttp -? 
    ```

SymProxy 的默认行为是使用通过 ProxyCfg 或 Netsh 指定任何 HTTP 代理。 如果没有 HTTP 代理配置，SymProxy 使用虚拟代理以便保护在 intranet 中的 HTTP 网站的访问权限。 产生了负面影响，这种方法可防止 SymProxy 使用直接连接到外部 Internet。 如果你想要允许 SymProxy 的直接连接到 Internet，创建 REG\_名为 DWORD 值**NoInternetProxy**中**符号服务器代理**注册表的密钥。 设置的值**NoInternetProxy**为 1，并验证是否通过 ProxyCfg 指示没有 HTTP 代理。

