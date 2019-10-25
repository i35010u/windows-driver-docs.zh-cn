---
title: 支持 UNC 命名和 MUP
description: 支持 UNC 命名和 MUP
ms.assetid: 07c4a498-10c7-41b2-aaeb-73cab946f392
keywords:
- 内核网络重定向 WDK，UNC 命名
- 内核网络重定向 WDK，MUP
- MUP WDK 网络重定向器
- 多 UNC 提供程序 WDK 网络重定向程序
- UNC WDK 网络重定向器
- 命名 WDK 文件系统
- 前缀解析 WDK 网络重定向器
- 前缀缓存 WDK 网络重定向器
- 串行前缀解析 WDK 网络重定向器
- 并行前缀解析 WDK 网络重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c17f495247d2b1d7ba8a24430ed65aa02fec246
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840961"
---
# <a name="support-for-unc-naming-and-mup"></a>支持 UNC 命名和 MUP


多 UNC 提供程序（MUP）是一个内核模式组件，该组件负责使用通用命名约定（UNC）名称对能够处理远程文件系统的网络重定向程序（UNC 提供程序）排列所有远程文件系统访问发出. 当应用程序使用 UNC 路径时，MUP 涉及到可从命令行执行的以下示例所示：

```cpp
notepad \\server\public\readme.txt
```

MUP 在创建映射驱动器号（例如 "NET USE" 命令）的操作过程中不涉及。 此操作由多提供商路由器（MPR）和网络重定向器的用户模式 WNet 提供程序 DLL 处理。 但是，用户模式 WNet 提供程序 DLL 可以在此操作期间直接与内核模式网络重定向程序驱动程序通信。

在 Microsoft Windows Server 2003、Windows XP 和 Windows 2000 上，在映射驱动器上执行的、不代表分布式文件系统（DFS）驱动器的远程文件操作不会经历 MUP。 这些操作直接跳到处理驱动器号映射的网络提供程序。

对于符合 Windows Vista 重定向程序模型的网络重定向程序，如果使用映射的网络驱动器，则会涉及 MUP。 在映射驱动器上执行的文件操作会通过 MUP 进入网络重定向程序。 请注意，在这种情况下，MUP 只是将操作传递到所涉及的网络重定向程序。

MUP 是*mup*二进制文件的一部分，它还包括 windows Server 2003、windows XP 和 windows 2000 中的 Microsoft DFS 客户端。

内核网络重定向程序通常还具有用户模式 WNet 提供程序 DLL，以支持与远程资源建立连接（例如，将驱动器号映射到远程资源）。 MPR 是一个用户模式 DLL，它基于到 WNet 提供程序的查询建立网络连接。 调用 MPR 可能会导致以下任何情况：

在命令提示符下发出的 "net use x： \\\\server\\share" 命令。

从 Windows 资源管理器建立的网络驱动器号连接

直接调用 WNet 函数。

网络重定向程序必须注册 MUP 才能处理 UNC 名称。 可以有多个 UNC 提供程序注册到 MUP。 这些 UNC 提供程序可以是下列一项或多项：

-   基于 RDBSS 的网络微重定向程序

-   旧版重定向器不基于 RDBSS

MUP 确定哪些提供程序可以处理基于名称的操作中的 UNC 路径，通常为 IRP\_MJ\_创建请求。 这称为 "前缀解析"。 在 Windows Vista 之前，前缀解析操作有两个用途：

-   导致前缀解析的基于名称的操作将被路由到声明前缀的提供程序。 如果成功，MUP 确保后续的基于处理程序的操作（如 IRP\_MJ\_读取和 IRP\_MJ\_写入，从而完全绕过 MUP。

-   该提供程序及其声明的前缀在由 MUP 维护的前缀缓存中输入。 对于后续的基于名称的操作，MUP 使用此前缀缓存来确定提供程序在尝试执行前缀解析之前是否已经声明了前缀。 将此前缀缓存中的每个条目添加到缓存后，它会受到超时（称为 TTL）的限制。 此超时到期后，将会丢弃某个条目，此时，MUP 会对后续基于名称的操作再次执行前缀解析。

