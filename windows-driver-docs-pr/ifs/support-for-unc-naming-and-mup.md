---
title: 支持 UNC 命名和 MUP
description: 支持 UNC 命名和 MUP
ms.assetid: 07c4a498-10c7-41b2-aaeb-73cab946f392
keywords:
- 内核网络重定向程序 WDK，UNC 命名
- 内核网络重定向程序 WDK MUP
- MUP WDK 网络重定向程序
- 多个 UNC 提供程序 WDK 网络重定向程序
- UNC WDK 网络重定向程序
- 名称 WDK 文件系统
- 前缀解析 WDK 网络重定向程序
- 前缀缓存 WDK 网络重定向程序
- 串行前缀解析 WDK 网络重定向程序
- 并行的前缀解析 WDK 网络重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d471ede1543438093cad0cb61592d8c9b502d8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344366"
---
# <a name="support-for-unc-naming-and-mup"></a>支持 UNC 命名和 MUP


多个 UNC provider (MUP) 是负责排列所有远程文件系统访问使用到能够处理远程文件系统的网络重定向 （UNC 访问接口） 的通用命名约定 (UNC) 名称的内核模式组件请求数。 MUP 时所涉及的 UNC 路径由应用程序可以从命令行执行下面的示例所示：

```cpp
notepad \\server\public\readme.txt
```

在创建映射的驱动器号 （例如"NET 使用"命令） 的操作的过程不涉及 MUP。 此操作是由多个提供商路由器 (MPR) 和用户模式下 WNet 提供程序 DLL for 网络重定向程序处理的。 但是，用户模式下 WNet 提供程序 DLL 可以直接与内核模式网络重定向程序驱动程序通信在执行此操作。

在 Microsoft Windows Server 2003、 Windows XP 和 Windows 2000 上，执行映射驱动器，无法表示的分布式文件系统 (DFS) 驱动器上的远程文件操作不需要经过 MUP。 这些操作直接转到处理驱动器号映射的网络提供程序。

为符合 Windows Vista 重定向程序模型的网络重定向，即使使用的映射的网络驱动器时涉及到 MUP。 在映射的驱动器上执行文件操作通过 MUP 转到网络重定向程序。 请注意，在这种情况下 MUP 只是将传递该操作向网络重定向程序涉及。

MUP 属于*mup.sys*还包括 Microsoft DFS 客户端在 Windows Server 2003、 Windows XP 和 Windows 2000 中的二进制文件。

通常情况下将内核网络重定向程序还具有用户模式下 WNet 提供程序 DLL 以支持建立到远程资源 （例如，将驱动器号映射到远程资源） 的连接。 MPR 是建立网络连接基于 WNet 提供程序对查询的用户模式 DLL。 从以下任一情况下，对 MPR 的调用将产生结果：

一个"使用 x:，net \\ \\server\\共享"命令提示符下发出命令。

从 Windows 资源管理器建立的网络驱动器号连接

直接调用 WNet 函数。

网络重定向程序必须注册 MUP 来处理 UNC 名称。 可以有多个 UNC 提供程序注册到 MUP。 这些 UNC 提供程序可以是一个或多项操作：

-   网络微型-重定向程序基于 RDBSS

-   不基于 RDBSS 的旧式重定向程序

MUP 确定哪个提供程序可以处理在基于名称的操作中，通常 IRP 的 UNC 路径\_MJ\_创建请求。 这被称为"前缀解决方法。" 在 Windows Vista 之前的前缀解析操作有两个用途：

-   基于名称的操作，从而产生了前缀解析路由到声明前缀的提供程序。 如果成功，MUP 可确保后续基于句柄的操作 (IRP\_MJ\_IRP 读\_MJ\_编写，例如) 转到完全绕过 MUP 相同的提供程序。

-   在维护 MUP 前缀缓存中输入提供程序和其声明的前缀。 对于后续基于名称的操作，MUP 使用此前缀缓存来确定是否提供程序尝试执行前缀解析之前已声明前缀。 此前缀缓存中的每个条目受到 （也称为 TTL） 的超时后添加到缓存。 此超时过期后立即引发一个条目，请在哪个时间点 MUP 将执行前缀解析再次为后续的基于名称的操作上此前缀。

MUP 执行前缀解析通过发出[ **IOCTL\_是否重定向\_查询\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff548313)网络重定向程序注册到 MUP 的请求。 IOCTL 的输入和输出缓冲区\_是否重定向\_查询\_路径如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">参数可在</th>
<th align="left">数据结构格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>输入的缓冲区</strong></p></td>
<td align="left"><p>IrpSp-&gt; Parameters.DeviceIoControl.Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>输出缓冲区</strong></p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL 和数据结构中定义*ntifs.h*。 从非分页缓冲池分配缓冲区。

