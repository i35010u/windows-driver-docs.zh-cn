---
title: 在 Microsoft Windows Vista MUP 更改
description: 在 Microsoft Windows Vista MUP 更改
ms.assetid: 8ca2f9bc-14f1-45d3-a397-f3e5459cf8ec
keywords:
- 内核网络重定向程序 WDK MUP
- MUP WDK 网络重定向程序
- 多个 UNC 提供程序 WDK 网络重定向程序
- UNC WDK 网络重定向程序
- 内核网络重定向程序 WDK，Windows Vista 重定向程序模型
- 旧版重定向程序 WDK 文件系统
- 前缀解析 WDK 网络重定向程序
- 前缀缓存 WDK 网络重定向程序
- 双精度筛选 WDK 网络重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45524f2823bda74db343326487a536f2a4014b12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522466"
---
# <a name="mup-changes-in-microsoft-windows-vista"></a>在 Microsoft Windows Vista MUP 更改


Windows Vista 实现多个对多个可能会影响网络重定向程序 UNC provider (MUP) 的更改。

MUP 和分布式文件系统 (DFS) 客户端是在单独的二进制文件。 MUP 组件是 mup.sys 中和 DFS 客户端位于 dfsc.sys。 在 Windows Server 2003，Windows XP 和 Windows 2000，MUP 内核组件、 mup.sys，也包含 DFS 客户端。

在 Windows Vista 上定义新的重定向程序模型：