MUP 通过发出[**IOCTL\_REDIR\_查询\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ni-ntifs-ioctl_redir_query_path)向注册到 MUP 的网络重定向程序请求路径请求来执行前缀解析。 用于 IOCTL\_REDIR\_QUERY\_路径的输入和输出缓冲区如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">可用参数于</th>
<th align="left">数据结构格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>输入缓冲区</strong></p></td>
<td align="left"><p>IrpSp-&gt; 参数. DeviceIoControl. Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>输出缓冲区</strong></p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL 和数据结构在*ntifs*中定义。 缓冲区是从非分页池分配的。

网络重定向程序应仅允许此 IOCTL 的内核模式发送方，验证 IRP 结构的**RequesterMode**成员是否为**KernelMode**。

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
<td align="left"><p><strong>FilePathName</strong>成员中包含的 Unicode 字符串的长度（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SecurityContext</strong></p></td>
<td align="left"><p>指向安全上下文的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePathName</strong></p></td>
<td align="left"><p>&lt;server&gt;&lt;共享&gt;&lt;路径&gt;形式的非 NULL 终止 Unicode 字符串。 字符串的长度（以字节为单位）由<strong>PathNameLength</strong>成员指定。</p></td>
</tr>
</tbody>
</table>



UNC 提供程序应使用查询\_路径\_响应数据结构来了解响应信息。

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
<td align="left"><p>提供程序从 QUERY_PATH_REQUEST 结构的<strong>FilePathName</strong>成员中指定的 Unicode 字符串路径的前缀的长度（以字节为单位）。</p></td>
</tr>
</tbody>
</table>



请注意，IOCTL\_REDIR\_查询\_路径是\_两个 IOCTL 的方法。 这意味着输入缓冲区和输出缓冲区可能不在同一地址。 UNC 提供程序的一个常见错误是假定输入缓冲区和输出缓冲区相同，并使用输入缓冲区指针来提供响应。

当 UNC 提供程序收到 IOCTL\_REDIR\_QUERY\_PATH 请求时，它必须确定该提供程序是否可以处理\_路径\_请求结构的查询的**FilePathName**成员中指定的 UNC 路径。 如果是这样，则必须将查询\_路径\_响应结构的**LengthAccepted**成员更新为它所声明的前缀的长度（以字节为单位），并完成状态为\_SUCCESS 的 IRP。 如果提供程序无法处理指定的 UNC 路径，则它必须使 IOCTL\_使用适当的 NTSTATUS 错误代码\_查询\_路径请求，且不得更新\_路径的查询的**LengthAccepted**成员\_响应结构。 提供程序不能修改任何其他成员或任何条件下的**FilePathName**字符串。

如果在响应 IRP\_MJ\_创建或其他使用 UNC 名称的 Irp 时无法识别 \\\\服务器\\共享前缀名称，建议返回的 NTSTATUS 代码是以下各项之一:

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>状态\_错误\_网络\_路径  
找不到网络路径。 虚拟机名称（例如\\\\服务器）无效或网络重定向程序无法解析计算机名称（使用任何可用的名称解析机制）。

<span id="STATUS_BAD_NETWORK_NAME"></span><span id="status_bad_network_name"></span>状态\_错误\_网络\_名称  
在远程服务器上找不到指定的共享名。 例如，计算机名（例如\\\\服务器）有效，但在远程服务器上找不到指定的共享名。

<span id="STATUS_INSUFFICIENT_RESOURCES"></span><span id="status_insufficient_resources"></span>状态\_\_资源不足  
没有足够的资源可用于为缓冲区分配内存。

<span id="STATUS_INVALID_DEVICE_REQUEST"></span><span id="status_invalid_device_request"></span>状态\_无效\_设备\_请求  
IOCTL\_REDIR\_查询\_路径请求应仅来自 MUP，而 IRP 的请求者模式应始终为**KernelMode**。 如果调用线程的请求者模式没有**KernelMode**，则返回此错误代码。

<span id="STATUS_INVALID_PARAMETER"></span><span id="status_invalid_parameter"></span>状态\_无效\_参数  
查询\_路径\_请求结构中的**PathNameLength**成员超出了 unicode 字符串的最大允许长度，UNICODE\_字符串\_最大\_字节数。

<span id="STATUS_LOGON_FAILURE_or_STATUS_ACCESS_DENIED"></span><span id="status_logon_failure_or_status_access_denied"></span><span id="STATUS_LOGON_FAILURE_OR_STATUS_ACCESS_DENIED"></span>状态\_登录\_失败或状态\_拒绝访问\_  
如果前缀解析操作由于无效或不正确的凭据而失败，则提供程序应返回远程服务器返回的确切错误代码;这些错误代码不得转换为状态\_错误\_网络\_名称或状态\_错误\_网络\_路径。 错误代码（如状态\_登录\_失败和状态\_拒绝访问\_将作为向用户提供的反馈机制，指示要求使用适当的凭据。 在某些情况下，也使用这些错误代码来自动提示用户输入凭据。 如果没有这些错误代码，用户可能会认为计算机无法访问。