网络重定向程序只应只需验证允许内核模式发件人的此 IOCTL **RequesterMode** IRP 结构中的成员是**KernelMode**。

MUP 使用查询\_路径\_请求信息的请求数据结构。

```cpp
typedef struct _QUERY_PATH_REQUEST {
    ULONG                PathNameLength;
    PIO_SECURITY_CONTEXT SecurityContext;
    WCHAR                FilePathName[1];
} QUERY_PATH_REQUEST, *PQUERY_PATH_REQUEST;
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>PathNameLength</strong></p></td>
<td align="left"><p>中包含的 Unicode 字符串的长度，以字节为单位， <strong>FilePathName</strong>成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SecurityContext</strong></p></td>
<td align="left"><p>指向的安全上下文的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePathName</strong></p></td>
<td align="left"><p>以非 NULL 结尾的 Unicode 字符串的窗体&amp;l t; 服务器&gt;&amp;l t; 共享&gt;&amp;l t; 路径&gt;。 通过指定的字符串，以字节为单位，长度<strong>PathNameLength</strong>成员。</p></td>
</tr>
</tbody>
</table>



UNC 提供程序应使用的查询\_路径\_响应数据结构，用于响应信息。

```cpp
typedef struct _QUERY_PATH_RESPONSE {
    ULONG  LengthAccepted;
} QUERY_PATH_RESPONSE, *PQUERY_PATH_RESPONSE;
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>LengthAccepted</strong></p></td>
<td align="left"><p>提供程序中指定的 Unicode 字符串路径从声明的前缀长度，以字节为单位， <strong>FilePathName</strong> QUERY_PATH_REQUEST 结构中的成员。</p></td>
</tr>
</tbody>
</table>



请注意该 IOCTL\_是否重定向\_查询\_路径是一种方法\_既不 IOCTL。 这意味着输入和输出缓冲区可能无法在相同的地址。 通过 UNC 提供程序的一个常见错误是假定输入的缓冲区和输出缓冲区是相同的并且使用输入的缓冲区指针来提供响应。

当 UNC 提供程序收到 IOCTL\_是否重定向\_查询\_路径请求时，它必须确定它是否可以处理中指定的 UNC 路径**FilePathName**成员查询\_路径\_请求结构。 如果因此，必须更新**LengthAccepted**查询的成员\_路径\_响应结构，它具有声明，并完成状态 IRP 的前缀长度，以字节为单位，\_成功。 如果提供程序无法处理指定的 UNC 路径，则必须失败 IOCTL\_是否重定向\_查询\_路径请求并返回相应的 NTSTATUS 错误代码并不能更新**LengthAccepted**查询的成员\_路径\_响应结构。 提供程序不能修改任何其他成员或**FilePathName**在任何情况下的字符串。

如果\\\\服务器\\共享前缀名无法识别响应 IRP\_MJ\_创建或使用 UNC 名称，建议的 NTSTATUS 代码，以返回其他 Irp 是以下之一：

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>状态\_坏\_网络\_路径  
找不到的网络路径。 计算机名称 (\\\\服务器，例如) 不是有效或网络重定向程序无法解析计算机名称 （使用任何名称解析机制）。

<span id="STATUS_BAD_NETWORK_NAME"></span><span id="status_bad_network_name"></span>状态\_坏\_网络\_名称  
在远程服务器上找不到指定的共享名称。 计算机名称 (\\\\服务器，例如) 是有效的但指定远程服务器上找不到共享名称。

<span id="STATUS_INSUFFICIENT_RESOURCES"></span><span id="status_insufficient_resources"></span>状态\_不足\_资源  
没有可用于为缓冲区分配内存资源不足。

<span id="STATUS_INVALID_DEVICE_REQUEST"></span><span id="status_invalid_device_request"></span>状态\_无效\_设备\_请求  
IOCTL\_是否重定向\_查询\_路径请求应仅来自 MUP 和 IRP 的请求者模式始终应**KernelMode**。 如果调用线程的请求者模式不返回此错误代码**KernelMode**。

<span id="STATUS_INVALID_PARAMETER"></span><span id="status_invalid_parameter"></span>状态\_无效\_参数  
**PathNameLength**在查询中的成员\_路径\_请求结构超出了最大允许长度 UNICODE\_字符串\_最大\_以字节为 Unicode字符串。

