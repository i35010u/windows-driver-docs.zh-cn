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
ms.openlocfilehash: aabf1d8a467a5932d7a004026ca830964bea59dd
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107378"
---
# <a name="support-for-unc-naming-and-mup"></a>支持 UNC 命名和 MUP


多 UNC 提供程序 (MUP) 是一个内核模式组件，该组件负责使用通用命名约定 (UNC) 名称到网络重定向程序， (UNC 提供程序) 能够处理远程文件系统请求。 当应用程序使用 UNC 路径时，MUP 涉及到可从命令行执行的以下示例所示：

```cpp
notepad \\server\public\readme.txt
```

MUP 在创建映射的驱动器号 ("NET USE" 命令中不涉及，例如) 。 此操作由多提供商路由器 (MPR) 和网络重定向程序的用户模式 WNet 提供程序 DLL 处理。 但是，用户模式 WNet 提供程序 DLL 可以在此操作期间直接与内核模式网络重定向程序驱动程序通信。

在 Microsoft Windows Server 2003、Windows XP 和 Windows 2000 上，在映射驱动器上执行的远程文件操作（不表示分布式文件系统 (DFS) 驱动器）不会经历 MUP。 这些操作直接跳到处理驱动器号映射的网络提供程序。

对于符合 Windows Vista 重定向程序模型的网络重定向程序，如果使用映射的网络驱动器，则会涉及 MUP。 在映射驱动器上执行的文件操作会通过 MUP 进入网络重定向程序。 请注意，在这种情况下，MUP 只是将操作传递到所涉及的网络重定向程序。

MUP 是 *mup.sys* 二进制文件的一部分，它还包括 windows Server 2003、windows XP 和 windows 2000 中的 Microsoft DFS 客户端。

通常，内核网络重定向器还会有一个用户模式 WNet 提供程序 DLL，以支持与远程资源建立连接 (将驱动器号映射到远程资源，例如) 。 MPR 是一个用户模式 DLL，它基于到 WNet 提供程序的查询建立网络连接。 调用 MPR 可能会导致以下任何情况：

在命令提示符下发出的 "net use x： \\ \\ server \\ share" 命令。

从 Windows 资源管理器建立的网络驱动器号连接

直接调用 WNet 函数。

网络重定向程序必须注册 MUP 才能处理 UNC 名称。 可以有多个 UNC 提供程序注册到 MUP。 这些 UNC 提供程序可以是下列一项或多项：

-   基于 RDBSS 的网络微重定向程序

-   旧版重定向器不基于 RDBSS

MUP 确定哪些提供程序可以处理基于名称的操作中的 UNC 路径，通常为 IRP \_ MJ \_ 创建请求。 这称为 "前缀解析"。 在 Windows Vista 之前，前缀解析操作有两个用途：

-   导致前缀解析的基于名称的操作将被路由到声明前缀的提供程序。 如果成功，MUP 将确保后续的基于句柄的操作 (IRP \_ mj \_ 读取和 IRP \_ mj \_ 写入，例如) 完全跳到相同的提供程序。

-   该提供程序及其声明的前缀在由 MUP 维护的前缀缓存中输入。 对于后续的基于名称的操作，MUP 使用此前缀缓存来确定提供程序在尝试执行前缀解析之前是否已经声明了前缀。 此前缀缓存中的每个条目都受超时 (在添加到缓存后称为 TTL) 。 此超时到期后，将会丢弃某个条目，此时，MUP 会对后续基于名称的操作再次执行前缀解析。

MUP 通过向使用 MUP 注册的网络重定向程序发出 [**IOCTL \_ REDIR \_ 查询 \_ 路径**](/windows-hardware/drivers/ddi/ntifs/ni-ntifs-ioctl_redir_query_path) 请求来执行前缀解析。 IOCTL \_ REDIR 查询路径的输入和输出缓冲区如下所示 \_ \_ ：

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
<td align="left"><p>IrpSp- &gt; DeviceIoControl. Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>输出缓冲区</strong></p></td>
<td align="left"><p>IRP- &gt; UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL 和数据结构在 *ntifs*中定义。 缓冲区是从非分页池分配的。

网络重定向程序应仅允许此 IOCTL 的内核模式发送方，验证 IRP 结构的 **RequesterMode** 成员是否为 **KernelMode**。

MUP 使用 \_ 请求信息的查询路径 \_ 请求数据结构。

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
<th align="left">说明</th>
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
<td align="left"><p>格式为 &lt; 服务器 &gt; &lt; 共享 &gt; &lt; 路径 &gt; 的非 NULL 终止的 Unicode 字符串。 字符串的长度（以字节为单位）由 <strong>PathNameLength</strong> 成员指定。</p></td>
</tr>
</tbody>
</table>



