---
title: 网络数据结构
description: 网络数据结构
keywords:
- NET_BUFFER
- NET_BUFFER_LIST
- NET_BUFFER_LIST_CONTEXT
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
- 包 WDK 网络，数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc11a6b6772b9055bf596e58ff284e7dc562f84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840897"
---
# <a name="network-data-structures"></a>网络数据结构





网络数据包含通过网络发送或接收的数据包。 NDIS 提供了用于描述和组织此类数据的数据结构。 用于 NDIS 6.0 和更高版本的主网络数据结构为：

-   [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)
-   [**网络 \_ 缓冲区列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)
-   [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)

下图说明了这些结构之间的关系。

![说明 ndis 6.0 网络数据结构的示意图](images/netbufferstructures.png)

在 NDIS 6.0 和更高版本中， [**NET \_ BUFFER**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 是用于封装网络数据的基本构建基块。 每个网络 \_ 缓冲区结构都有一个 MDL 链。 MDLs 将数据缓冲区的地址映射到 NET BUFFER 结构指定的数据空间 \_ 。 此数据映射与 NDIS 5 的 MDL 链完全相同。*x* 及更早版本的驱动程序在 [**NDIS \_ 数据包**](/previous-versions/windows/hardware/network/ff557086(v=vs.85)) 结构中使用。 NDIS 提供操作 MDL 链的函数。

可以将多个网络 \_ 缓冲区结构附加到网络 \_ 缓冲区 \_ 列表结构。 NET \_ BUFFER 结构组织为以 NULL 结尾的单向链接列表。 只有产生了网络 \_ 缓冲区列表结构的驱动程序 \_ 或 NDIS 才能直接修改链接列表，以插入和删除网络 \_ 缓冲区结构。

[**NET \_缓冲区列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构包含描述附加到列表的所有 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构的信息。 如果驱动程序需要额外的空间来存储上下文信息，则驱动程序可以将此类信息存储在网络 \_ 缓冲区 \_ 列表 \_ 上下文结构中。 NDIS 提供函数以分配、释放和访问网络 \_ 缓冲区 \_ 列表上下文结构中的数据 \_ 。

可以附加多个网络 \_ 缓冲区 \_ 列表结构，以形成网络 \_ 缓冲区 \_ 列表结构的列表。 NET \_ BUFFER \_ list 结构被组织为以 NULL 结尾的单向链接列表。 驱动程序可以直接修改链接列表，以插入和删除网络 \_ 缓冲区 \_ 列表结构。

## <a name="related-topics"></a>相关主题


[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)

[网络 \_ 缓冲区结构](net-buffer-structure.md)

[**网络 \_ 缓冲区列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[网络 \_ 缓冲区 \_ 列表结构](net-buffer-list-structure.md)

[**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)

[网络 \_ 缓冲区 \_ 列表 \_ 上下文结构](net-buffer-list-context-structure.md)

 