<span id="STATUS_LOGON_FAILURE_or_STATUS_ACCESS_DENIED"></span><span id="status_logon_failure_or_status_access_denied"></span><span id="STATUS_LOGON_FAILURE_OR_STATUS_ACCESS_DENIED"></span>状态\_LOGON\_故障或状态\_访问\_被拒绝  
如果由于凭据无效或不正确，前缀解析操作失败，该提供程序应返回远程服务器; 返回的具体错误代码必须将这些错误代码转换到状态\_坏\_网络\_名称或状态\_错误\_网络\_路径。 错误代码等状态\_LOGON\_故障和状态\_访问\_拒绝作为，该值指示需要使用相应的凭据的用户的反馈机制。 这些错误代码还在某些情况下用于提示用户自动提供凭据。 如果没有这些错误代码，用户可能认为计算机不可访问。

如果无法解析前缀网络重定向程序，它必须返回与上述列表中的建议 NTSTATUS 代码从预期的语义相符的 NTSTATUS 代码。 网络重定向程序不能返回实际遇到的错误 (状态\_连接\_被拒绝，例如) 直接向 MUP 如果 NTSTATUS 代码不是上述列表中。

声明提供程序的前缀长度取决于单个 UNC 提供程序。 大多数提供程序通常声明\\ \\ &lt;servername&gt;\\&lt;sharename&gt;窗体的路径的一部分\\ \\ &lt;servername&gt;\\&lt;sharename&gt;\\&lt;路径&gt;。 例如，如果提供程序声明\\\\服务器\\给定路径的公共\\ \\server\\公共\\dir1\\dir2，对于所有基于名称的操作前缀\\\\服务器\\公共 (\\server\\公共\\file1，例如) 将被路由到该提供程序而不会因为任何前缀解析前缀已在前缀缓存。 但是，使用前缀路径\\服务器\\市场营销\\演示文稿将经历前缀解析。

如果网络重定向程序声明一个服务器名称 (\\\\，例如，服务器)，此服务器上的共享的所有请求将都转到此网络重定向程序。 此行为只是不可能由不同的网络重定向程序访问在同一服务器上的另一个共享的情况下可以接受的。 例如，网络重定向程序声明\\ \\UNC 路径的服务器将阻止其他网络重定向到此服务器上的其他共享的访问 (WebDAV 访问\\ \\server\\web，例如).

任何旧的网络重定向程序 （不基于使用 RDBSS） 注册为与 MUP UNC 提供程序通过调用[ **FsRtlRegisterUncProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff547178)将收到 IOCTL\_是否重定向\_查询\_路径请求。

