---
title: Microsoft Windows Vista 中的 MUP 更改
description: Microsoft Windows Vista 中的 MUP 更改
ms.assetid: 8ca2f9bc-14f1-45d3-a397-f3e5459cf8ec
keywords:
- 内核网络重定向 WDK，MUP
- MUP WDK 网络重定向器
- 多 UNC 提供程序 WDK 网络重定向程序
- UNC WDK 网络重定向器
- 内核网络重定向程序 WDK，Windows Vista 重定向程序模型
- 旧重定向器 WDK 文件系统
- 前缀解析 WDK 网络重定向器
- 前缀缓存 WDK 网络重定向器
- 双重筛选 WDK 网络重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b00c81dc2705d811708d1c183bcfb04a29ca18a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841059"
---
# <a name="mup-changes-in-microsoft-windows-vista"></a>Microsoft Windows Vista 中的 MUP 更改


Windows Vista 实现了对多 UNC 提供程序（MUP）的许多更改，这些更改可能会影响网络重定向程序。

MUP 和分布式文件系统（DFS）客户端位于单独的二进制文件中。 MUP 组件在 mup 中，DFS 客户端在 dfsc 中。 在 Windows Server 2003、Windows XP 和 Windows 2000 上，MUP 内核组件 mup 也包含 DFS 客户端。

在 Windows Vista 上定义了新的重定向程序模型：

-   MUP 使用 i/o 管理器通过调用[**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)注册为文件系统。

-   网络重定向程序使用[**FsRtlRegisterUncProviderEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex) （Windows Vista 中引入的新例程）注册 MUP。

-   网络重定向程序将未命名的设备对象传递到[**FsRtlRegisterUncProviderEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)。

-   网络重定向程序将设备名称传递到[**FsRtlRegisterUncProviderEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)。

-   网络重定向程序不会使用 i/o 管理器注册为文件系统（不会调用[**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)）。

-   从 MUP 到网络重定向程序的所有调用（包括前缀解析、IOCTLs 和 FSCTLs）都是在启用 Apc 的情况下进行的。 所有从其他组件到 MUP 的调用都预计会在启用 Apc 的情况中进行。 当调用与[**FsRtlCancellableWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff545738)或[**FsRtlCancellableWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff545731)一起使用时，在 Windows Vista 中引入的新例程将确保当发出 i/o 请求的线程早.

-   前缀解析是使用 IOCTL\_REDIR\_QUERY\_路径\_EX （Windows Vista 中引入的新 IOCTL）执行的。

-   使用 MUP 注册的网络重定向器设备名称成为 MUP 设备对象的符号链接。

对于符合 Windows Vista 重定向程序模型的网络重定向程序，MUP 在对象管理器命名空间中创建一个符号链接，并在调用[**FsRtlRegisterUncProviderEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)时使用网络重定向程序指定的设备名称。 此符号链接的目标是 MUP 设备对象（\\设备\\Mup）。

将 MUP 注册为文件系统，并将网络重定向器的设备名称注册为 MUP 设备对象的符号链接的优点是：所有远程文件系统 i/o 操作（而不只是基于名称的操作）都要经历 MUP。 因此，需要位于远程文件系统堆栈上的文件系统筛选器驱动程序只需附加到 MUP 设备对象即可。 文件系统筛选器驱动程序不再需要硬编码提供程序设备对象名称（例如\\设备\\LanmanRedirector）。 通过这种方式，文件系统筛选器驱动程序可以通过单个附件监视颁发给所有网络重定向程序的所有 i/o 操作。 这还消除了 Windows Vista 之前的文件系统筛选器驱动程序（例如，单独附加到 DFS （mup）和单个网络重定向程序（例如\\设备\\LanmanRedirector）所发现的重复 i/o 操作，以便监视对两者的 i/o 操作。

