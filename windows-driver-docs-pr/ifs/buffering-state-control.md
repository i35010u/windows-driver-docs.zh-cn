---
title: 缓冲状态控件
description: 缓冲状态控件
ms.assetid: 16590332-9d0d-4d8b-8304-a3fa9269c0e2
keywords:
- RDBSS WDK 的文件系统，缓冲状态
- 重定向驱动器缓冲子系统 WDK 的文件系统，缓冲状态
- 缓冲状态 WDK RDBSS
- 分布式的缓存协调性 WDK RDBSS
- 缓存 WDK RDBSS
- SRV_OPEN 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3042dc6dd1a967db8b6fad3f7b4b6c050a687f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391497"
---
# <a name="buffering-state-control"></a>缓冲状态控件


## <span id="ddk_buffering_state_control_if"></span><span id="DDK_BUFFERING_STATE_CONTROL_IF"></span>


RDBSS 提供缓冲管理器，用于提供各种网络的最小重定向结合使用的分布式的缓存协调性的机制。 此服务被封装在处理请求，以更改缓冲状态的 RDBSS 中的缓冲管理器。 RDBSS 中的缓冲管理器跟踪，并启动上缓冲生成由各种网络最小重定向以及 RDBSS 状态请求的所有更改的操作。

在典型的网络微型重定向的缓存协调性的实现中有多个常见组件：

-   若要创建和打开文件例程的修改。

    在此路径中，确定缓冲请求的类型，并向服务器发出相应的请求。 返回从网络微型重定向，和可能是服务器时，缓冲 FCB 与相关联的状态将会更新基于创建或打开调用的结果。

-   修改，以便收到指示代码来处理从服务器更改缓冲状态通知。

    如果检测到此类请求，则必须触发本地的机制来协调缓冲状态。

-   用于更改 RDBSS 的一部分实现的缓冲状态的机制。 缓冲状态请求的任何更改必须标识 SRV\_打开请求应用的结构。

标识 SRV 所涉及的计算工作量\_打开结构取决于协议和网络微型重定向的详细信息。 SMB 协议在机会锁 (oplock) 的缓存一致性提供必要的基础结构。 在 Windows 中的 SMB 协议实现中，使用多路复用 ID Api 提供通过 RDBSS。 在服务器获取选择用于标识在服务器上打开的文件的多路复用 ID。 多路复用 Id 是相对于 NET\_根 （共享） 打开它们。 因此，缓冲状态请求的每项更改由两个密钥： NetRootKey 和 SrvOpenKey，需要转换为相应的 NET\_根和 SRV\_分别打开结构。 若要与资源获取/释放机制提供更好地集成并避免重复此操作在各种网络最小重定向，RDBSS 提供此服务。

有两个例程 RDBSS 中提供的该值指示缓冲状态更改为 SRV\_打开结构：

-   [**RxIndicateChangeOfBufferingState** ](https://msdn.microsoft.com/library/windows/hardware/ff554485)注册请求

-   [**RxIndicateChangeOfBufferingStateForSrvOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff554490)为关联的 SRV\_与键打开结构

请注意，键的关联是不可逆的并且将持续的生存期相关联的 SRV\_打开结构。

网络微型-重定向程序需要辅助机制用于建立从多路复用 Id 映射到 SRV\_打开结构可以使用[ **RxIndicateChangeOfBufferingState**](https://msdn.microsoft.com/library/windows/hardware/ff554485)，尽管可以使用网络微型-重定向程序不需要这种辅助[ **RxIndicateChangeOfBufferingStateForSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff554490)。

RDBSS 中的缓冲管理器在不同阶段中处理这些请求。 它维护从各种基础网络微型-重定向程序在多个列表之一中接收的请求。

-   调度程序列表包含的所有请求为其映射到 SRV 的适当\_打开结构未建立。

-   处理程序列表包含所有相应的映射已建立，但尚未处理的请求。

-   LastChanceHandlerList 包含所有为其初始处理未成功的请求。 这通常发生在 FCB 已获取在共享模式下在缓冲状态请求的更改时接收到的时间。 在这种情况下，只能由延迟的辅助线程处理 oplock 破坏请求。

FCB 获得和释放协议而更改缓冲状态请求网络微型重定向程序驱动程序中处理。 这有助于确保周转时间更短。

RDBSS 提供了以下例程来管理网络微型重定向程序驱动程序可以使用的缓冲状态：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554335" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554335)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>此例程调用以处理缓冲的状态更改请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554485" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554485)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>此例程称为注册以供将来处理缓冲状态更改请求 （oplock 中断指示）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554490" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554490)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>此例程称为注册以供将来处理缓冲状态更改请求 （oplock 中断指示）。</p></td>
</tr>
</tbody>
</table>

 

 

 