UNC 提供程序应 \_ \_ 为响应信息使用查询路径响应数据结构。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>LengthAccepted</strong></p></td>
<td align="left"><p>提供程序从 QUERY_PATH_REQUEST 结构的 <strong>FilePathName</strong> 成员中指定的 Unicode 字符串路径的前缀的长度（以字节为单位）。</p></td>
</tr>
</tbody>
</table>



请注意，IOCTL \_ REDIR \_ 查询 \_ 路径是一种不是 ioctl 的方法 \_ 。 这意味着输入缓冲区和输出缓冲区可能不在同一地址。 UNC 提供程序的一个常见错误是假定输入缓冲区和输出缓冲区相同，并使用输入缓冲区指针来提供响应。

当 UNC 提供程序收到 IOCTL \_ REDIR \_ 查询 \_ 路径请求时，必须确定该提供程序是否可以处理查询路径请求结构的 **FilePathName** 成员中指定的 UNC \_ 路径 \_ 。 如果是这样，则必须**LengthAccepted** \_ \_ 用它所声明的前缀的长度（以字节为单位）更新查询路径响应结构的 LengthAccepted 成员，并完成 IRP 状态为 "成功" \_ 的操作。 如果提供程序无法处理指定的 UNC 路径，则它必须使 IOCTL \_ REDIR \_ 查询 \_ 路径请求失败并提供相应的 NTSTATUS 错误代码，并且不得**LengthAccepted**更新查询 \_ 路径响应结构的 LengthAccepted 成员 \_ 。 提供程序不能修改任何其他成员或任何条件下的 **FilePathName** 字符串。

