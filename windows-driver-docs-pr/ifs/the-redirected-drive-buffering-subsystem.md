---
title: 重定向的驱动器缓冲子系统
description: 重定向的驱动器缓冲子系统
keywords:
- 网络重定向 WDK，RDBSS
- 重定向程序驱动程序 WDK，RDBSS
- 重定向驱动器缓冲子系统 WDK 文件系统
- RDBSS WDK 文件系统
- 小型重定向程序 WDK，RDBSS
- 非整体驱动程序 WDK
- 缓冲代码 WDK 网络重定向器
- I/o WDK 网络重定向器
- 内核网络重定向 WDK，RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b05b70c9e107153a07e2d068bed4257fb08db411
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838907"
---
# <a name="the-redirected-drive-buffering-subsystem"></a>重定向的驱动器缓冲子系统


## <span id="ddk_the_redirected_drive_buffering_subsystem_if"></span><span id="DDK_THE_REDIRECTED_DRIVE_BUFFERING_SUBSYSTEM_IF"></span>


重定向的驱动器缓冲子系统 (RDBSS) 作为内核模式文件系统驱动程序提供， *rdbss.sys*，该驱动程序包含在操作系统中，后者作为静态库（ *rdbsslib*）包含在 Windows 驱动程序工具包 (WDK) 中。 静态库复制 *rdbss.sys* 内核模式驱动程序中的代码。

原始方案是所有网络微重定向器都将与 *rdbss.sys* 内核驱动程序动态链接。 动态链接到 *rdbss.sys* 的驱动程序称为非单片驱动程序。 但是，此功能从未完全实现，因此，只有 Microsoft SMB 网络微型重定向程序链接会动态地 *rdbss.sys* ，这是一个非单一的驱动程序。 所有其他网络微型重定向程序（包括操作系统中包含的其他 Microsoft 重定向程序）都是针对 *rdbsslib* 库的链接，并静态地包含与 *rdbss.sys* 内核驱动程序相同的代码。 尽管 *rdbss.sys* 驱动程序和 *rdbsslib* 库中都使用相同的 RDBSS 源代码，但单一网络小型重定向程序驱动程序的大小较大，因为每个驱动程序都包含 *rdbss.sys* 中的大部分代码。 例如，在 Windows Server 2003 上，各种驱动程序的文件大小如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序</th>
<th align="left">文件大小</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>rdbss.sys</em></p></td>
<td align="left"><p>156 KB</p></td>
<td align="left"><p>RDBSS 设备驱动程序只能由 Microsoft SMB 小型重定向程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>mrxdav.sys</em></p></td>
<td align="left"><p>179 KB</p></td>
<td align="left"><p>Microsoft WebDAV 网络微型重定向程序驱动程序，其链接在很多 <em>rdbsslib</em>中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>rdrpdr.sys</em></p></td>
<td align="left"><p>185 KB</p></td>
<td align="left"><p>Microsoft 终端服务网络微型重定向程序驱动程序，它很多 <em>rdbsslib</em>。</p></td>
</tr>
</tbody>
</table>

 

RDBSS 与 i/o 管理器、缓存管理器、内存管理器、网络小型重定向程序以及其他内核系统进行通信。 RDBSS 支持以下功能：

-   定义了定义完善的机制，用于 RDBSS 和最小重定向器驱动程序之间的通信。

-   支持多个缓冲模式。 还提供了一些支持例程，可帮助网络小型重定向程序动态更改缓冲模式以启用实时共享。

-   网络小型重定向程序可指示支持各种选项，包括区分大小写的名称、UNC 命名、打印、管道、mailslots 和清理 (重用某些数据结构) 。

-   网络小型重定向程序支持命名空间、文件信息和连接缓存，以减少不必要的网络操作。

RDBSS 使用定义良好的通信机制。 RDBSS 导出大量可由小型重定向程序驱动程序和其他内核系统调用的函数以设置选项和执行各种操作。

小型重定向程序实现了许多回叫函数，RDBSS 使用这些函数与最小重定向程序驱动程序通信。 当微型重定向程序驱动程序首次开始 (在其 **DriverEntry** 例程) 中时，驱动程序会调用 RDBSS 函数来注册最小重定向程序驱动程序，并将包含指向这些回调函数的指针的结构传入 (调度表) 以及一些配置数据值。

必须在小型重定向程序驱动程序中实现的回调函数分为以下基本类别：

-   用于管理网络小型重定向程序数据结构的回调。

-   文件 i/o 操作的回调。
    -   同步文件 i/o 例程 (创建、关闭和清理，例如) 。
    -   异步文件 i/o 例程 (读取、写入。 FSTCL、IOCTL 和 lock，例如) 。 由于历史原因，网络小型重定向器中的这些同步文件 i/o 例程经常称为低 i/o 操作。

文件 i/o 回调应为同步，但位于低 i/o 类别中的函数除外。 低 i/o 例程可以异步操作，因此必须支持取消操作。

RDBSS 和微重定向器通常使用 RX \_ 上下文来传递信息。 RX \_ 上下文封装了大量信息，并包括指向当前 IRP 的指针。 此 RX 上下文数据结构有默认大小 \_ 。 此 RX \_ 上下文结构的大小可根据远程文件系统和网络微型重定向程序的要求进行扩展。 \_当微型重定向程序第一次向 RDBSS 注册 () 指定的数据值之一时，将定义用于此扩展 RX 上下文的大小。

RDBSS 和微重定向器还会广泛使用以下数据结构抽象：

-   服务器调用上下文 (SRV \_ 调用) -与每个已知文件系统服务器关联的上下文。

-   Net ROOT (NET \_ ROOT) -用户打开的共享的根目录。

-   虚拟网络根 (\_ net \_ ROOT) --服务器上共享的视图。 视图可以沿多个维度进行约束。 例如，可以将视图与登录 ID 相关联，这会限制可以对共享执行的操作。

-   文件控制块 (FCB) --与在客户端上打开的每个唯一文件关联的 RDBSS 数据结构。

-   文件对象扩展 (FOBX) --NT 文件对象的 RDBSS 扩展 \_ 。

-   服务器端打开上下文 (SRV \_ 打开) --远程共享上的文件的打开句柄。

RDBSS 具有非常灵活的缓冲支持。 RDBSS 可以设置为单独的缓冲区读取和写入请求。 还可以缓存文件大小和文件时间。 允许使用显式缓冲策略，并在打开文件服务器上的共享时设置这些策略。 还可以对单独的文件设置缓冲。

RDBSS 将尝试使用访问历史记录来减少不必要的网络请求的需要。 例如，如果对远程文件的打开请求失败，则 RDBSS 会缓存此信息。 如果客户端立即请求打开类似的文件，并在文件名中更改大小写，则 RDBSS 将无法请求在文件名中忽略大小写的远程文件系统。

 

 