附加到 MUP 设备对象的文件系统筛选器驱动程序可以有选择地筛选发送到特定网络重定向程序的流量。 在这种情况下，筛选器驱动程序通过调用[**FsRtlMupGetProviderIdFromName**](https://msdn.microsoft.com/library/windows/hardware/ff546971)例程将相关网络重定向器的设备名称映射到提供程序标识符。 然后，筛选器驱动程序可以通过比较通过使用提供程序标识符调用[**FsRtlMupGetProviderInfoFromFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff546981)例程获取的提供程序标识符，来确定它是否应筛选特定文件对象的流量相关的网络控制器。

对于符合 Windows Vista 重定向程序模型的网络重定向程序：

-   远程文件系统堆栈上的所有文件对象都解析为 MUP。 因此， [**IoGetDeviceAttachmentBaseRef**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetdeviceattachmentbaseref)返回 MUP 的设备对象，而不是拥有该文件对象的网络重定向程序。 但文件对象的内容仍由网络重定向器拥有。

-   颁发给网络重定向程序的设备名称的 IRP\_MJ\_创建（例如，\\设备\\LanmanRedirector\\server\\共享）将以该网络重定向程序为目标，而无需通过 MUP 前缀解决方法与 Windows Server 2003、Windows XP 和 Windows 2000 完全相同。

不基于 Windows Vista RDBSS （动态或静态链接）的网络重定向程序称为 "旧重定向程序"。 这些旧的网络重定向器包括：

-   为 Windows Server 2003、Windows XP 和 Windows 2000 编写的网络重定向器，使用[**FsRtlRegisterUncProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider)直接注册了 MUP。

-   为 Windows Server 2003、Windows XP 和 Windows 2000 编写的网络微重定向程序，它以静态方式链接到 Windows Server 2003、Windows XP 或 Windows 2000 的 rdbsslib 库。

-   为使用[**FsRtlRegisterUncProviderEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)直接注册到 MUP 的 Windows Vista 编写的网络重定向程序。

动态链接到 Windows Vista RDBSS （RDBSS）的网络微型重定向程序自动符合 Windows Vista 重定向程序模型，因为 RDBSS 使用[*FsRtlRegisterUncProviderEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)注册 MUP。 静态链接到 Windows Vista RDBSS （rdbsslib）的网络微型重定向程序也自动符合 Windows Vista 重定向程序模型，因为 RDBSS 使用**FsRtlRegisterUncProviderEx**注册 MUP。

为直接注册到 MUP 的 Windows Vista 编写的旧版网络重定向程序必须符合 Windows Vista 重定向程序模型。

为 Windows Server 2003、Windows XP 和 Windows 2000 编写的网络重定向器直接使用[**FsRtlRegisterUncProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider)与在 windows server 2003、windows Xp 和 windows 2000 上的运行方式完全相同。 为 Windows Server 2003、windows XP 和 windows 2000 编写的、与 Windows Server 2003、Windows XP 和 Windows 2000 的 rdbsslib 库静态链接的网络微重定向器的工作方式与在 Windows Server 2003 上的运行方式完全相同，Windows XP 和 Windows 2000。 这些旧的网络重定向程序和微型重定向器会出现以下行为：

-   它们将对监视文件系统注册的文件系统筛选器驱动程序可见。

-   其设备对象的名称为。 设备名称不是符号链接，不指向 \\设备\\MUP。

-   文件对象解析为网络重定向器的命名设备对象。

-   MUP 仅涉及前缀解析操作。 标识网络提供程序后，MUP "通过返回状态\_重新分析来进入。 所有后续操作都不会通过 MUP。

保留此行为是为了防止双重筛选，如果提供程序设备名称是指向 \\设备\\MUP 的符号链接，则会发生这种情况。 之所以发生这种双重筛选，原因如下：

-   文件系统筛选器驱动程序已附加到 \\设备\\MUP。

-   文件系统筛选器驱动程序会附加到任何注册的文件系统。 由于使用命名设备对象的网络重定向器会将其自身注册为文件系统，因此文件系统筛选器驱动程序将最终筛选相同的 i/o 两次。

在 Windows Vista 上，在 Windows Vista 上从 MUP 调用和，这会产生以下影响：

-   如果需要，可以根据具体的方法保护从 MUP 调用的代码路径，特别是\_REDIR\_查询\_路径处理程序。 请注意，线程挂起可能会持续很长时间。

-   务必确保涉及用户模式线程（而非系统线程）的任何 "等待 i/o" 操作始终使用 "可取消等待"。 有关详细信息，请参阅[**FsRtlCancellableWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff545738)和[**FsRtlCancellableWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff545731)例程。

-   当线程暂停持有某些重要的锁时，可能会发生死锁。 务必要运行测试，使挂起的用户模式线程随意检查是否存在死锁情况。

-   务必要运行测试来验证 "等待 i/o 操作" 是否确实是可取消的，以及用户模式应用程序是否可以快速终止线程，使应用程序在尝试时不会显示为 "未响应" 状态。终止被称为线程。

Windows Vista 上 MUP 使用的前缀缓存大小和超时现在由以下注册表值控制：

-   PrefixCacheSizeInKB

-   PrefixCacheTimeoutInSeconds.

无需重新启动即可动态更改这些注册表值。 这些注册表值位于以下注册表项下：

```cpp
HKLM\System\CurrentControlSet\Services\Mup\Parameters.
```

ProviderOrder 注册表值，它确定在不重新启动系统的情况下，可动态更改对各个重定向程序发出前缀解析请求的顺序。 此注册表值位于以下注册表项下：

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

在 Windows Vista 上，MUP 执行前缀解析的方式不同，具体取决于是否通过调用[**FsRtlRegisterUncProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider)或[**FsRtlRegisterUncProviderEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)向 MUP 注册了网络重定向程序。 通过调用**FsRtlRegisterUncProvider**向 MUP 注册的旧网络重定向器将接收[**IOCTL\_REDIR\_查询\_路径**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ni-ntifs-ioctl_redir_query_path)请求来解析前缀。 此方法与在 Windows Server 2003、Windows XP 和 Windows 2000 上使用的方法相同。

符合 Windows Vista 重定向程序模型并通过调用[**FsRtlRegisterUncProviderEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)进行注册的网络重定向器将接收[**IOCTL\_REDIR\_QUERY\_路径\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ni-ntifs-ioctl_redir_query_path_ex)前缀请求分辨率. 请注意，在 Windows Vista 上，使用 rdbsslib 静态链接的网络微型重定向程序或使用 rdbss 进行动态链接的将通过 RDBSS 间接调用**FsRtlRegisterUncProviderEx** 。

用于 IOCTL 的输入和输出缓冲区\_REDIR\_QUERY\_路径\_EX 如下：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left">可用参数于</td>
<td align="left">数据结构格式</td>
</tr>
<tr class="even">
<td align="left"><p>输入缓冲区</p></td>
<td align="left"><p>IrpSp-&gt; 参数. DeviceIoControl. Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST_EX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>输出缓冲区</p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL 和数据结构在 ntifs 中定义。 缓冲区是从非分页池分配的。

网络重定向器仅应通过验证**Irp&gt;irp->requestormode**是否**KernelMode**，来服从此 IOCTL 的内核模式发送方。

MUP 使用查询\_路径\_请求信息\_EX 数据结构。

```cpp
typedef struct _QUERY_PATH_REQUEST_EX {
  PIO_SECURITY_CONTEXT  pSecurityContext;
 ULONG  EaLength;
 PVOID  pEaBuffer;
  UNICODE_STRING  PathName;
} QUERY_PATH_REQUEST_EX, *PQUERY_PATH_REQUEST_EX;
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
<td align="left"><p><strong>pSecurityContext</strong></p></td>
<td align="left"><p>指向安全上下文的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>EaLength</strong></p></td>
<td align="left"><p>扩展属性缓冲区的长度（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>pEaBuffer</strong></p></td>
<td align="left"><p>指向扩展属性缓冲区的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>路径名</strong></p></td>
<td align="left"><p>&lt;server&gt;&lt;共享&gt;&lt;路径&gt;形式的非 NULL 终止 Unicode 字符串。</p></td>
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
<td align="left"><p>提供程序从 QUERY_PATH_REQUEST_EX 结构的<strong>PathName</strong>成员中指定的 Unicode 字符串路径的前缀的长度（以字节为单位）。</p></td>
</tr>
</tbody>
</table>



请注意，IOCTL\_REDIR\_QUERY\_路径\_EX 是两个不是 IOCTL 的\_方法。 这意味着输入缓冲区和输出缓冲区可能不在同一地址。 UNC 提供程序的一个常见错误是假定输入缓冲区和输出缓冲区相同，并使用输入缓冲区指针来提供响应。

当 UNC 提供程序接收 IOCTL\_REDIR\_查询\_路径\_EX 请求时，它必须确定它是否可以处理查询的**PathName**成员中指定的 UNC 路径\_\_请求\_构造. 如果是这样，UNC 提供程序必须以字节为单位，用它所声明的前缀的长度（以字节为单位）来更新\_\_查询的**LengthAccepted**成员，并完成状态为\_SUCCESS 的 IRP。 如果提供程序无法处理指定的 UNC 路径，则它必须使用适当的 NTSTATUS 错误代码将 IOCTL\_REDIR\_QUERY\_路径\_EX 请求，且不得更新查询的**LengthAccepted**成员\_路径\_响应结构。 在任何情况下，提供程序都不能修改任何其他成员或**路径名**字符串。

在 Windows Vista 上，基于使用 RDBSS 的网络微重定向程序将指示支持作为 UNC 提供程序将接收此前缀声明，就像使用 FILE\_CREATE\_@no__ 树的用户模式 Createfile 调用一样：已设置 t_2_ 连接标志。 RDBSS 会将[**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)请求发送到网络小型重定向程序，然后调用[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)和[**MRxCreateVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)。 在调用[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](https://msdn.microsoft.com/library/windows/hardware/ff550715)时，不会收到此前缀声明。 当网络微重定向器注册到 RDBSS 时，网络小型重定向器的驱动程序调度表将由 RDBSS 复制到指向内部 RDBSS 入口点。 然后，RDBSS 接收到此 IOCTL\_REDIR\_QUERY\_路径，\_内部网络小型重定向程序，并调用**MRxCreateSrvCall**、 **MRxSrvCallWinnerNotify**和**MRxCreateVNetRoot**。 原始 IOCTL\_REDIR\_查询\_路径\_EX IRP 将包含在传递到**MRxCreateSrvCall**例程的 RX\_上下文中。 此外，将修改传递到**MRxCreateSrvCall**的 RX\_上下文中的以下成员：

即使原始 IRP 为 IRP\_MJ\_设备\_控件， **MajorFunction**成员也设置为 IRP\_MJ\_CREATE。

将**PrefixClaim**成员设置为查询\_路径\_请求\_EX 结构的**PathName**成员。

将**PrefixClaim**成员设置为查询\_路径\_请求\_EX 结构的**PathName**成员。

**ThisIsATreeConnectOpen**成员设置为**TRUE**。

**ThisIsAPrefixClaim**成员设置为**TRUE**。

**SecurityContext**成员设置为\_\_EX 结构\_请求的查询的**SecurityContext**成员。

**EaBuffer**成员设置为查询\_路径\_请求\_EX 结构的**pEaBuffer**成员。

**EaLength**成员设置为查询\_路径\_请求\_EX 结构的**EaLength**成员。

**Create Flags**成员将具有 RX\_上下文\_创建\_\_UNC\_名称位集。

如果网络小型重定向程序想要查看前缀声明的详细信息，则可以读取 RX 中的这些成员\_传递给[**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)的上下文结构。 否则，它只会尝试连接到服务器共享，并在**MRxCreateSrvCall**调用成功时返回状态\_成功。 RDBSS 将代表网络小型重定向器发出前缀声明。








