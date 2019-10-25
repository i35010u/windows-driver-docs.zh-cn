---
title: 缓冲状态控件
description: 缓冲状态控件
ms.assetid: 16590332-9d0d-4d8b-8304-a3fa9269c0e2
keywords:
- RDBSS WDK 文件系统，缓冲状态
- 重定向驱动器缓冲子系统 WDK 文件系统，缓冲状态
- 缓冲状态 WDK RDBSS
- 分布式缓存一致性 WDK RDBSS
- 缓存 WDK RDBSS
- SRV_OPEN 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b664f3966da3bde490d0310bcd1633540918de6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841479"
---
# <a name="buffering-state-control"></a>缓冲状态控件


## <span id="ddk_buffering_state_control_if"></span><span id="DDK_BUFFERING_STATE_CONTROL_IF"></span>


RDBSS 提供了一个缓冲管理器，它是一种用于提供分布式缓存与各种网络微型重定向程序的一致性的机制。 此服务封装在 RDBSS 中的缓冲管理器中，用于处理更改缓冲状态的请求。 RDBSS 中的缓冲管理器跟踪并启动由各种网络微型重定向程序以及 RDBSS 生成的所有更改缓冲状态请求的操作。

典型的网络微重定向程序中的缓存一致性实现中有几个常见组件：

-   用于创建和打开文件例程的修改。

    在此路径中，将确定缓冲请求的类型，并向服务器发出适当的请求。 从网络小型重定向程序（可能为服务器）返回时，将根据创建或打开调用的结果更新与 FCB 关联的缓冲状态。

-   用于接收指示代码以处理来自服务器的更改缓冲状态通知的修改。

    如果检测到此类请求，则必须触发用于协调缓冲状态的本地机制。

-   一种用于更改作为 RDBSS 的一部分实现的缓冲状态的机制。 任何更改缓冲状态请求都必须确定请求适用的 SRV\_开放结构。

标识 SRV\_开放结构所涉及的计算工作量取决于网络小型重定向器的协议和详细信息。 在 SMB 协议中，机会锁（oplock）为缓存一致性提供必要的基础结构。 在 Windows 中的 SMB 协议实现中，使用 RDBSS 提供的多路复用 ID Api。 服务器将获取用于标识在服务器上打开的文件的多路复用 ID。 多路复用 Id 相对于打开它们的网络\_根（共享）。 因此，每个更改缓冲状态请求都由两个密钥标识： NetRootKey 和 SrvOpenKey，需要分别将其转换为相应的 NET\_ROOT 和 SRV\_开放结构。 为了更好地与资源获取/释放机制集成，并避免在各种网络微型重定向器中重复此项工作，RDBSS 提供了此服务。

RDBSS 中提供了两个例程，用于指示对 SRV\_开放结构的缓冲状态更改：

-   用于注册请求的[**RxIndicateChangeOfBufferingState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)

-   用于将 SRV\_开放结构与密钥相关联的[**RxIndicateChangeOfBufferingStateForSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)

请注意，密钥关联是不可逆的，并且将在关联的 SRV\_开放结构的生存期内进行。

需要使用辅助机制建立从多路复用 Id 到 SRV\_开放结构的映射的网络微重定向器可使用[**RxIndicateChangeOfBufferingState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)，而不需要此的网络微重定向器帮助可以使用[**RxIndicateChangeOfBufferingStateForSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)。

RDBSS 中的缓冲管理器在不同阶段处理这些请求。 它在多个列表之一中维护从各种基础网络微重定向程序收到的请求。

-   调度程序列表包含的所有请求都未建立与 SRV\_开放结构的适当映射。

-   处理程序列表包含已为其建立适当映射但尚未处理的所有请求。

-   LastChanceHandlerList 包含初始处理未成功的所有请求。 这通常发生在收到更改缓冲状态请求时，在共享模式下获取 FCB。 在这种情况下，oplock 中断请求只能由延迟的工作线程处理。

网络微型重定向程序驱动程序中的更改缓冲状态请求处理与 FCB 获取和释放协议过度交织。 这有助于确保周转时间较短。

RDBSS 提供以下例程来管理可由网络微型重定向程序驱动程序使用的缓冲状态：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>调用此例程来处理缓冲状态更改请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>调用此例程来注册缓冲状态更改请求（例如，oplock 中断指示）以供以后处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>调用此例程来注册缓冲状态更改请求（例如，oplock 中断指示）以供以后处理。</p></td>
</tr>
</tbody>
</table>

 

 

 