如果 \\ \\ \\ 在对 IRP MJ 创建或其他使用 UNC 名称的 irp 的响应中无法识别服务器共享前缀名称 \_ \_ ，则建议返回的 NTSTATUS 代码是以下各项之一：

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>状态 \_ 错误的 \_ 网络 \_ 路径  
找不到网络路径。 计算机名称 (\\ \\ server) 无效，或者网络重定向程序无法使用任何可用的名称解析机制) 解析计算机 (名称。

<span id="STATUS_BAD_NETWORK_NAME"></span><span id="status_bad_network_name"></span>状态 \_ 错误的 \_ 网络 \_ 名称  
在远程服务器上找不到指定的共享名。 计算机名称 (\\ \\ server，例如) 有效，但在远程服务器上找不到指定的共享名。

<span id="STATUS_INSUFFICIENT_RESOURCES"></span><span id="status_insufficient_resources"></span>状态 \_ \_ 资源不足  
没有足够的资源可用于为缓冲区分配内存。

<span id="STATUS_INVALID_DEVICE_REQUEST"></span><span id="status_invalid_device_request"></span>状态 \_ 无效的 \_ 设备 \_ 请求  
IOCTL \_ REDIR \_ 查询 \_ 路径请求应仅来自 MUP，而 IRP 的请求者模式应始终为 **KernelMode**。 如果调用线程的请求者模式没有 **KernelMode**，则返回此错误代码。

<span id="STATUS_INVALID_PARAMETER"></span><span id="status_invalid_parameter"></span>状态 \_ 无效 \_ 参数  
查询路径请求结构中的 **PathNameLength** 成员 \_ 超出了 \_ unicode 字符串允许的最大长度，即 unicode \_ 字符串 \_ 最大 \_ 字节数。

<span id="STATUS_LOGON_FAILURE_or_STATUS_ACCESS_DENIED"></span><span id="status_logon_failure_or_status_access_denied"></span><span id="STATUS_LOGON_FAILURE_OR_STATUS_ACCESS_DENIED"></span>状态 \_ 登录 \_ 失败或状态 \_ 访问 \_ 被拒绝  
如果前缀解析操作由于无效或不正确的凭据而失败，则提供程序应返回远程服务器返回的确切错误代码;这些错误代码不能转换为 " \_ 错误的 \_ 网络 \_ 名称" 或 \_ " \_ 错误 \_ 的网络路径" 状态。 错误代码（如状态 \_ 登录 \_ 失败和 \_ 状态 \_ 拒绝访问）充当用户的反馈机制，指示要求使用适当的凭据。 在某些情况下，也使用这些错误代码来自动提示用户输入凭据。 如果没有这些错误代码，用户可能会认为计算机无法访问。

如果网络重定向程序无法解析前缀，则它必须返回与上述建议的 NTSTATUS 代码列表中的预期语义最为匹配的 NTSTATUS 代码。 网络重定向程序不得返回实际遇到的错误 (状态 \_ 连接 \_ 被拒绝，例如，如果 NTSTATUS 代码不在上面的列表中，则直接) 。

提供程序声明的前缀长度取决于单个 UNC 提供程序。 大多数提供商通常会声明 "服务器名称共享名" 路径 \\ \\ &lt; &gt; \\ &lt; &gt; 形式路径的 servername 共享部分 \\ \\ &lt; &gt; \\ &lt; &gt; \\ &lt; &gt; 。 例如，如果提供程序在 \\ \\ \\ 给定 path server public dir1 dir2 的情况下声明了服务器公共 \\ \\ \\ \\ \\ ，则前缀 (服务器的所有基于名称的操作都将 \\ \\ \\ \\ \\ \\ 被自动路由到该提供程序) ，而不会进行任何前缀解析，因为前缀已在前缀缓存中。 但是，带有前缀 \\ 服务器 \\ 市场营销演示的路径 \\ 将通过前缀解析。

如果网络重定向程序将服务器名称声明 (\\ \\ 服务器，例如) ，则此服务器上的所有共享请求都将发送到此网络重定向程序。 仅当其他网络重定向程序无法访问同一服务器上的另一个共享时，此行为才是可接受的。 例如，使用 \\ \\ UNC 路径的服务器的网络重定向器将阻止其他网络重定向器访问此服务器上的其他共享 (WebDAV 访问 \\ \\ 服务器 \\ 网络，例如) 。

任何传统的网络重定向程序 (不基于使用通过 [**FsRtlRegisterUncProvider**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider) 注册为 UNC 提供程序的 RDBSS) 将接收 IOCTL \_ REDIR \_ 查询 \_ 路径请求。

表示支持的网络微型重定向程序将接收此前缀声明，就像它是 IRP \_ MJ \_ CREATE 调用一样。 此创建请求类似于**Createfile** \_ \_ \_ 在上设置了文件创建树连接标志的用户模式 Createfile 调用。 网络小型重定向程序将不会接收前缀声明作为对[**MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL \] **](./mrxlowiosubmit-lowio-op-ioctl-.md)的调用。 对于前缀声明，RDBSS 会将 [**MRxCreateSrvCall**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall) 请求发送到网络小型重定向程序，然后调用 [**MRxSrvCallWinnerNotify**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify) 和 [**MRxCreateVNetRoot**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)。 当网络微重定向器注册到 RDBSS 时，网络小型重定向器的驱动程序调度表将由 RDBSS 复制到指向内部 RDBSS 入口点。 然后，RDBSS 将 \_ \_ \_ 为网络小型重定向器在内部接收此 IOCTL REDIR 查询路径，并调用 **MRxCreateSrvCall**、 **MRxSrvCallWinnerNotify**和 **MRxCreateVNetRoot**。 原始 IOCTL \_ REDIR \_ 查询 \_ 路径 IRP 将包含在 \_ 传递到 **MRxCreateSrvCall** 例程的 RX 上下文结构中。 此外， \_ 将修改传递到 **MRXCREATESRVCALL** 的 RX 上下文中的以下成员：

**MajorFunction** \_ \_ 即使原始 IRP 为 irp \_ mj \_ 设备 \_ 控制，MajorFunction 成员也会设置为 irp mj CREATE。

**PrefixClaim**成员设置为查询**FilePathName** \_ 路径请求结构的 FilePathName 成员 \_ 。

**PrefixClaim**成员设置为查询**PathNameLength** \_ 路径请求结构的 PathNameLength 成员 \_ 。

**NtCreateParameters. SecurityContext**成员设置为查询**SecurityContext** \_ 路径请求结构的 SecurityContext 成员 \_ 。

**ThisIsATreeConnectOpen**成员设置为**TRUE**。

**Create Flags**成员具有 RX \_ 上下文 \_ 创建 \_ 标志 \_ UNC \_ 名称位集。

如果网络小型重定向程序想要查看前缀声明的详细信息，则可以读取 \_ 传递给 **MRXCREATESRVCALL**的 RX 上下文中的这些成员。 否则，它只会尝试连接到服务器共享，并 \_ 在 **MRxCreateSrvCall** 调用成功时返回状态 SUCCESS。 RDBSS 将代表网络小型重定向器发出前缀声明。

