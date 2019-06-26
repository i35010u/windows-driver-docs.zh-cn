---
title: 网络数据结构
description: 网络数据结构
ms.assetid: c29aaae6-6f68-404a-90dc-bae005ac9b6e
keywords:
- NET_BUFFER
- NET_BUFFER_LIST
- NET_BUFFER_LIST_CONTEXT
- 网络数据 WDK，结构
- 数据 WDK 网络结构
- 数据包 WDK 网络、 数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c5534ae67d8e5ffb3358b0a75346b56b302817e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386222"
---
# <a name="network-data-structures"></a>网络数据结构





网络数据包含的发送或通过网络接收的数据包。 NDIS 提供的数据结构来描述和组织此类数据。 NDIS 6.0 及更高版本的主网络数据结构是：

-   [**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)
-   [**NET\_缓冲区列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)
-   [**NET\_BUFFER\_LIST\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)

下图说明了这些结构之间的关系。

![演示如何 ndis 6.0 网络数据结构的关系图](images/netbufferstructures.png)

NDIS 6.0 及更高版本， [ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)是用于打包网络数据的基本构造块。 每个网络\_缓冲区结构具有 MDL 链。 MDLs 映射到数据缓冲区的数据的地址空间的 NET\_缓冲区结构指定。 此数据映射等同于 MDL 链接该 NDIS 5。*x*以及早期驱动程序中使用[ **NDIS\_数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构。 NDIS 提供函数来操作 MDL 链。

多个 NET\_缓冲区结构可以附加到 NET\_缓冲区\_列表结构。 NET\_缓冲区结构组织为以 NULL 结尾的单向链接列表。 源自网络驱动程序\_缓冲区\_列表结构或 NDIS，应修改的链接的列表直接插入和删除 NET\_缓冲区结构。

[**NET\_缓冲区列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构包含用于描述所有信息[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)附加到列表的结构。 如果驱动程序的上下文信息需要额外的空间，该驱动程序可此类信息存储在 NET\_缓冲区\_列表\_上下文结构。 NDIS 提供可以分配、 释放和访问网络中的数据的函数\_缓冲区\_列表\_上下文结构。

多个 NET\_缓冲区\_列表结构可以附加到窗体中的 NET 列表\_缓冲区\_列表结构。 NET\_缓冲区\_列表结构组织为以 NULL 结尾的单向链接列表。 驱动程序可以修改的链接的列表直接插入和删除 NET\_缓冲区\_列表结构。

## <a name="related-topics"></a>相关主题


[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)

[NET\_缓冲区结构](net-buffer-structure.md)

[**NET\_缓冲区列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

[NET\_缓冲区\_列表结构](net-buffer-list-structure.md)

[**NET\_BUFFER\_LIST\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)

[NET\_缓冲区\_列表\_上下文结构](net-buffer-list-context-structure.md)

 

 