如果网络重定向程序无法解析前缀，则它必须返回与上述建议的 NTSTATUS 代码列表中的预期语义最为匹配的 NTSTATUS 代码。 如果不是上述列表中的 NTSTATUS 代码，网络重定向程序不能将实际遇到的错误（例如\_连接\_拒绝）直接返回到 MUP。

提供程序声明的前缀长度取决于单个 UNC 提供程序。 大多数提供商通常会声明 \\\\&lt;服务器名称&gt;\\&lt;共享 &gt; \\\\&lt;servername&gt;\\&lt;&gt;&lt;路径\\&gt;。 例如，如果提供程序在给定 \\路径 \\\\server\\公共公开\\server\\public\\dir1\\dir2，则前缀的所有基于名称的操作 \\\\server\\公开（例如\\server\\公用\\file1）会自动路由到该提供程序，而不会进行任何前缀解析，因为前缀已在前缀缓存中。 不过，\\server\\行销\\演示的前缀路径将通过前缀解析。

如果网络重定向程序声明服务器名称（例如\\\\服务器），则此服务器上的所有共享请求都将发送到此网络重定向程序。 仅当其他网络重定向程序无法访问同一服务器上的另一个共享时，此行为才是可接受的。 例如，声明 UNC 路径 \\\\服务器的网络重定向器将阻止其他网络重定向程序访问此服务器上的其他共享（例如，WebDAV 访问 \\\\server\\web）。

通过调用[**FsRtlRegisterUncProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider) ，使用 MUP 注册为 UNC 提供程序的任何旧版网络重定向程序（而不是基于使用 RDBSS）将接收 IOCTL\_REDIR\_QUERY\_路径请求。