在这种情况下，网络小型重定向器可以直接接收此 IOCTL。 网络小型重定向程序可以在初始化并注册到 RDBSS 之前保存其驱动程序调度表的副本。 在调用 [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr) 以向 RDBSS 注册后，网络小型重定向程序可以保存由 RDBSS 安装的新驱动程序调度表入口点的副本，并还原其原始驱动程序调度表。 需要对还原的驱动程序调度表进行修改，以便在为网络微型重定向程序所需的目标检查收到的 IRP 后，调用将转发到 RDBSS 驱动程序调度入口点。 当驱动程序初始化 RDBSS 并调用 **RxRegisterMinrdr**时，RDBSS 将复制网络小型重定向程序的驱动程序调度表。 链接到*rdbsslib*的网络微重定向程序必须先保存其原始驱动程序调度表，然后再从其**DriverEntry**例程调用[**RxDriverEntry**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry) ，以便在调用**RxRegisterMinrdr**后初始化 RDBSS 静态库并还原其驱动程序调度表。 这是因为 RDBSS 会在 **RxDriverEntry** 和 **RxRegisterMinrdr** 例程中通过网络小型重定向器发送表进行复制。

在前缀解析过程中查询提供程序的顺序由 \_ 存储在以下注册表项下的注册表值控制：

```cpp
HKLM\System\CurrentControlSet\Control\NetworkProvider\Order
```

ProviderOrder 注册表值中的单个提供程序名称以逗号分隔，不包含任何前导或尾随空格。

例如，此值可能包含字符串：

```cpp
RDPNP,LanmanWorkstation,WebClient
```

给定 UNC 路径 \\ \\ &lt; 服务器 &gt; \\ &lt; 共享 &gt; \\ &lt; 路径 &gt; ，如果 (服务器共享或服务器的前缀，则 mup 发出前缀解析请求 \\ \\ \\ \\ \\ ，例如) 在 MUP 前缀缓存中找不到。 MUP 按以下顺序向每个提供程序发送前缀解析请求，直到提供程序声明前缀 (或已) 查询所有提供程序：

1.  TS 客户端 (RDPNP) 

2.  SMB 重定向程序 (LanmanWorkstation) 

3.  WebDAV 重定向程序 (WebClient) 

更改 ProviderOrder 注册表值需要重新启动才能在 Windows Server 2003、Windows XP 和 Windows 2000 上的 MUP 中生效。

MUP 使用列出的每个提供程序名称来查找以下注册表项下的提供程序的注册表项：

```cpp
HKLM\System\CurrentControlSet\Services\<ProviderName>
```

MUP 然后读取 NetworkProvider 子项下的 DeviceName 值以查找提供程序将注册的设备名称。 当提供程序实际注册时，MUP 会将传入的设备名称与已知提供程序的设备名称列表相匹配，并将提供程序置于排序列表中以用于前缀解析。 此列表中提供程序的顺序基于前面讨论的 ProviderOrder 注册表值中指定的顺序。

请注意，此提供程序顺序也由多提供商路由器 (MPR) ，这是基于 WNet 提供程序的查询建立网络连接的用户模式 DLL。

在带有 service pack 1 和 Windows XP Service Pack 2 的 Windows Server 2003 之前，MUP 行为是按 ProviderOrder 注册表值中指定的顺序向所有提供程序 "并行" 发出前缀解析请求，然后等待所有提供程序完成前缀解析操作。 因此，即使第一个提供程序声明了前缀，MUP 仍会等待所有其他提供程序完成前缀解析操作。 当多个提供程序使用前缀声明进行响应时，MUP 会根据在 ProviderOrder 注册表值中指定的顺序选择该提供程序。

在 Windows XP Service Pack 2 和更高版本以及 Windows Server 2003 Service Pack 1 及更高版本中，此行为略有变化。 MUP 按顺序发出前缀解析请求，并在第一个提供程序声明前缀时立即停止。 因此，在上述示例中，如果 RDPNP 声明了前缀，则 MUP 将不会调用 SMB 或 WebDAV 重定向器。

此行为的主要原因是 "串行前缀解析" 方案阻止了 ProviderOrder 值中优先级较低的网络重定向程序的事例，导致 ProviderOrder 值中优先级较高的网络重定向器出现性能问题。 例如，假设有一个使用防火墙的远程服务器，配置为阻止特定类型的 TCP/IP 数据包 (对 HTTP 的访问，例如) ，但允许其他人 (SMB 访问，例如) 。 在这种情况下，即使 SMB 网络重定向程序配置为 ProviderOrder 值中的第一个提供程序并快速声明前缀，WebDAV 重定向程序可能会通过等待 TCP 连接超时来大幅延迟完成前缀解析。