-   将注册为与 I/O 管理器的文件系统的 MUP 通过调用[ **IoRegisterFileSystem**](https://msdn.microsoft.com/library/windows/hardware/ff548494)。

-   网络重定向程序注册使用 MUP [ **FsRtlRegisterUncProviderEx** ](https://msdn.microsoft.com/library/windows/hardware/ff547184) ，在 Windows Vista 中引入的新例程。

-   网络重定向程序未命名的设备将对象传递给[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)。

-   网络重定向器将传递到的设备名称[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)。

-   网络重定向程序不会注册为文件系统与 I/O 管理器 (不会调用[ **IoRegisterFileSystem**](https://msdn.microsoft.com/library/windows/hardware/ff548494))。

-   从 MUP 网络重定向程序，包括前缀解析、 Ioctl 和 FSCTLs，到的所有调用都都是使用启用的 Apc。 从其他组件对 MUP 的所有调用都需要使用已启用的 Apc 来进行。 将用于调用[ **FsRtlCancellableWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff545738)或[ **FsRtlCancellableWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff545731)，新在 Windows Vista 中引入的例程，这样可以确保如果发出 I/O 请求的线程终止，可以中止长时间等待。

-   前缀解析执行使用 IOCTL\_是否重定向\_查询\_路径\_EX、 在 Windows Vista 中引入新 IOCTL。

-   注册到 MUP 网络重定向程序设备名称将成为到 MUP 设备对象的符号链接。

对于 Windows Vista 重定向程序模型符合网络重定向程序，MUP 创建符号链接对象管理器命名空间中通过网络重定向程序对的调用中指定的设备名称[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)。 此符号链接的目标是 MUP 设备对象 (\\设备\\Mup)。

文件系统和网络重定向程序正在 MUP 设备对象的符号链接的设备名称注册 MUP 的优点是所有远程文件系统 I/O 操作，并不只基于名称的操作经过 MUP。 因此文件系统筛选器驱动程序的需要是远程文件系统堆栈上可以只需将附加到 MUP 设备对象中。 它不是必需的文件系统筛选器驱动程序进行硬编码提供程序设备对象名称 (\\设备\\LanmanRedirector，例如) 到了其驱动程序。 在这种方式，文件系统筛选器驱动程序可以监视由单个附件颁发给所有网络重定向程序的所有 I/O 操作。 这还消除了重复的文件系统筛选器驱动程序在 Windows Vista，单独连接到 DFS (mup.sys) 和单个网络重定向之前看到的 I/O 操作 (\\设备\\LanmanRedirector，例如) 中监视对 I/O 操作的顺序。

附加到 MUP 设备对象的文件系统筛选器驱动程序可以有选择地筛选发送到特定网络重定向的流量。 在这种情况下，筛选器驱动程序映射的网络重定向程序感兴趣的设备名称到提供程序标识符通过调用[ **FsRtlMupGetProviderIdFromName** ](https://msdn.microsoft.com/library/windows/hardware/ff546971)例程。 然后，筛选器驱动程序可以确定它是否应通过比较通过调用获取的提供程序标识符筛选特定文件对象的流量[ **FsRtlMupGetProviderInfoFromFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff546981)例程替换感兴趣的网络控制器的提供程序标识符。

有关 Windows Vista 重定向程序模型符合网络重定向程序：

-   远程文件系统堆栈上的所有文件对象都解析为 MUP。 因此， [ **IoGetDeviceAttachmentBaseRef** ](https://msdn.microsoft.com/library/windows/hardware/ff548365) MUP，不网络重定向程序拥有的文件对象返回的设备对象。 但是，仍由网络重定向程序拥有的文件对象的内容。

-   IRP\_MJ\_创建颁发给网络重定向程序的设备名称 (\\设备\\LanmanRedirector\\server\\共享，例如) 将加载到该网络重定向程序目标而无需通过 MUP 前缀解析，按照其处于 Windows Server 2003、 Windows XP 和 Windows 2000。

不基于 Windows Vista RDBSS （动态或静态链接） 的网络重定向程序分别称为"旧版重定向程序"。 这些旧的网络重定向程序包括：

-   网络重定向程序编写的 Windows Server 2003、 Windows XP 和 Windows 2000 的 MUP 使用直接注册[ **FsRtlRegisterUncProvider**](https://msdn.microsoft.com/library/windows/hardware/ff547178)。

-   最小-重定向程序编写的 Windows Server 2003、 Windows XP 和 Windows 2000，以静态方式与 rdbsslib.lib 库链接的 Windows Server 2003、 Windows XP 或 Windows 2000 的网络。

-   网络的重定向器为 Windows Vista 编写直接注册使用 MUP [ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)。

网络微型-重定向程序动态自动链接针对 Windows Vista RDBSS (rdbss.sys) 的符合到 Windows Vista 重定向程序模型，因为 MUP 使用注册 RDBSS [ *FsRtlRegisterUncProviderEx*](https://msdn.microsoft.com/library/windows/hardware/ff547184). 网络微型-重定向程序，以静态方式还会自动针对 Windows Vista RDBSS (rdbsslib.lib) 链接到 Windows Vista 重定向程序模型符合，因为 MUP 使用注册 RDBSS **FsRtlRegisterUncProviderEx**.

为直接向 MUP 注册的 Windows Vista 编写的旧版网络重定向程序必须符合 Windows Vista 重定向程序模型。

网络重定向程序编写的 Windows Server 2003、 Windows XP 和 Windows 2000 向注册的直接使用 MUP [ **FsRtlRegisterUncProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff547178)继续工作的方式，就像在 Windows Server 2003、 Windows XP 和 Windows 2000。 最小-重定向程序编写的 Windows Server 2003、 Windows XP 和 Windows 2000 的 Windows Server 2003、 Windows XP 和 Windows 2000 继续工作的方式，就像在 Windows Server 2003 上，与 rdbsslib.lib 库静态链接的网络Windows XP 和 Windows 2000。 这些旧的网络重定向程序和最小重定向程序会表现出的以下行为：

-   它们将显示文件系统筛选器驱动程序的监视文件系统注册。

-   其设备对象的命名。 设备名称不是符号链接和未指向\\设备\\MUP。

-   文件对象解析网络重定向程序指定的设备对象。

-   MUP 仅参与前缀解析操作。 一旦确定网络提供商，MUP"开"通过获取返回状态\_重新分析。 所有后续操作将不能通过 MUP。

此行为已被保留，以便防止 double 筛选如果提供程序设备名称的符号链接发生\\设备\\MUP。 由于以下原因，此双筛选会发生：

-   文件系统筛选器驱动程序已附加到\\设备\\MUP。

-   文件系统筛选器驱动程序将附加到任何注册的文件系统。 自网络重定向程序，使用命名的设备对象本身注册为文件系统的文件系统筛选器驱动程序将最终会两次筛选相同 I/O。

调用与在 Windows Vista MUP 都是使用 Apc 启用，这将产生以下影响：

-   务必要保护，如果需要，代码路径获取从 MUP 针对调用线程暂停通过适当的方式，尤其是 IOCTL\_是否重定向\_查询\_路径处理程序。 请注意，一个线程挂起是可能"无限制的等待"操作可以持续很长时间。

-   请务必确保任何始终涉及用户模式线程 （而不是系统线程） 的"等待 I/O"操作，使用"可取消等待"。 请参阅[ **FsRtlCancellableWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff545738)并[ **FsRtlCancellableWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff545731)例程的详细信息。

-   当一个线程获取挂起持有一些重要的锁时，可能会发生死锁。 请务必运行出现用户模式线程获取任意挂起检查死锁条件的测试。

-   务必要运行测试来验证是否"等待 I/O 操作"是否真正可取消，并在用户模式应用程序可以足够快的速度终止线程，以便应用程序似乎不处于"非响应"状态时尝试终止所述的线程。

前缀的缓存大小和超时由在 Windows Vista MUP 现在由以下注册表值控制：

-   PrefixCacheSizeInKB

-   PrefixCacheTimeoutInSeconds。

可以动态更改这些注册表值，而无需重新启动。 这些注册表值是以下注册表项下：

```cpp
HKLM\System\CurrentControlSet\Services\Mup\Parameters.
```

可以动态更改 ProviderOrder 注册表值，该值确定在哪些 MUP 问题的前缀解析请求到单个重定向程序的顺序，而无需重新启动系统。 此注册表值位于以下注册表项下：

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

在 Windows Vista MUP 执行以不同的方式取决于是否网络重定向程序注册到 MUP 通过调用的前缀解析[ **FsRtlRegisterUncProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff547178)或[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)。 旧版网络重定向程序，通过调用注册 MUP **FsRtlRegisterUncProvider**将收到[ **IOCTL\_是否重定向\_查询\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff548313)前缀解析请求。 这是 Windows Server 2003、 Windows XP 和 Windows 2000 使用的相同方法。

网络重定向程序的符合 Windows Vista 重定向程序模型，并通过调用注册 MUP [ **FsRtlRegisterUncProviderEx** ](https://msdn.microsoft.com/library/windows/hardware/ff547184)将收到[ **IOCTL\_是否重定向\_查询\_路径\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff548320)前缀解析请求。 请注意，在 Windows Vista 中，网络微型-重定向程序与 rdbsslib.lib 以静态方式链接或与 rdbss.sys 动态链接将调用**FsRtlRegisterUncProviderEx** RDBSS 通过间接。

IOCTL 的输入和输出缓冲区\_是否重定向\_查询\_路径\_EX 如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left">参数可在</td>
<td align="left">数据结构格式</td>
</tr>
<tr class="even">
<td align="left"><p>输入的缓冲区</p></td>
<td align="left"><p>IrpSp-&gt; Parameters.DeviceIoControl.Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST_EX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>输出缓冲区</p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL 和数据结构 ntifs.h 中定义。 从非分页缓冲池分配缓冲区。

网络重定向程序应仅使用内核模式发件人的此 IOCTL，只需验证**Irp-&gt;RequestorMode**是**KernelMode**。

MUP 使用查询\_路径\_请求\_EX 请求信息的数据结构。

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
<td align="left"><p>指向的安全上下文的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>EaLength</strong></p></td>
<td align="left"><p>扩展的属性缓冲区长度 （字节）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>pEaBuffer</strong></p></td>
<td align="left"><p>扩展的属性缓冲区的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>PathName</strong></p></td>
<td align="left"><p>以非 NULL 结尾的 Unicode 字符串的窗体&amp;l t; 服务器&gt;&amp;l t; 共享&gt;&amp;l t; 路径&gt;。</p></td>
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
<td align="left"><p>提供程序中指定的 Unicode 字符串路径从声明的前缀长度，以字节为单位， <strong>PathName</strong> QUERY_PATH_REQUEST_EX 结构中的成员。</p></td>
</tr>
</tbody>
</table>



请注意该 IOCTL\_是否重定向\_查询\_路径\_EX 是一种方法\_既不 IOCTL。 这意味着输入和输出缓冲区可能无法在相同的地址。 通过 UNC 提供程序的一个常见错误是假定输入的缓冲区和输出缓冲区是相同的并且使用输入的缓冲区指针来提供响应。

当 UNC 提供程序收到 IOCTL\_是否重定向\_查询\_路径\_EX 请求，它必须确定它是否可以处理中指定的 UNC 路径**路径名**查询的成员\_路径\_请求\_EX 结构。 如果这样，UNC 提供程序必须更新**LengthAccepted**查询的成员\_路径\_响应结构，它已在使用和完成状态IRP的前缀长度，以字节为单位，\_成功。 如果提供程序无法处理指定的 UNC 路径，则必须失败 IOCTL\_是否重定向\_查询\_路径\_EX 请求并返回相应的 NTSTATUS 错误代码并不能更新**LengthAccepted**查询的成员\_路径\_响应结构。 提供程序不能修改任何其他成员或**PathName**在任何情况下的字符串。

在 Windows Vista 中，网络微型重定向以使用 RDBSS，该值指示支持 UNC 提供程序会收到此前缀声明，就像常规树连接基础创建，类似于文件的用户模式下 Createfile 调用\_创建\_树\_连接标志设置。 将发送 RDBSS [ **MRxCreateSrvCall** ](https://msdn.microsoft.com/library/windows/hardware/ff549864)网络微型重定向到的调用后跟对请求[ **MRxSrvCallWinnerNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff550824)并[ **MRxCreateVNetRoot**](https://msdn.microsoft.com/library/windows/hardware/ff549869)。 此前缀声明不会收到与调用[ **MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](https://msdn.microsoft.com/library/windows/hardware/ff550715)。 当网络微型重定向注册与 RDBSS 时，网络微型重定向的驱动程序调度表将被复制转移 RDBSS 为指向内部 RDBSS 入口点。 RDBSS 然后接收此 IOCTL\_是否重定向\_查询\_路径\_在内部用于网络微型重定向和调用 EX **MRxCreateSrvCall**， **MRxSrvCallWinnerNotify**，并**MRxCreateVNetRoot**。 原始 IOCTL\_是否重定向\_查询\_路径\_EX IRP 将包含在 RX\_上下文传递给**MRxCreateSrvCall**例程。 此外，RX 中的以下成员\_上下文传递给**MRxCreateSrvCall**将进行相应修改：

**MajorFunction**成员设置为 IRP\_MJ\_创建即使原始 IRP 是 IRP\_MJ\_设备\_控件。

**PrefixClaim.SuppliedPathName.Buffer**成员设置为**PathName.Buffer**查询的成员\_路径\_请求\_EX 结构。

**PrefixClaim.SuppliedPathName.Length**成员设置为**PathName.Length**查询的成员\_路径\_请求\_EX 结构。

**Create.ThisIsATreeConnectOpen**成员设置为**TRUE**。

**Create.ThisIsAPrefixClaim**成员设置为**TRUE**。

**Create.NtCreateParameters.SecurityContext**成员设置为**SecurityContext**查询的成员\_路径\_请求\_EX 结构。

**Create.EaBuffer**成员设置为**pEaBuffer**查询的成员\_路径\_请求\_EX 结构。

**Create.EaLength**成员设置为**EaLength**查询的成员\_路径\_请求\_EX 结构。

**Create.Flags**成员将具有 RX\_上下文\_创建\_标志\_UNC\_名称位集。

如果网络微型-重定向程序想要查看的前缀声明的详细信息，它可以读取这些成员中 RX\_上下文结构传递给[ **MRxCreateSrvCall**](https://msdn.microsoft.com/library/windows/hardware/ff549864)。 否则，它可以只是尝试连接到服务器共享，并返回状态\_成功如果**MRxCreateSrvCall**调用是否成功。 RDBSS 将代表网络声明的前缀微型重定向。