表示支持作为 UNC 提供程序的网络微重定向程序将接收此前缀声明，就像它是 IRP\_MJ\_CREATE 调用一样。 此创建请求类似于用户模式**Createfile**调用，文件\_创建\_树\_连接标志。 网络小型重定向程序将不会接收前缀声明作为对[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](https://msdn.microsoft.com/library/windows/hardware/ff550715)的调用。 对于前缀声明，RDBSS 会将[**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)请求发送到网络小型重定向程序，然后调用[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)和[**MRxCreateVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)。 当网络微重定向器注册到 RDBSS 时，网络小型重定向器的驱动程序调度表将由 RDBSS 复制到指向内部 RDBSS 入口点。 然后，RDBSS 接收到此 IOCTL\_REDIR\_查询为网络微型重定向程序在内部\_路径，并调用**MRxCreateSrvCall**、 **MRxSrvCallWinnerNotify**和**MRxCreateVNetRoot**。 原始 IOCTL\_REDIR\_查询\_路径 IRP 将包含在传递到**MRxCreateSrvCall**例程的 RX\_上下文结构中。 此外，将修改传递到**MRxCreateSrvCall**的 RX\_上下文中的以下成员：

即使原始 IRP 为 IRP\_MJ\_设备\_控件， **MajorFunction**成员也设置为 IRP\_MJ\_CREATE。

**PrefixClaim**成员设置为查询\_路径\_请求结构的**FilePathName**成员。

**PrefixClaim**成员设置为查询\_路径\_请求结构的**PathNameLength**成员。

**NtCreateParameters. SecurityContext**成员设置为查询\_路径\_请求结构的**SecurityContext**成员。

**ThisIsATreeConnectOpen**成员设置为**TRUE**。

**Create Flags**成员具有 RX\_上下文\_创建\_\_UNC\_名称位集的标志。

如果网络小型重定向程序想要查看前缀声明的详细信息，则可以读取 RX 中的这些成员\_传递给**MRxCreateSrvCall**的上下文。 否则，它只会尝试连接到服务器共享，并在**MRxCreateSrvCall**调用成功时返回状态\_成功。 RDBSS 将代表网络小型重定向器发出前缀声明。

在这种情况下，网络小型重定向器可以直接接收此 IOCTL。 网络小型重定向程序可以在初始化并注册到 RDBSS 之前保存其驱动程序调度表的副本。 在调用[**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)以向 RDBSS 注册后，网络小型重定向程序可以保存由 RDBSS 安装的新驱动程序调度表入口点的副本，并还原其原始驱动程序调度表。 需要对还原的驱动程序调度表进行修改，以便在为网络微型重定向程序所需的目标检查收到的 IRP 后，调用将转发到 RDBSS 驱动程序调度入口点。 当驱动程序初始化 RDBSS 并调用**RxRegisterMinrdr**时，RDBSS 将复制网络小型重定向程序的驱动程序调度表。 链接到*rdbsslib*的网络微型重定向程序必须先保存其原始驱动程序调度表，然后再从其**DriverEntry**例程调用[**RxDriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry) ，以初始化 RDBSS 静态库并还原其驱动程序调用**RxRegisterMinrdr**之后调度表。 这是因为 RDBSS 会在**RxDriverEntry**和**RxRegisterMinrdr**例程中通过网络小型重定向器发送表进行复制。

前缀解析期间查询提供程序的顺序由存储在以下注册表项下的 REG\_SZ ProviderOrder 注册表值控制：

```cpp
HKLM\System\CurrentControlSet\Control\NetworkProvider\Order
```

ProviderOrder 注册表值中的单个提供程序名称以逗号分隔，不包含任何前导或尾随空格。

例如，此值可能包含字符串：

```cpp
RDPNP,LanmanWorkstation,WebClient
```

给定 UNC 路径 \\\\&lt;server&gt;\\&lt;共享&gt;\\&lt;&gt;\\，MUP 发出前缀解析请求（如果前缀为\\@no__t_例如，在 MUP 前缀缓存中找不到12_ 共享或 \\\\服务器）。 MUP 按以下顺序向每个提供程序发送前缀解析请求，直到提供程序声明前缀（或已查询所有提供程序）：

1.  TS 客户端（RDPNP）

2.  SMB 重定向程序（LanmanWorkstation）

3.  WebDAV 重定向程序（WebClient）

更改 ProviderOrder 注册表值需要重新启动才能在 Windows Server 2003、Windows XP 和 Windows 2000 上的 MUP 中生效。

MUP 使用列出的每个提供程序名称来查找以下注册表项下的提供程序的注册表项：

```cpp
HKLM\System\CurrentControlSet\Services\<ProviderName>
```

MUP 然后读取 NetworkProvider 子项下的 DeviceName 值以查找提供程序将注册的设备名称。 当提供程序实际注册时，MUP 会将传入的设备名称与已知提供程序的设备名称列表相匹配，并将提供程序置于排序列表中以用于前缀解析。 此列表中提供程序的顺序基于前面讨论的 ProviderOrder 注册表值中指定的顺序。

请注意，此提供程序顺序也由多提供商路由器（MPR）提供，后者基于 WNet 提供程序的查询建立网络连接。

在带有 service pack 1 和 Windows XP Service Pack 2 的 Windows Server 2003 之前，MUP 行为是以 ProviderOrder 注册表值中指定的顺序向所有提供程序 "并行" 发出前缀解析请求，然后等待所有提供程序完成前缀解析操作。 因此，即使第一个提供程序声明了前缀，MUP 仍会等待所有其他提供程序完成前缀解析操作。 当多个提供程序使用前缀声明进行响应时，MUP 会根据在 ProviderOrder 注册表值中指定的顺序选择该提供程序。

在 Windows XP Service Pack 2 和更高版本以及 Windows Server 2003 Service Pack 1 及更高版本中，此行为略有变化。 MUP 按顺序发出前缀解析请求，并在第一个提供程序声明前缀时立即停止。 因此，在上述示例中，如果 RDPNP 声明了前缀，则 MUP 将不会调用 SMB 或 WebDAV 重定向器。

更改此行为的主要原因是 "串行前缀解析" 方案阻止了 ProviderOrder 值中优先级较低的网络重定向程序的事例，导致ProviderOrder 值。 例如，考虑使用防火墙的远程服务器，配置为阻止特定类型的 TCP/IP 数据包（例如，对 HTTP 的访问），但允许其他类型的（例如 SMB 访问）。 在这种情况下，即使 SMB 网络重定向程序配置为 ProviderOrder 值中的第一个提供程序并快速声明前缀，WebDAV 重定向程序可能会通过等待 TCP 连接到timeout.