一个网络微型重定向，该值指示支持 UNC 提供程序会收到此前缀声明，就好像 IRP\_MJ\_创建调用。 此创建请求是类似于用户模式**Createfile**调用与文件一起\_创建\_树\_连接标志上设置。 网络微型重定向不会与调用收到的前缀声明[ **MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](https://msdn.microsoft.com/library/windows/hardware/ff550715)。 前缀声明，将发送 RDBSS [ **MRxCreateSrvCall** ](https://msdn.microsoft.com/library/windows/hardware/ff549864)网络微型重定向到的调用后跟对请求[ **MRxSrvCallWinnerNotify**](https://msdn.microsoft.com/library/windows/hardware/ff550824)并[ **MRxCreateVNetRoot**](https://msdn.microsoft.com/library/windows/hardware/ff549869)。 当网络微型重定向注册与 RDBSS 时，网络微型重定向的驱动程序调度表将被复制转移 RDBSS 为指向内部 RDBSS 入口点。 RDBSS 然后接收此 IOCTL\_是否重定向\_查询\_内部的网络微型重定向和调用路径**MRxCreateSrvCall**， **MRxSrvCallWinnerNotify**，并**MRxCreateVNetRoot**。 原始 IOCTL\_是否重定向\_查询\_路径 IRP 将包含在 RX\_上下文结构传递给**MRxCreateSrvCall**例程。 此外，RX 中的以下成员\_上下文传递给**MRxCreateSrvCall**将进行相应修改：

**MajorFunction**成员设置为 IRP\_MJ\_创建即使原始 IRP 是 IRP\_MJ\_设备\_控件。

**PrefixClaim.SuppliedPathName.Buffer**成员设置为**FilePathName**查询的成员\_路径\_请求结构。

**PrefixClaim.SuppliedPathName.Length**成员设置为**PathNameLength**查询的成员\_路径\_请求结构。

**Create.NtCreateParameters.SecurityContext**成员设置为**SecurityContext**查询的成员\_路径\_请求结构。

**Create.ThisIsATreeConnectOpen**成员设置为**TRUE**。

**Create.Flags**成员具有 RX\_上下文\_创建\_标志\_UNC\_名称位集。

如果网络微型-重定向程序想要查看的前缀声明的详细信息，它可以读取这些成员中 RX\_上下文传递给**MRxCreateSrvCall**。 否则它可以仅尝试连接到服务器共享，并返回状态\_成功如果**MRxCreateSrvCall**调用是否成功。 RDBSS 将代表网络声明的前缀微型重定向。

没有一种情况下网络微型重定向无法直接接收此 IOCTL。 网络微型重定向无法初始化和注册 RDBSS 之前保存一份其驱动程序调度表。 在调用[ **RxRegisterMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554693)注册 RDBSS，网络微型重定向可保存一份新的驱动程序调度表入口点，由 RDBSS 安装并还原其原始的驱动程序调度表。 还原驱动程序调度表将需要修改，以便网络微型重定向到感兴趣的那些检查接收的 IRP，完后调用转发到 RDBSS 驱动程序调度入口点。 驱动程序初始化 RDBSS 和调用时，将通过网络微型重定向的驱动程序调度表复制 RDBSS **RxRegisterMinrdr**。 一个网络微型重定向链接针对*rdbsslib.lib*必须保存其原始的驱动程序调度表，然后调用[ **RxDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554404)从其**DriverEntry**例程，以初始化 RDBSS 静态库，并还原其驱动程序调度表之后调用**RxRegisterMinrdr**。 这是因为在这种网络微型重定向程序调度表通过复制 RDBSS **RxDriverEntry**并**RxRegisterMinrdr**例程。

提供程序在前缀解析期间进行查询的顺序受 REG\_SZ ProviderOrder 注册表值都存储在以下项：

```cpp
HKLM\System\CurrentControlSet\Control\NetworkProvider\Order
```

而无需任何前导或尾随空格的逗号分隔单个提供程序名称 ProviderOrder 注册表值中。

例如，此值可能包含字符串：

```cpp
RDPNP,LanmanWorkstation,WebClient
```

给定的 UNC 路径\\ \\&lt;服务器&gt;\\&lt;共享&gt;\\&lt;路径&gt;，如果将 MUP 发出前缀解析请求前缀 (\\\\服务器\\共享或\\\\服务器，例如) MUP 前缀缓存中找不到。 MUP 将前缀解析请求发送到每个提供程序按以下顺序直到提供程序声明前缀 （或所有提供程序已查询）：

1.  TS 客户端 (RDPNP)

2.  SMB 重定向程序 (LanmanWorkstation)

3.  WebDAV 重定向程序 (WebClient)

对 ProviderOrder 注册表值的更改需要重新启动才能在 Windows Server 2003、 Windows XP 和 Windows 2000 上 MUP 中生效。

MUP 使用下列查找提供程序的注册表项下的注册表项下每个提供程序名称：

```cpp
HKLM\System\CurrentControlSet\Services\<ProviderName>
```

MUP 然后读取要查找与提供程序将注册的设备名称的 NetworkProvider 子项下的设备名称值。 当实际注册时提供程序时，MUP 匹配传递使用已知的提供程序的设备名称的列表的设备名称，并出于前缀解析的有序列表中将提供程序。 此列表中的提供程序的顺序基于上文所述的 ProviderOrder 注册表值中指定的顺序。

请注意，此提供程序的顺序也可由多个提供程序路由器 (MPR)，建立基于 WNet 提供程序对查询的网络连接的用户模式 DLL。

在 Windows Server 2003 Service Pack 1 和 Windows XP Service Pack 2 之前, MUP 行为是 ProviderOrder 注册表值中指定的顺序向"并行"的所有提供程序颁发的前缀解析请求，然后等待所有提供程序若要完成的前缀解析操作。 因此，即使第一个提供程序声明前缀，MUP 仍会等待所有其他提供程序来完成前缀解析操作。 当多个提供程序与前缀声明做出响应时，MUP 选择基于 ProviderOrder 注册表值中指定的顺序的提供程序。

在 Windows XP Service Pack 2 和更高版本和 Windows Server 2003 Service Pack 1 及更高版本，此行为稍有更改。 MUP 按顺序发出前缀解析请求，并停止时的第一个提供程序声明前缀。 因此，在上面的示例中，如果 RDPNP 声明一个前缀，MUP 将不调用 SMB 或 WebDAV 重定向程序。

此行为已更改的主要原因是，"串行前缀解析"方案可以防止网络重定向程序的情况下 ProviderOrder 值中较低优先级导致性能问题的更高优先级中的网络重定向程序ProviderOrder 值。 例如，考虑具有防火墙，配置为阻止特定类型的 TCP/IP 数据包 （访问 HTTP，例如），但允许其他人 （例如 SMB 访问） 的远程服务器。 在这种情况下，即使 SMB 网络重定向程序配置为 ProviderOrder 值中的第一个提供程序，并且快速声明前缀，WebDAV 重定向程序可能会明显延迟前缀解析的完成等待 TCP 连接到超时值。








