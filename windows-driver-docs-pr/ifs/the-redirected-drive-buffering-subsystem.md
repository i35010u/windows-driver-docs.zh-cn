---
title: 重定向的驱动器缓冲子系统
description: 重定向的驱动器缓冲子系统
ms.assetid: 901a8b3e-222a-44be-8279-765d8ec4ffe1
keywords:
- 网络重定向程序 WDK，RDBSS
- 重定向程序驱动程序 WDK RDBSS
- 重定向驱动器缓冲子系统 WDK 的文件系统
- RDBSS WDK 的文件系统
- 最小-重定向程序 WDK RDBSS
- 非整体化驱动程序 WDK
- 缓冲代码 WDK 网络重定向程序
- I/O WDK 网络重定向程序
- 内核网络重定向程序 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 269e7fdb33ea8cd91275fd17cc777e096d19c608
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385645"
---
# <a name="the-redirected-drive-buffering-subsystem"></a>重定向的驱动器缓冲子系统


## <span id="ddk_the_redirected_drive_buffering_subsystem_if"></span><span id="DDK_THE_REDIRECTED_DRIVE_BUFFERING_SUBSYSTEM_IF"></span>


作为内核模式文件系统驱动程序，提供重定向驱动器缓冲子系统 (RDBSS) *rdbss.sys*，这是包含与操作系统中，为静态库*rdbsslib.lib*、 哪些使用 Windows Driver Kit (WDK) 中包含。 静态库重复项中的代码*rdbss.sys*内核模式驱动程序。

原始方案已使用的所有网络微型重定向会将动态都链接*rdbss.sys*内核驱动程序。 为动态链接的驱动程序*rdbss.sys*称为非整体化驱动程序。 但是，此功能是永远不会完全实现，因此只有 Microsoft SMB 网络微型重定向链接到动态*rdbss.sys*和是一个非单一式驱动程序。 针对所有其他网络微型-重定向程序，包括包含操作系统，其他 Microsoft 重定向程序链接*rdbsslib.lib*库并以静态方式包含与相同的代码*rdbss.sys*内核驱动程序。 尽管在这种使用相同的 RDBSS 源代码*rdbss.sys*驱动程序和*rdbsslib.lib*库，整体化网络微型重定向程序驱动程序的大小较大以来中代码的大部分*rdbss.sys*随每个驱动程序。 例如，在 Windows Server 2003 上各种驱动程序的文件大小如下所示：

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
<td align="left"><p>仅由 Microsoft SMB 微型重定向 RDBSS 设备驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>mrxdav.sys</em></p></td>
<td align="left"><p>179 KB</p></td>
<td align="left"><p>Microsoft WebDAV 网络微型重定向程序驱动程序，它在很大程度的链接<em>rdbsslib.lib</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>rdrpdr.sys</em></p></td>
<td align="left"><p>185 KB</p></td>
<td align="left"><p>Microsoft 终端服务网络微型重定向程序驱动程序，它在很大程度的链接<em>rdbsslib.lib</em>。</p></td>
</tr>
</tbody>
</table>

 

RDBSS 与 I/O 管理器进行通信，缓存管理器中，内存管理器中，网络微型重定向程序和其他内核系统。 RDBSS 支持以下功能：

-   RDBSS 和最小重定向程序驱动程序之间的通信定义完善的机制。

-   支持多个缓冲模式。 此外，还有支持例程，以帮助网络微型重定向更改动态启用实时共享的缓冲模式。

-   网络微型重定向可以指示对各种选项，包括 UNC 命名打印、 管道、 mailslot 和清理 （重复使用一些数据结构） 的区分大小写名称的支持。

-   网络微型重定向为命名空间、 文件信息和连接缓存以减少不必要的网络操作提供支持。

RDBSS 使用定义完善的机制进行通信。 RDBSS 导出大量可由最小重定向程序驱动程序和其他内核系统，设置选项并执行各种操作调用的函数。

微型重定向实现多个 RDBSS 用于与最小重定向程序驱动程序通信的调用的回调函数。 最小重定向程序驱动程序的第一次启动 (在其**DriverEntry**例程)，驱动程序具有这些回调函数 （调度的指针的结构中注册微型重定向程序驱动程序并传递调用 RDBSS 函数表） 以及某些配置数据值。

必须在最小重定向程序驱动程序中实现的回调函数划分为以下基本类别：

-   若要管理网络微型重定向数据结构的回调。

-   文件 I/O 操作的回调。
    -   同步文件 I/O 例程 (创建、 close、 和清理，例如)。
    -   异步文件 I/O 例程 （读取、 写入。 FSTCL、 IOCTL 和锁定，例如）。 由于历史原因，在网络微型重定向这些同步文件 I/O 例程通常调用低 I/O 操作。

文件 I/O 回调都将是同步的但处于低 I/O 类别中的函数除外。 较低的 I/O 例程可以以异步方式运行，因此必须支持取消。

RDBSS 和最小重定向程序通常使用基本数据结构，RX\_上下文，以将信息传递。 RX\_上下文封装大量的信息，并包括指向当前 IRP 的指针。 没有此 RX 的默认大小\_上下文数据结构。 此 RX 大小\_上下文结构可以根据远程文件系统的需求进行扩展和网络微型重定向。 要为此使用的大小扩展 RX\_RDBSS （之一指定的数据值） 与第一次注册微型重定向时定义上下文。

RDBSS 和最小重定向程序也使广泛使用了以下数据结构抽象：

-   服务器调用上下文 (SRV\_调用)-与已知的文件系统的每个服务器关联的上下文。

-   Net 根 (NET\_根)-由用户打开共享的根。

-   虚拟网络的根 (V\_NET\_根)-在服务器上共享的视图。 该视图可以限制针对多个维度。 作为示例的视图可以是与登录 ID，这样可约束可以在共享执行的操作相关联。

-   文件控制块 (FCB)-与客户端上打开每个唯一文件相关联的 RDBSS 数据结构。

-   文件对象扩展 (FOBX)-NT 文件 RDBSS 扩展\_对象。

-   服务器端打开上下文 (SRV\_打开)-远程共享上的文件的打开句柄。

RDBSS 已缓冲非常灵活的支持。 可以设置 RDBSS 单独缓冲读取和写入请求。 也可以缓存文件的大小和文件时间。 允许显式缓冲策略和打开文件服务器上的共享时，可以设置这些。 此外可以在单个文件基础上设置缓冲。

RDBSS 将尝试使用访问历史记录以减少不必要的网络请求的需要。 例如，如果远程文件的打开请求失败，将通过 RDBSS 缓存此信息。 如果客户端立即请求以打开类似的文件，文件名中的用例的更改，RDBSS 将失败的请求忽略大小写文件名中的远程文件系统。

 

 




